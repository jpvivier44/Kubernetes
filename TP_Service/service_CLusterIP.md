## Exercice

Dans cet exercice, vous allez créer un Pod et l'exposer à l'intérieur du cluster en utilisant un Service de type *ClusterIP*.

### 1. Création d'un Pod

Créez un fichier *backend_php_pod.yaml* définissant un Pod ayant les propriétés suivantes:
- nom: *backend*
- label associé au Pod: *app: backend* (ce label est à spécifier dans les metadatas du Pod)
- nom du container: *backend*
- image du container: *bilbloke/backend:1.0*

### 2. Lancement du Pod

La commande suivante permet de créer le Pod

```
$ kubectl apply -f backend_php_pod.yaml
```

### 3. Définition d'un service de type ClusterIP

Créez un fichier *backend_service_clusterIP.yaml* définissant un service ayant les caractéristiques suivantes:
- nom: *backend*
- type: *ClusterIP*
- un selector permettant le groupement des Pods ayant le label *app: backend*.
- exposition du port *80* dans le cluster
- forward des requètes vers le port *80* des Pods sous-jacents

### 4. Lancement du Service

A l'aide de *kubectl* créez le Service défini dans *backend_service_clusterIP.yaml*

### 5. Accès au Service depuis le cluster

- Créer un fichier *client_pod.yaml* définissant le Pod dont la spécification est la suivante:

```
apiVersion: v1
kind: Pod
metadata:
  name: debug
spec:
  containers:
  - name: debug
    image: alpine:3.9
    command:
    - "sleep"
    - "10000"
```

Nous allons utiliser ce Pod pour accèder au Service *backend* depuis l'intérieur du cluster. Ce Pod contient un seul container, basé sur alpine et qui est lancé avec la commande `sleep 10000`. Ce container sera donc en attente pendant 10000 secondes. Nous pourrons alors lancer un shell intéractif à l'intérieur de celui-ci et tester la communication avec le Service *backend*.

- Lancez le Pod avec *kubectl*.

- Lancez un shell intéractif *sh* dans le container *debug* du Pod.

- Installer l'utilitaire *curl*

le container *debug* du Pod du même nom est basé sur l'image *alpine:3.9* qui ne contient pas l'utilitaire *curl* par défaut. Il faut donc l'installer avec la commande suivante:

```
/ # apk update && apk add curl
```

- Utilisez *curl* pour envoyer une requête HTTP Get sur le port *80* du service *backend*.
Vous devriez obtenir le contenu, sous forme textuel, de la page *index.php* servie par défaut par *backend*.

```
curl http://backend/index.php
```

Ceci montre que depuis le cluster, si l'on accède au Service *backend* la requête est bien envoyée à l'un des Pods (nous en avons créé un seul ici) regroupé par le Service (via la clé *selector*).

### 6. Visualisation de la ressource

A l'aide de `kubectl get`, visualisez la spécification du service *backend*.

### 7. Détails du service

A l'aide de *kubectl describe*, listez les détails du service *backend*

Notez l'existence d'une entrée dans *Endpoints*, celle-ci correspond à l'IP du Pod qui est utilisé par le Service.

Note: si plusieurs Pods avaient le label *app: backend*, il y aurait une entrée Endpoint pour chacun d'entre eux.

### 8. Cleanup

Supprimez l'ensemble des ressources créés dans cet exercice
