# Cluster de production 

## Cluster Kubernetes managé 
* GKE - Google Kubernetes Engine 
    ```
    gcloud init
    gcloud container vlusters create kube-demo --cluster-version= latest --num-nodes 3 
    ```
* AKS - Azure Container Service
    ```
    az group create --name kube-groupe --location westeurope
    
    az aks create --name kube-demo ... 
    ```
* EKS - Amazon Elastic Container Service 
* DigitalOcean
* OVH
* ...

## De nombreuses solutions
* kubeadm
* kops
* kubespray
* rancher
* pharos
* docker ee (swarm et kubernetes)
* terraform + ansible
