```sh
export MY_ZONE=

export MY_ZONE=us-central1-a

#####Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2


kubectl version



```
