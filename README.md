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

> Listing des resources k8s

```kubectl api-resources```

> Explication des resources :

```kubectl explain pods```

> Bash completion

```$ sudo apt install bash-completion```
```$ source <(kubectl completion bash)```


> Interrogation des composants système K8S via le namespace kube-system

```kubectl get pods --namespace kube-system```

> Test création Pods :

```kubectl run nginx --image nginx:1.18-alpine```