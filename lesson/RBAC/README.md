# (Revenir plus tard)
# Utilisateurs et droits d'accès - RBAC 
* Authentification -> Autorisation -> service

## Authentification 
* Deux types de requetes: 
     * Human 
         * Certificat client 
             * --client-ca-file=FILE au démarrage de l'API Server
         * Bearer tokens 
             * --tokens-auth-file=FILE au démarrage
         * HTTP basic auth
             * --basic-auth-file=FILE
     * Pod 
         * Utilisation d'un ServiceAccount
             * donne des droits aux containers tournant dans un Pod 
             * JWT token disponible via un Secret


### Certificat client (x509)
```yaml
apiVersion:
kind: CertificateSigningRequest
...
```
```bash
$ kubectl certificate approve 
```    

### ServiceAccount
```
kubectl get sa/default -o yaml
```
```yaml
apiVersion:
kind: ServiceAccount
metadata:
    name:
```
```
kubectl get secret defaukt-token-..
```

## Autorisation

mini exercice: https://gitlab.com/lucj/k8s-exercices/-/blob/master/RBAC/ServiceAccount.md

https://gitlab.com/lucj/k8s-exercices/-/blob/master/RBAC/certificat-x509.md