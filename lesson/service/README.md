# Services

NodePort: permet d'exposer une application à l'extérieur du cluster

## Les commandes de base
```shell
# creation d'un service
$ kubectl apply -f PATH
$ kubectl expose...
$ kubectl create service 

# Liste de l'ensemble des services
$ kubectl get service 
$ kubectl get svc

#Principales informations concernant un service 
$ kubectl get svc/SERVICE_NAME

# Informations détaillées d'un service 
$ kubectl describe svc SERVICE_NAME

# Suppression d'un service
$ kubectl delete svc/SERVICE_NAME
```