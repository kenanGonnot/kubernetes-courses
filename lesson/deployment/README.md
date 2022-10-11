# Deployment 

## Exemple de deployment .yml
```
apiVersion: apps/v1
kind: Deployment
metadata:
    name:www
spec:
    replicas:5
    selector:
        matchLabels:
            app: www
    template:
        metadata:
            labels:
                app: www
        spec:
            containers:
            - name: www
              image: nginx:1.1    
```
deploy.yml
```
kubectl apply -f deploy.yml
```
```
kubectl get deplor,rs,pod
```

## Approche impérative 

```
kubectl create deploy vote --image instavote/vote
```
* PLusieurs limitations => il n'est pas possible de:
    * spécifier le nombre de réplicas (1 par défaut)
    * spécifier plusieurs containers 
    * ... 
* Pratique mais beaucoup moins flexible qu'une specification yaml

# <!> Generation de la spécification d'un deployment <!>
```
kubectl create deploy vote --image instavote/vote --dry-run=client -o yaml
```

## Mis à jour d'un deployment 

* Canary 
    * 75% v1 et 25% v2 
    * petit à petit vers la V2
* Rolling update 
    * dispo dans kubernetes
* Blue Green
* Recreate 
    * Pas conseillé, car un moment il n'y aura pas de service pendant un moment 

### Rolling update 
* Màj graduelle de l'ensemble des Pods 
* Params pour controler la màj
    * maxUnavailable
    * maxSurge 

#### Màj avec l'apporche impérative 
```
kubectl set image deploy/vote vote=instavote/vote:movies --record
```


#### Historique des màj 
```
kubectl rollout history deploy/vote
```

#### Rollback 
```shell 
kubectl rollout undo deploy/vote

kubectl rollout undo deploy/vote --to-revision=X
```

#### Forcer la mise à jour 
```shell
kubectl rollout restart deploy/www
```

Petit exercice sur les maj: https://gitlab.com/lucj/k8s-exercices/-/blob/master/Deployment/rollout_rollback.md


## Mise à l'echelle 
#### Scalling horizontal
```shell
#Creation d'un deployment 
$ kubectl create deploy www --image=nginx:1.16

#Augmentation du nombre de réplicas 
$ kubectl scale deploy/www --replicas=5
```

#### HorinzontalPodAutoscaler
Exemple de spécification: 
```
apiVersion: 
kind: HorizontalPodAutoscaler 
...

```
approche applicative
```
kubectl autoscale deploy www --min=2 --max=10 --cpu-percent=50
```

```
kubectl get hpa -w
```

Mini exercice: https://gitlab.com/lucj/k8s-exercices/-/blob/master/Deployment/HorizontalPodAutoscaler.md

# Namespace
```shell
# Creation du namespaces developement
$ kubectl create namespace development
```

Mini exercice: https://gitlab.com/lucj/k8s-exercices/-/blob/master/Namespace/namespace.md

https://gitlab.com/lucj/k8s-exercices/-/blob/master/Namespace/ResourceQuota.md

https://gitlab.com/lucj/k8s-exercices/-/blob/master/Namespace/LimitRange.md