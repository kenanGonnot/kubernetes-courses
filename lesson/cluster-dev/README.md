# Cluster de développement

## Différentes solutions
* Minikube
* Docker Desktop 
* Kind
* MicroK8s
* K3S


## Multipass
* permet de créer des machines virtuelles ubuntu très rapidement
* Hyperkit pour macos 
* Très utile pour la mise en place de cluster local

```
multipass launch -n node1
```
Pour install docker dans la VM node1 
```
multipass exec node1 -- /bin/bash -c "curl -sSL https://get.docker.com | sh"
```
Par défaut cette VM est configurée avec 1G de RAM, 1 cpu et 5 Go de disque mais différentes options peuvent être utilisées pour modifier ces valeurs. La commande suivante permet par exemple de créer une VM nommée node2 avec 2 cpu, 3 Go de RAM et 10 Go de disque:
```
multipass launch -n node2 -c 2 -m 3G -d 10G
```

Petit exemple: https://gitlab.com/lucj/k8s-exercices/-/blob/master/Installation/multipass.md
