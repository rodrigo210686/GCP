# GCP 
Exam:
https://www.examtopics.com/exams/google/associate-cloud-engineer/
## Cheat  | Palavras/Serviços chaves
https://github.com/priyankavergadia/google-cloud-4-words

# Documentações sobre billing

https://cloud.google.com/billing/docs/how-to/billing-access

https://support.google.com/a/answer/9807615

https://cloud.google.com/billing/docs/how-to/billing-access

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

### Criando preemtible(spot) isntances. São instancias mais baratas que desligam após 24h
gcloud compute instances create t1 t2 t3 --project=planning-and-261-29def703 --zone=us-central1 --zone=us-central1-a --machine-type=e2-micro --preemptible

```

#### Instalando agentes e chaves RSA
```sh
In this lesson we will launch a VM and create a custom key to access it from outside of
our environment.
Commands to create a custom key
`ssh-keygen -t rsa`
Curl data for the logging agent
``curl -sSO https://dl.google.com/cloudagents/add-logging-agent-repo.sh``
install the logging agent
``sudo bash add-logging-agent-repo.sh --also-install``
check to see if fluentd is active
``sudo service google-fluentd status``
Curl data for the monitoring agent
``curl -sSO https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh
``
Install the monitoring agent
``sudo bash add-monitoring-agent-repo.sh --also-install``
Start the stackdriver service
``sudo service stackdriver-agent start``
check the status
``sudo service stackdriver-agent status``
```

# GKE 

```sh
Creating your cluster
gcloud container clusters create acloud-cluster --num-nodes=3
--zone=us-central1-a

Authorize to connect to your pods
gcloud container clusters get-credentials acloud-cluster
--zone=us-central1-a

deploy an application
kubectl create deployment hello-server
--image=us-docker.pkg.dev/google-samples/containers/gke/hello--app
:1.0

Create a service to expose the deployment
kubectl expose deployment helo-server --type LoadBalancer --port 80
--target-port 8080

Check your pods
kubectl get pods

Grab the IP address for the service
kubectl get services hello-server

Update the cluster enable monitoring
gcloud container clusters update acloud-cluster --zone=us-central1-a --logging=SYSTEM,WORKLOAD --monitoring=SYSTEM

Resize the cluster
gcloud container clusters resize acloud-clusters --num-nodes=2 --zone=us-central1-a

Implement autoscaling
gcloud container clusters update cloud-cluster --enable-autoscaling --min-nodes 2 --max-nodes 5 --zone=us-central1-a

Create a node pool
gcloud container node-pools create cloud-pool --cluster acloud-cluster --zone=us-central1-a



```
