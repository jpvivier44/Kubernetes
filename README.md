# Formation Kubernetes

## Installation plateforme de dev
- https://kubernetes.io/fr/docs/tasks/tools/install-kubectl/
- https://kubernetes.io/fr/docs/setup/learning-environment/minikube/

``` minikube start --driver=virtualbox```


## Test kubectl :
```kubectl version --client```

```kubectl get nodes```

```kubectl get nodes -o wide```

> describe (analyse, description, inscpection d'une ressource)
```kubectl describe node minikube```