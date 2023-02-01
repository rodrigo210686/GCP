### Topologia
![image](https://user-images.githubusercontent.com/59710101/216000784-fb51a138-5eeb-464b-b43b-b29705c4b1f4.png)

## Comandos para criar via console
```sh
gcloud compute networks create managementnet --project=qwiklabs-gcp-00-6e10122d2007 --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional && gcloud compute networks subnets create managementsubnet-us --project=qwiklabs-gcp-00-6e10122d2007 --range=10.240.0.0/20 --stack-type=IPV4_ONLY --network=managementnet --region=us-west3

```
ou

```sh
gcloud compute networks create privatenet --subnet-mode=custom

gcloud compute networks subnets create privatesubnet-us --network=privatenet --region=us-west3 --range=172.16.0.0/24
```

Listando
```sh
gcloud compute networks list

```
