# Kind 

Exercise: https://gitlab.com/lucj/k8s-exercices/-/blob/master/Installation/kind.md

issue: https://github.com/kubernetes-sigs/kind/issues/2448

## Before run
```
docker build -t tempkind . 
```

## Run 
```
kind create cluster --name k8s-2 --image tempkind --config config.yaml
```

## Cleanup 
```bash
$ kind delete cluster --name k8s

$ kind delete cluster --name k8s-2
```
