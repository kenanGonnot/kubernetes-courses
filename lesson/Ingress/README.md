# Ingress 
Différentss façon d'exposer une application au monde extérieur.

* Ensemble de règles pour la connection aux services du cluster depuis internet 
* Nécessite qu'un Ingress Controller soit déployé 
    * container Docker avec un processus de controle 
    * load balancer managé par kubernetes
    * exemple: GCE, nginx, Traefik, HAProxy
* Différents cas d'usage
    * routage HTTP, ex:hôtes virtuels basés sur le nom 
    * terminaison TLS
    * Load balancing
* Add-ons pour Minikube: "$ minikube addons enable ingress"

Mais il y a d'autres options: 
* Service de type NodePort
    * statique 
    * load balancer externe pour le dispatch entre plusieurs nodes
* Service de type Load Balancer 
    * nécessite l'utilisation d'un cloud provider (AWS, GCE, Azure ...) 



Exemple de spécification:
```yaml
apiVersion: extensions/v1beta1
kind: Ingress 
metadata:
    name:
spec:
    rules:
        - host: www.exemple.com
          http:
            paths:
                - backend:
                    serviceName:www
                    servicePort:80
```

        
