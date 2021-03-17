# liens doc web

## volumes

> https://kubernetes.io/fr/docs/concepts/storage/volumes/

> https://kubernetes.io/fr/docs/concepts/storage/volumes/#hostpath

> https://kubernetes.io/fr/docs/concepts/storage/volumes/#emptydir

> https://kubernetes.io/docs/tasks/access-application-cluster/communicate-containers-same-pod-shared-volume/

## Configuration

> https://kubernetes.io/docs/concepts/configuration/configmap/

> https://kubernetes.io/fr/docs/concepts/configuration/secret/

## Workflow

> https://kubernetes.io/fr/docs/concepts/workloads/pods/pod/

## Network

> https://kubernetes.io/fr/docs/concepts/services-networking/service/

## Containers : init, side-car, satellite

> https://kubernetes.io/fr/docs/concepts/workloads/pods/init-containers/

> https://kubernetes.io/fr/docs/concepts/cluster-administration/logging/

## Commandes déploiement

- 1. Mariadb

```
$ kubectl apply -f cm-mariadb.yaml

$ kubectl apply -f sct-mariadb.yaml

$ kubectl apply -f pod-mariadb.yaml

$ kubectl apply -f svc-mariadb.yaml

$ kubectl get pod,secret,svc,cm -l app=mariadb
```

- 2. php
  
```