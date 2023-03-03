## Criando a chave em um servidor qualquer

ssh-keygen -t rsa -f ~/.ssh/KEY_FILENAME -C USERNAME -b 2048


## Acesse a console GCP e gere a chave para instancia

```sh
gcloud compute os-login ssh-keys add \
    --key-file=KEY_FILE_PATH \
    --project=PROJECT \
    --ttl=EXPIRE_TIME
    
   Exemplo
   gcloud compute os-login ssh-keys add \
    --key-file=/home/hypercloud_rodrigo/mykey \
    --project=landingzone-prod-01 \
    --ttl=90d
    
    ``` 
    Pegue a chave gerada e inclua na VM
