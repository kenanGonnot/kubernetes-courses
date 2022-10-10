# La plateforme Kubernetes 
* Kubernetes / k8s / kube 
* google

## Fonctionnalités
* Gestion d'applications tournant dans des containers
    * déploiement 
    * scaling
    * self-healing
* Applications stateless et stateful 
* Secrets et des Configurations
* Long-running process et batch jobs
* RBAC 
* cncf.io

## Concepts de base
### Cluster
* Ensemble de nodes Linux ou Windows 
* Nodes Masters + nodes Workers (pareil que swarm)
* Un master expose l'api Server - Entrée 

### Pods 
* Plus petite unité applicative qui tourne sur un cluster k8s
* GRoupe de containers qui partagent un réseau 

### Deployment
* Permet de gérer un ensemble de Pods identiques (màj / rollback)

### Service 
* Expose les applications des Pods à l'intérieur ou à l'extérieur du cluster

## Les ressources principales 
* Workload 
* Configuration
* Extension du cluster
* Network
* Stockage
* RBAC

## Fichers en yaml 
* Ressemble bcp à docker-compose.yml
* Exemple de spécification 
    * Pod
    * Service
    * Deployment

## Processus
* "Kubelet": Responsable du redémarrage des containers d'un Pod en cas de défaillance
* "kube-apiserver": fait partie du control plane assurant la gestion du cluster
* attention kube-proxy ne fait pas partie du control plane

