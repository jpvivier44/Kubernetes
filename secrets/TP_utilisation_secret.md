## Exercice

Dans cet exercice vous allez créer un pod qui utilise une ressource de type *secret* afin de récupérer une valeur sensible et l'injecter dans son application

## 1. Création du secret encodé

> La doc K8s recommande d'encoder la valeur à enregistrer en tant que secret sur base 64 :
> https://kubernetes.io/fr/docs/concepts/configuration/secret/

- Encoder le mode de passe prévu :

```
$ echo -n "roottoor" | base64
cm9vdHRvb3I=
```

## 1. Création d'une ressource de type *Secret*

Créer un fichier de specification *mysql_secret.yaml* pour créer la ressource *secret* en intégrant le mot de passe encodé avec le contenu ci-dessous :

```
apiVersion: v1
kind: Secret
metadata:
  name: demo-secret
type: Opaque
data:
  db_root_password: cm9vdHRvb3I=
```

## 2. Création du secret

La commande suivante permet de créer le secret

```
$ kubectl apply -f mysql_secret.yaml
```

## 2. Spécification du pod utilisant une ressource *secret*

Créer un fichier *pod_mysql_secret.yaml* avec les spécifications suivantes :

- nom du Pod: *mariadb*
- label: app:tp_secret
- image du container: *mariadb:10.3*
- nom du container: *bdd*
- variable d'environnement utilisant une valeur *secretKeyRef* :
    ```
    env:
      - name: MYSQL_ROOT_PASSWORD
        valueFrom:
          secretKeyRef:
            name: demo-secret
            key: db_root_password
    ```

## 3. Création du pod

La commande suivante permet de créer le Pod

```
$ kubectl apply -f pod_mysql_secret.yaml
```

## 3. Status du Pod

La commande suivante permet d'obtenir le status du Pod

```
$ kubectl get pod
NAME      READY   STATUS    RESTARTS   AGE
mariadb   1/1     Running   0          3m45s
```

## 4. Test

Connectez-vous dans le conteneur *bdd* du pod *mariadb* pour vérifier la variable d'environnement *MYSQL_ROOT_PASSWORD* et la connexion à la base

```
$ kubectl exec -it mariadb -c bdd -- bash

root@mariadb:/# env | grep MYSQL
MYSQL_ROOT_PASSWORD=roottoor

root@mariadb:/# env | grep MYSQL
MYSQL_ROOT_PASSWORD=roottoor
root@mariadb:/# mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 10.3.28-MariaDB-1:10.3.28+maria~focal mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```


## 5. Suppression des ressources

Supprimer les ressources crées