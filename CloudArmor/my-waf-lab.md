ca-lab-vpc - > my-lab-waf

## Crie uma VPC customizada

Cria VPC
```sh
gcloud compute networks create my-lab-waf --subnet-mode custom

```

Criar subnet
```sh

gcloud compute networks subnets create my-lab-waf-subnet \
        --network my-lab-waf --range 10.0.0.0/24 --region us-central1
```` 
Firewalls rules

The first firewall rule named allow-js-site allows all IPs to access the external IP of the test application's website on port 3000.

The second firewall rule named allow-health-check allows health-checks from source IP of the load balancers.
```sh
gcloud compute firewall-rules create allow-js-site --allow tcp:3000 --network my-lab-waf
```` 

firewall rule to allow health-checks from the Google health-check ranges:
```sh
gcloud compute firewall-rules create allow-health-check \
    --network=my-lab-waf \
    --action=allow \
    --direction=ingress \
    --source-ranges=130.211.0.0/22,35.191.0.0/16 \
    --target-tags=allow-healthcheck \
    --rules=tcp
```` 

## Set up the test application
Create the test application, in this case, the OWASP Juice Shop web server. When you create the compute instance, you use a container image to ensure the server has the appropriate services. You deploy this server in the us-central1-a and has a network tag that allows health checks.

Create the OWASP Juice Shop application
Use the open source well-known OWASP Juice Shop application to serve as the vulnerable application. You can also use this application to do OWASP security challenges through the OWASP website.

```sh
gcloud compute instances create-with-container owasp-juice-shop-app --container-image bkimminich/juice-shop \
     --network my-lab-waf \
     --subnet my-lab-waf-subnet \
     --private-network-ip=10.0.0.3 \
     --machine-type n1-standard-2 \
     --zone us-central1-a \
     --tags allow-healthcheck
```` 

Create unmanaged instance  group
```sh
gcloud compute instance-groups unmanaged create juice-shop-group \
    --zone=us-central1-a
```` 

Add the Juice Shop Google Compute Engine (GCE) instance to the unmanaged instance group:
```sh
gcloud compute instance-groups unmanaged add-instances juice-shop-group \
    --zone=us-central1-a \
    --instances=owasp-juice-shop-app
```` 
Set the named port to that of the Juice Shop application:
```sh
gcloud compute instance-groups unmanaged set-named-ports \
juice-shop-group \
   --named-ports=http:3000 \
   --zone=us-central1-a
```` 
## Configure Load Balancer
create the health-check for the Juice Shop service port:
```sh
gcloud compute health-checks create tcp tcp-port-3000 \
        --port 3000
```` 
create the backend service parameters:
```sh
gcloud compute backend-services create juice-shop-backend \
        --protocol HTTP \
        --port-name http \
        --health-checks tcp-port-3000 \
        --enable-logging \
        --global
```` 
Add the Juice Shop instance group to the backend service:
```sh
 gcloud compute backend-services add-backend juice-shop-backend \
        --instance-group=juice-shop-group \
        --instance-group-zone=us-central1-a \
        --global

```` 
create the URL map to send incoming requests to the backend:
```sh
gcloud compute url-maps create juice-shop-loadbalancer \
        --default-service juice-shop-backend
```` 
create the Target Proxy to route incoming requests the URL map:
```sh
gcloud compute target-http-proxies create juice-shop-proxy \
        --url-map juice-shop-loadbalancer
```` 
create the forwarding rule for the Load Balancer:
```sh
gcloud compute forwarding-rules create juice-shop-rule \
        --global \
        --target-http-proxy=juice-shop-proxy \
        --ports=80
```` 
Pegue o IP do ALB e valide se está on. Costuma demorar cerca de 5 minutos
```sh
PUBLIC_SVC_IP="$(gcloud compute forwarding-rules describe juice-shop-rule  --global --format="value(IPAddress)")"
echo $PUBLIC_SVC_IP

curl -Ii http://$PUBLIC_SVC_IP
```` 

### Verificando as vulnerabilidades
LFI vulnerability: path traversal

Local File Inclusion is the process of observing files present on the server by exploiting lack of input validation in the request to potentially expose sensitive data. The following shows a path traversal is possible. In your browser or with curl, observe an existing path served by the application.

```sh
curl -Ii http://$PUBLIC_SVC_IP/ftp

curl -Ii http://$PUBLIC_SVC_IP/ftp/../

````

RCE vulnerability

Remote Code Execution includes various UNIX and Windows command injection scenarios allowing attackers to execute OS commands usually restricted to privileged users. The following shows a simple ls command execution passed in.

```sh
curl -Ii http://$PUBLIC_SVC_IP/ftp?doc=/bin/ls
```

well-known scanner's access

Both commercial and open source scan applications for various purposes, including to find vulnerabilities. These tools use well-known User-Agent and other Headers. Observe curl works with a well-known User-Agent Header.

```sh
curl -Ii http://$PUBLIC_SVC_IP -H "User-Agent: blackwidow"
```
protocol attack: HTTP splitting

Some web applications use input from the user to generate the headers in the responses. If the application doesn't properly filter the input, an attacker can potentially poison the input parameter with the sequence %0d%0a (the CRLF sequence that is used to separate different lines).

The response could then be interpreted as two responses by anything that happens to parse it, like an intermediary proxy server, potentially serving false content in subsequent requests. Insert the sequence %0d%0a into the input parameter, which can lead to serving a misleading page.

```sh
curl -Ii "http://$PUBLIC_SVC_IP/index.html?foo=advanced%0d%0aContent-Length:%200%0d%0a%0d%0aHTTP/1.1%20200%20OK%0d%0aContent-Type:%20text/html%0d%0aContent-Length:%2035%0d%0a%0d%0a<html>Sorry,%20System%20Down</html>"
```
session fixation

```sh
curl -Ii http://$PUBLIC_SVC_IP -H session_id=X
```

### Define Cloud Armor WAF rules

List predefined rules
```sh
gcloud compute security-policies list-preconfigured-expression-sets
```
Create the Cloud Armor security policy using the following command in Cloud Shell:
```sh
gcloud compute security-policies create block-with-modsec-crs \
    --description "Block with OWASP ModSecurity CRS"
```
update the security policy default rule.

```sh
gcloud compute security-policies rules update 2147483647 \
    --security-policy block-with-modsec-crs \
    --action "deny-403"
```

Since the default rule is configured with action deny, you must allow access from your IP. Please find your public IP (curl, ipmonkey, whatismyip, etc):
```sh
MY_IP=$(curl ifconfig.me)
```
Add the first rule to allow access from your IP (INSERT YOUR IP BELOW):
```sh
gcloud compute security-policies rules create 10000 \
    --security-policy block-with-modsec-crs  \
    --description "allow traffic from my IP" \
    --src-ip-ranges "$MY_IP/32" \
    --action "allow"
```
update the security policy to block LFI attacks
```sh
gcloud compute security-policies rules create 9000 \
    --security-policy block-with-modsec-crs  \
    --description "block local file inclusion" \
     --expression "evaluatePreconfiguredExpr('lfi-stable')" \
    --action deny-403
```
update the security policy to block Remote Code Execution (rce).
```sh
gcloud compute security-policies rules create 9001 \
    --security-policy block-with-modsec-crs  \
    --description "block rce attacks" \
     --expression "evaluatePreconfiguredExpr('rce-stable')" \
    --action deny-403
```
Update the security policy to block security scanners.
```sh
gcloud compute security-policies rules create 9002 \
    --security-policy block-with-modsec-crs  \
    --description "block scanners" \
     --expression "evaluatePreconfiguredExpr('scannerdetection-stable')" \
    --action deny-403
```
update the security policy to block protocol attacks.
```sh
gcloud compute security-policies rules create 9003 \
    --security-policy block-with-modsec-crs  \
    --description "block protocol attacks" \
     --expression "evaluatePreconfiguredExpr('protocolattack-stable')" \
    --action deny-403
```
Update the security policy to block session fixation.
```sh
gcloud compute security-policies rules create 9004 \
    --security-policy block-with-modsec-crs \
    --description "block session fixation attacks" \
     --expression "evaluatePreconfiguredExpr('sessionfixation-stable')" \
    --action deny-403
```
### Attach the security policy to the backend service:
```sh
gcloud compute backend-services update juice-shop-backend \
    --security-policy block-with-modsec-crs \
    --global
```
```sh

```
```sh

```

