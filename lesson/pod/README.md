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
* Suppression d'un POD 
    ```
    kubectl delete pod POD_NAME
    ```
    
    
    