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

> Listin des resources k8s

```kubectl api-resources```

> Bash completion

```$ sudo apt install bash-completion```
```$ source <(kubectl completion bash)```