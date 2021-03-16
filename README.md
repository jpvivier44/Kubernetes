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

> Suppression POD

```kubectl delete pod nginx```

> Création d'un Pod depuis un fichier de spec :

```kubectl apply -f pod_nginx.yml```

> Suppression d'un Pod :

```kubectl delete pod nginx```



## Approche imérative

https://kubernetes.io/docs/tasks/manage-kubernetes-objects/imperative-command/

> Sauvegarder la commande impérative dans un fichier de spec yaml

```kubectl run nginx --image nginx:1.18-alpine --dry-run=client -o yaml > pod_nginx_imperativ.yaml```

```kubectl create service clusterip my-svc --clusterip="None" -o yaml --dry-run=client > srv.yaml```



## K8s Dashboard
https://kubernetes.io/fr/docs/tasks/access-application-cluster/web-ui-dashboard/

> Dans un répertoire dashboard :

```wget https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended.yaml```

```kubectl apply -f recommended.yaml```

```kubectl get pod,svc,deploy -n kubernetes-dashboard```

```kubectl proxy```

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/.


## Purge des ressources

> Complète :
```kubectl delete all --all```

> Affinage sur namespace :
```kubectl delete all --all -n developpement```

> Affinage sur label :
```kubectl delete all --all -l app=dev```


## Secret

- Méthode de création via fichier de spec :

```
kubectl apply -f resource_secret.yaml
secret/demo-secret created
kubectl get secret
kubectl describe secrets demo-secret 
```

- Méthode de création impérative :
https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/

```
kubectl create secret generic imperative-secret --from-literal='username=my-app'
secret/imperative-secret created
```