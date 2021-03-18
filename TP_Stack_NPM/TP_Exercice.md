## Exercice manipulation des ressources K8s

Le but de ce TP est de décrire et manipuler un ensemble de ressources K8s fondamentales : 

- Pods
  - mono-container
  - multi-container (side-car)
- volumes
  - emtpyDir
  - hostPath
- services
  - CluterIP
  - nodePort
- configMap
- secret

## liens doc web

### volumes

> https://kubernetes.io/fr/docs/concepts/storage/volumes/

> https://kubernetes.io/fr/docs/concepts/storage/volumes/#hostpath

> https://kubernetes.io/fr/docs/concepts/storage/volumes/#emptydir

> https://kubernetes.io/docs/tasks/access-application-cluster/communicate-containers-same-pod-shared-volume/

### Configuration

> https://kubernetes.io/docs/concepts/configuration/configmap/

> https://kubernetes.io/fr/docs/concepts/configuration/secret/

### Workflow

> https://kubernetes.io/fr/docs/concepts/workloads/pods/pod/

### Network

> https://kubernetes.io/fr/docs/concepts/services-networking/service/

### Containers : init, side-car, satellite

> https://kubernetes.io/fr/docs/concepts/workloads/pods/init-containers/

> https://kubernetes.io/fr/docs/concepts/cluster-administration/logging/

### Commandes déploiement

- 1 : Mariadb

```
$ kubectl apply -f cm-mariadb.yaml

$ kubectl apply -f sct-mariadb.yaml

$ kubectl apply -f pod-mariadb.yaml

$ kubectl apply -f svc-mariadb.yaml

$ kubectl get pod,secret,svc,cm -l app=mariadb
```

- 2 : php
  
```
$ kubectl apply -f pod-php.yaml

$ kubectl apply -f svc-php.yaml

$ kubectl get pod,svc -l app=php
```

- 3 : nginx

```
$ kubectl apply -f cm-nginx.yaml

$ kubectl apply -f pod-nginx.yaml

$ kubectl apply -f svc-nginx.yaml

$ kubectl get pod,svc,cm -l app=php
```

- 4 : ALL

```
$ kubectl get all -l projet=npm
$ kubectl get po,secret,cm,svc -l projet=npm
```


- 5 : Debug

```
$ kubectl describe {ressource}
$ kubectl logs pod/nginx
$ kubectl exec pod/php -c php -- ls -l /srv/http
$ kubectl exec -it pod/nginx -- bash
```