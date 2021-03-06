## Correction

### 1. Création du Pod

La spécification du Pod est la suivante:

```
apiVersion: v1
kind: Pod
metadata:
  name: www
  labels:
    app: www
spec:
  containers:
  - name: nginx
    image: nginx:1.18-alpine
```

### 2. Lancement du Pod

La commande suivante permet de créer le Pod:

```
$ kubectl apply -f www_pod.yaml
```

### 3. Définition d'un Service de type NodePort

La spécification du Service demandé est la suivante:

```
apiVersion: v1
kind: Service
metadata:
  name: www-np
  labels:
    app: www
spec:
  selector:
    app: www
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    nodePort: 31000
```

### 4. Lancement du Service

La commande suivante permet de lancer le Service:

```
$ kubectl apply -f www_service_NodePort.yaml
service/www-np created
```

### 6. Cleanup

Les ressources peuvent être supprimées avec les commandes suivantes:

```
$ kubectl delete po/www
$ kubectl delete svc/www-np
```
