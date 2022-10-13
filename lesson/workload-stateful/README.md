# Workflow stateful 

## Volume 
* Découple les données du cycle de vie d'un container 
* Permet aux containers d'un même Pod de partager des données 

#### Volume, ex: EmptyDir
* Lié au cycle de vie d'un Pod
* Vide à la création

#### Volume, ex: hostPath
* Montage d'une ressource de la machine hôte dans un Pod (repértoire, fichier, ..)
* Exemples: monitoring, communication avec le daemon Docker, ...

#### Volume, ex: Amazon awsElasticBlockStore (EBS)
* Montage d'un EBS dans un Pod 
* Quelques contraintes 
    * Disponible pour des VMs sur AWS
    * utilisé par une instance EC2 à la fois
    * même région et AZ 



#### Volume, ex: Google gcePersistentDisk (PD)
* Montage d'un PD dans un Pod 
* Quelques contraintes 
    * disponible pour des VMs sur GCP
    * une seule VM avec un accès en écriture 
    * même projet et zone que le PD 

### PersistentVolumeClaim
* Demande de stockage 
* Spécifie des contraintes
    * taille
    *  type
    *  mode d'accès
*  Consomme un PV existant ou provisionnement dynamique via une StorageClass
*  Utilisé par un Pod 


## StatefulSet 
* Utilisé pour la gestion d'applications Stateful
    * Ex: cluster de base de données 
* Management d'un ensemble de Pods non interchangeables
* Chaque Pod à 
    * un nom constant 
    * un identifiant réseau persistant 
    * son propre stockage 
* Mise en place / suppression de l'application selon un ordre défini 

## rook.io
* Orchestrateur de stockage pour k8s
* https://rook.io
* Supporte différent type de stockage 
* Mini exercice: https://gitlab.com/lucj/k8s-exercices/-/blob/master/Application-Stateful/rook.md

https://gitlab.com/lucj/k8s-exercices/-/blob/master/Application-Stateful/longhorn.md