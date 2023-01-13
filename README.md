# GCP 
## Cheat  | Palavras/Serviços chaves
https://github.com/priyankavergadia/google-cloud-4-words

# Documentações sobre billing

https://cloud.google.com/billing/docs/how-to/billing-access

https://support.google.com/a/answer/9807615

## View Sample Billing Data with BigQuery
Part of working with billing data is working with data exported to BigQuery. In this lab, we are going to view sample billing exports maintained by Google, and conduct queries against a public dataset of billing exports. This will be a fun lab in that we can play around with SQL queries in BigQuery and see what kind of results we can get. Let's get started!

Once you are in your lab project, we will need to get into the BigQuery web console. From the top left menu, scroll down to Big Data, and select BigQuery.

Now that we are in BigQuery, let's look at the sample dataset we are going to work with. We are going to view all columns in our example table to see what fields are included. From the large Query Editor box, copy and paste the following query, then click the Run button:

```sql
SELECT *  
FROM `cloud-training-prod-bucket.arch_infra.billing_data`

```
If we click the Results tab underneath, we can view the entire table we are going to work with. Feel free to experiment with other queries such as ordering by cost or usage amount by adding the below string to your query to sort by the column of your choice:
```sql
SELECT *  
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
ORDER BY cost DESC

```
In this query, we are bringing up the entire table contents, but sorting by the highest cost first. You can experiment with other fields as well.

Let's now do some specific queries. In the same Query editor box, delete the existing contents, and enter the below query to find all charges that were more than 3 dollars:
```sql
SELECT product, resource_type, start_time, end_time,  
cost, project_id, project_name, project_labels_key, currency, currency_conversion_rate,
usage_amount, usage_unit
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
WHERE (cost > 3)

```
Next let’s find which product had the highest total number of records:


```sql
SELECT product, COUNT(*)
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
GROUP BY product
LIMIT 200

```
Looks like Pub/Sub is pretty popular here...

Finally, let’s see which product most frequently cost more than a dollar:

```sql
SELECT product, cost, COUNT(*)
FROM `cloud-training-prod-bucket.arch_infra.billing_data`
WHERE (cost > 1)
GROUP BY cost, product
LIMIT 200

```

```sql


```

```sql


```


## CloudShell

https://github.com/ACloudGuru/gcp-cloud-engineer

Verificar configurações de perfil cli
```sh
#gcloud config list

[accessibility]
screen_reader = True
[component_manager]
disable_update_check = True
[compute]
gce_metadata_read_timeout_sec = 30
[core]
account = cloud_user_p_70b606b9@linuxacademygclabs.com
disable_usage_reporting = True
project = playground-s-11-54ddeda2
[metrics]
environment = devshell
``` 


Move diretório local para bucket
```sh
## lista buckets
gsutil ls

## move arquivos
gsutil mv -p 1-col.xlsm  gs://rodrigo-teste2/colaboradoresl.xlsm

### Criar bucket
gsutil mb gs://rodrigo-teste-3
``` 
comandos mais usados bucket
``` sh
pwd
ls

gcloud config list

gsutil ls
gsutil ls gs://storage-lab-console/
gsutil ls gs://storage-lab-console/**

gsutil mb --help

gsutil mb -l northamerica-northeast1 gs://storage-lab-cli
gsutil ls

gsutil label get gs://storage-lab-console/
gsutil label get gs://storage-lab-console/ >bucketlabels.json
cat bucketlabels.json

gsutil label get gs://storage-lab-cli/
gsutil label set bucketlabels.json gs://storage-lab-cli/
gsutil label get gs://storage-lab-cli/

gsutil label ch -l "extralabel:extravalue" gs://storage-lab-cli

gsutil versioning get gs://storage-lab-cli/
gsutil versioning set on gs://storage-lab-cli/
gsutil versioning get gs://storage-lab-cli/

gsutil ls gs://storage-lab-cli/
gsutil cp README-cloudshell.txt gs://storage-lab-cli/
gsutil ls gs://storage-lab-cli/

gsutil ls gs://storage-lab-cli/
gsutil ls -a gs://storage-lab-cli/
gsutil rm gs://storage-lab-cli/README-cloudshell.txt
gsutil ls gs://storage-lab-cli/
gsutil ls -a gs://storage-lab-cli/

gsutil cp gs://storage-lab-console/** gs://storage-lab-cli/
gsutil ls gs://storage-lab-cli/
gsutil ls -a gs://storage-lab-cli/

gsutil acl ch -u AllUsers:R gs://storage-lab-cli/Selfie.jpg
```


## Google CLoud Storage GCS

Storage Class info

![image](https://user-images.githubusercontent.com/59710101/212160679-66e7c276-da01-447f-ae02-3c674b1aac87.png)

## GCE Google computer Engine

```sh
### Cria uma vm
gcloud compute instances create ziri-vm

## Lista tipos de instancia filtrando uma zona
gcloud compute machine-types list --filter="NAME:f1-micro AND ZONE~us-west"

### Definindo uma zona e região para subir uma instancia
gcloud config set compute/zone us-west2-b

gcloud config set compute/region us-west2

### Criando a instancia depois das configurações de região

cloud compute instances create --machine-type=f1-micro ziri-vm

### depois de criar a VM para gerar a chave ssh vc precisa logar nela a partir do Cloud Shell. No primeiro login será criada a chave.

gcloud compute ssh ziri-vm

### Pegar o metadata 
curl -H "Metadata-Flavor:Google" metadata.google.internal/computeMetadata/v1


```

User Data 

```sh
#! /bin/bash

#
# Echo commands as they are run, to make debugging easier.
# GCE startup script output shows up in "/var/log/syslog" .
#
set -x


#
# Stop apt-get calls from trying to bring up UI.
#
export DEBIAN_FRONTEND=noninteractive


#
# Make sure installed packages are up to date with all security patches.
#
apt-get -yq update
apt-get -yq upgrade


#
# Install Google's Stackdriver logging agent, as per
# https://cloud.google.com/logging/docs/agent/installation
#
curl -sSO https://dl.google.com/cloudagents/install-logging-agent.sh
bash install-logging-agent.sh


#
# Install and run the "stress" tool to max the CPU load for a while.
#
apt-get -yq install stress
stress -c 8 -t 120


#
# Report that we're done.
#

# Metadata should be set in the "lab-logs-bucket" attribute using the "gs://mybucketname/" format.
log_bucket_metadata_name=lab-logs-bucket
log_bucket_metadata_url="http://metadata.google.internal/computeMetadata/v1/instance/attributes/${log_bucket_metadata_name}"
worker_log_bucket=$(curl -H "Metadata-Flavor: Google" "${log_bucket_metadata_url}")

# We write a file named after this machine.
worker_log_file="machine-$(hostname)-finished.txt"
echo "Phew!  Work completed at $(date)" >"${worker_log_file}"

# And we copy that file to the bucket specified in the metadata.
echo "Copying the log file to the bucket..."
gsutil cp "${worker_log_file}" "${worker_log_bucket}"

```
