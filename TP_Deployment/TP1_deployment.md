## Exercice

Dans cet exercice, vous allez créer deux *Deployment*, un frontend exposé vers l'extérieur via un service *NodePort* et un backend exposé dans le cluster k8s via un service ClusterIP
Le frontend sera en mesure de communiquer avec le backend via le service de type ClusterIP

> https://kubernetes.io/fr/docs/concepts/workloads/controllers/deployment/

### 1. Spécification d'un Deployment frontend

Créez un fichier *frontend_deployment.yaml* définissant un Deployment ayant les propriétés suivantes:
- nom: *frontend*
- labels:
  - projet: tp_deploy
- nombre de replicas: 3
- définition d'un selector sur le label *app: frontend*
- spécification du Pod:
  * label *app: frontend*
  * un container nommé *frontend* basé sur l'image *bilbloke/frontend:1.0* et exposant le port *80*

### 2. Création du Deployment

Utilisez *kubectl apply* pour créer le Deployment

### 3. Status du Deployment

A l'aide de *kubectl*, examinez le status du Deployment *frontend*.

A partir de ces informations, que pouvez-vous dire par rapport au nombre de Pods gérés par ce Deployment ?

### 4. Status des Pods associés

A l'aide de *kubectl*, lister les Pods associés à ce Deployment.

### 5. Exposition des Pods du Deployment frontend

Créez un Service permettant d'exposer les Pods du Deployment à l'extérieur du cluster

Conseils:

- vous pourrez commencer par créer une spécification pour le Service, en spécifiant que le *selector* doit permettre de regrouper les Pods ayant le label *app: frontend*.

- utilisez un service de type *NodePort*, vous pourrez par exemple le publier sur le port *31111* des nodes du cluster

- le container basé sur l'image *frontend* tourne sur le port *80*, ce port devra donc être référencé en tant que *targetPort* dans la spécification du Service.

Note: n'hésitez pas à vous reporter à l'exercice sur les Services de type NodePort que nous avons vu précédemment

Une fois le service créé, vous pourrez accéder à l'interface de l'application *frontend* sur *http://IP_NODE:31111/index.php* ou IP est l'adresse IP d'une machine du cluster Kubernetes.

Note: vous pouvez récupérer les IPs des machines de votre cluster avec la commande `$ kubectl get nodes -o wide`


### 6. Spécification d'un deployment backend

A partir du TP_Service : POD backend *backend_php_pod.yaml*, convertir ce backend en specification deployment *backend_deployment.yaml*

- nom: *backend*
- labels:
  - projet: tp_deploy
- nombre de replicas: 2
- définition d'un selector sur le label *app: fronbackendtend*
- spécification du Pod:
  * label *app: backend*
  * un container nommé *backend* basé sur l'image *bilbloke/backend:1.0* et exposant le port *80*


### 7. Création du service backend

A partir du TP_Service : Service backend *backend_service_clusterIP.yaml*, créer la ressource de type service ClusterIP pour accèder au backend

## 8. Tester l'application via un navigateur web 

URL : http://ip_node:31111/index.php

> Si on actualise la page web, on constate que les *id" des conteneurs "attaqués* changent : le cluster nous oriente vers un des pods aléatoirement
