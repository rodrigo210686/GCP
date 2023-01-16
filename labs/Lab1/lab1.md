# Lab Diagram
![image](https://user-images.githubusercontent.com/59710101/212776521-d9bc81b8-2093-40d1-bf73-5411a01b0cee.png)

Documento com os passsos em anexo

## Criando uma imagem baseada em uma VM via CLI
gcloud compute images create custom-webpage --source-disk=custom-webpage --source-disk-zone=us-central1-a --family=webserver

## Deprecated a image by CLI
gcloud compute images deprecate webserver-base --state DEPRECATED
