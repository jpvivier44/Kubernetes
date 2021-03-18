# Lancement dashbord :

https://kubernetes.io/fr/docs/tasks/access-application-cluster/web-ui-dashboard/

- 1 : Déploiement des ressourcs via le fichier de specs
  
```
kubectl apply -f Dashboard/recommended.yaml
```

- 2 : Création d'un utilisateur et son rôle 
  
> https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md

- 3 : mise à dispo du dashboard via proxy :

```
kubectl proxy
```