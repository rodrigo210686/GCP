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

```sh

```` 

```sh

```` 

```sh

```` 

```sh

```` 

```sh

```` 

```sh

```` 
