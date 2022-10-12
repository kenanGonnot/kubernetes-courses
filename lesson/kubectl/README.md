# Kubectl - Tips and Tricks


## kubectl-aliases
* https://github.com/ahmetb/kubectl-aliases
## Plugins 
* Permet d'étendre les fonctionnalités de kubectl
* https://github.com/ahmetb/krew

## Gestion du cluster 


## Gestion des ressources
### Imperative vs Declarative 
#### Imperative Dev 
* Gestion des ressources en ligne de commande 
* Approche simple pour aller vite
* Pas de suivi des changement dans un VCS 
* Nombreuses commandes

#### Déclarative Prod
* Fichier de configuration pour chaque ressource
* Nécessite une connaissance des ressources
* Suivi des changements dans un VCS
* Commandes apply 
* Analyse automatique des diff

#### api ressources
```
kubectl api-resources
```
#### Documentation des ressources
```shell
# Exemple 
kubectl explain pod.spec.containers.command
```

### Information sur l'état des ressources
```shell
kubectl get pods 

kubectl describe 
```
### Proxy 
Ouvre une connexion entre la machine locale et l'API Server 
```
kubectl proxy 
```


## Troubleshooting
