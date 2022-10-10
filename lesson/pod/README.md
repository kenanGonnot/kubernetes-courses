# Pod 
* Groupe de containers tournant dans un même context d'isolation
    * Linux namespaces: network, IPC, UTS
* Partagent la stack réseau et le stockage (volumes)
* Adresse IP dédiée, pas de NAT pour la communication entre les Pods 

![module_03_pods](assets/module_03_pods.svg)
![module_03_nodes](assets/module_03_nodes.svg)

* Application découpée en plusieurs spécifications de Pods 
* Chaque spécification correspond à un service métier (microservice)
* Scaling horizontal via le nombre de replica d'un Pod 
    * création de nouveaux Pod basé sur la même spécification


## Exemple de spécification
### server http
fichier yaml (format json)
```
apiVersion: v1
kind: Pod 
metadata:
    name: nginx
spec:
    containers: 
    - name: www
    image: nginx:1.12.1    
```

## Cycle de vie
* Lancement d'un Pod 
    ```
    kubectl create -f POD_SPECIFICATION.yaml
    ```
* Liste des Pods 
    ```
    kubectl get pod 
    ```
* Description d'un Pod 
    ```
    kubectl describe pod POD_NAME
    kubectl describe po/POD_NAME
    ```
* Logs d'un container
    ```
    kubectl logs POD_NAME [-c container_name]
    ```
* Lancement d'une commande dans un Pod existant 
    ```
    kubectl exec POD_NAME [-c container_name] --COMMAND 
    ```
* port-forward 
    ```
    kubectl port-forward NAME_POD 8080:80
    ```
* Suppression d'un POD 
    ```
    kubectl delete pod POD_NAME
    ```

Mini exercice: https://gitlab.com/lucj/k8s-exercices/-/blob/master/Pod/pod_whoami.md


## Rôle
* kube-scheduler
* nodeSelector -> permet de scheduler un pod sur un node specifique
    * dans le fichier *.yml, ajout d'une contrainte dans la spécification du Pod 
        * "nodeSelector: 
                disktype: ssd"   
* nodeAffinity
    * permet de scheduler des pods sur certains nodes seulement 
    * plus granulaire que nodeSelector
    * autorise les opérateurs In, NotIn, Exists, DoesNotExist, Gt, Lt 
    * se base sur les labels existant sur les nodes 
    * Différentes règles, dans le fichier *.yaml, dans la balise nodeAffinity: 
        * requiredDuringSchedulingIgnoredDuringExecution (contrainte "hard")
        * preferredDuringSchedulingIgnoredDuringExecution (contrainte "soft")
    * Utilise le champ **topologyKey** pour la spécification de domaines topologiques 
        * hostname
        * region
        * az
        * ...
Exemple: 
```
apiVersion: v1
kind: Pod
metadata:
  name: with-node-affinity
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: topology.kubernetes.io/zone
            operator: In
            values:
            - antarctica-east1
            - antarctica-west1
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
          - key: another-node-label-key
            operator: In
            values:
            - another-node-label-value
  containers:
  - name: with-node-affinity
    image: registry.k8s.io/pause:2.0
```

* PodAffinity / podAntiAffinity
* Taints / Tolerations 
* Allocation des ressources
Important de limiter les ressources des pods (ram, cpu...)
dans le fichier *.yml
```
    ressources:
        requests:
            memory: ...
```

Exemple : https://gitlab.com/lucj/k8s-exercices/-/blob/master/Pod/pod_scheduling.md

***
### Approche impérative 

permet de créer un conteneur 
```
docker run ...
```
permet de creer un pod 
```
kubectl run db --image mongo:4.0
```

#### Option: dry-run 

simule la création d'une ressource
```
kubectl run db --image monga:4.0 -- dry-run=client -o yaml
```
"client" ne vas pas jusqu'a l'api server, mais reste chez le client.
Permet de simuler une màj.


# Résumé 
* Application composée de plusieurs Pods qui communiquent entre eux
* Pod contient souvent un seul container applicatif 
    * en plus du container pause
* Instrumentation d'une application en ajoutant des containers de services 
    * monitoring 
    * logs
    * service mesh
* Pods généralement créés via un **ReplicaSet** dans un **Deployment** 
* Exposition dans le cluster ou vers l'extérieur via un **Service**