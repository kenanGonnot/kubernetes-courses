# Exercise - service clusterip

https://gitlab.com/lucj/k8s-exercices/-/blob/master/Services/service_ClusterIP.md

```
kubectl apply -f www_pod.yml
```

```
kubectl apply -f www_service_clusterIP.yaml
```

```
kubectl apply -f debug_pod.yml
```

```
kubectl exec -ti debug -- sh
```

### cleanup 
```
kubectl delete po/www
kubectl delete svc/www
kubectl delete po/debug
```
