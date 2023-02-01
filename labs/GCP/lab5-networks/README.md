### Topologia
![image](https://user-images.githubusercontent.com/59710101/216000784-fb51a138-5eeb-464b-b43b-b29705c4b1f4.png)

## Comandos para criar via console
```sh
gcloud compute networks create managementnet --project=qwiklabs-gcp-00-6e10122d2007 --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional && gcloud compute networks subnets create managementsubnet-us --project=qwiklabs-gcp-00-6e10122d2007 --range=10.240.0.0/20 --stack-type=IPV4_ONLY --network=managementnet --region=us-west3

```
ou

```sh
gcloud compute networks create privatenet --subnet-mode=custom

## Criando subnets
gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-west3 --range=172.16.0.0/24

gcloud compute networks subnets create privatesubnet-eu --network=privatenet --region=europe-west1 --range=172.20.0.0/20
```

Listando
```sh
gcloud compute networks list

```
Criando regras de firewall
```sh

gcloud compute firewall-rules create privatenet-allow-icmp-ssh-rdp --direction=INGRESS --priority=1000 --network=privatenet --action=ALLOW --rules=icmp,tcp:22,tcp:3389 --source-ranges=0.0.0.0/0

```

Criando VM 
```sh
gcloud compute instances create privatenet-us-vm --zone=us-west3-c --machine-type=e2-micro --subnet=privatesubnet-us --image-family=debian-11 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=privatenet-us-vm

```
