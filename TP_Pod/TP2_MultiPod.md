# Création d'un Pod multi conteneurs

## Exercice

Dans cet exercice, vous allez créer une spécification pour lancer un  Pod avec deux conteneurs.

### 1. Création de la spécification

Créez un fichier yaml *multipod.yaml* définissant un Pod ayant les propriétés suivantes:
- nom du Pod: *mulitpod*
- image du container nginx: *nginx:1.18-alpine*
- nom du container: *nginx*
  
- image du container debian : *debian:buster-slim*
- nom du container: *debian*
- command: ["sleep", "600"]

### 2. Lancement du Pod

Lancez le Pod à l'aide de *kubectl*

### 3. Vérification

Listez les Pods lancés et assurez vous que le Pod *multipod* apparait bien dans cette liste.

### 4. Details du Pod

Observez les détails du Pod à l'aide de *kubectl* et retrouvez l'information de l'image utilisée par le container *multipod*.

### 5. Se connecter dans le conteneur debian du pod multipod 

Avec la commande *kubectl exec -it * se connecter dans le conteneur debian
Tester une requete curl vers le service pod_ngin ```curl http://localhost:80```

### 6. Suppression du Pod

Supprimez le Pod.


## Correction

### 1. Création de la spécification

La spécification, définie dans le fichier *whoami.yaml*, est la suivante:

```
apiVersion: v1             
kind: Pod                  
metadata:
  name: whoami
spec:
  containers:
  - name: whoami
    image: containous/whoami
```

### 2. Lancement du Pod

Le Pod peut être créé avec la commande suivante:

```
$ kubectl apply -f whoami.yaml
```

### 3. Vérification

La commande suivante permet de lister les Pods présent:

```
$ kubectl get pods
NAME      READY     STATUS    RESTARTS   AGE
whoami    1/1       Running   0          14s
```

Note: il est aussi possible de précisez *pod* (au singulier) ou simplement *po*

```
$ kubectl get pod
NAME      READY     STATUS    RESTARTS   AGE
whoami    1/1       Running   0          16s

$ kubectl get po
NAME      READY     STATUS    RESTARTS   AGE
whoami    1/1       Running   0          22s
```

### 4. Details du Pod

Les details d'un Pod peuvent être obtenus avec la commande suivante:

```
$ kubectl describe pod whoami
```

### 5. Accès à l'application via un port-forward

Depuis un premier terminal lancez la commande suivante:

```
$ kubectl port-forward whoami 8888:80
```

Depuis un second terminal, vérifiez que l'application est accessible sur localhost depuis le port 8888:

```
$ curl localhost:8888
Hostname: whoami
IP: 127.0.0.1
IP: 10.244.1.4
RemoteAddr: 127.0.0.1:51562
GET / HTTP/1.1
Host: localhost:8888
User-Agent: curl/7.64.1
Accept: */*
```


### 6. Suppression du Pod

Le Pod peut etre supprimé avec la commande suivante:

```
$ kubectl delete po/whoami
```

ou

```
kubectl delete -f TP1_Pod/whoami.yaml
```
