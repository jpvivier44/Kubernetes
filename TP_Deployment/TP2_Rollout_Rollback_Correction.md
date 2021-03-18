# Exercice

Dans cet exercice, vous allez effectuer un scaling update ainsi qu'un rolling update sur un *deployment*

## 1. Scaling

Changez le nombre de replicas du deployment *frontend* de façon à en avoir 10.
>Note: pour cela vous pourrez avoir besoin de la commande $ kubectl scale .... 

>L'aide en ligne $ kubectl scale --help donne quelques exemples d'utilisation.

## 2. Mise à jour de l'image

Mettez l'image frontend à jour avec la version bilbloke/frontend:2.0

> Note : pour cela vous pourrez avoir besoin de la commande $ kubectl set image .... 

>Note: spécifiez l'option --record afin de conserver l'historique de la mise à jour


## 3. Historique des mises à jour

Listez les mises à jour (= révisions) du Deployment.
>Note: utilisez la commande kubectl rollout...

## 4. Effectuez un rollback

Faites un rollback et vérifier que le Deployment est maintenant basé sur la version précédente de l'image (bilbloke/frontend:1.0)


# Correction

Dans cet exercice, vous allez effectuer un scaling update ainsi qu'un rolling update sur un *deployment*

## 1. Scaling

Changez le nombre de replicas du deployment *frontend* de façon à en avoir 10.

>Note: pour cela vous pourrez avoir besoin de la commande $ kubectl scale .... 

>L'aide en ligne $ kubectl scale --help donne quelques exemples d'utilisation.

```
kubectl scale --replicas 10 deployment frontend
```

## 2. Mise à jour de l'image

Mettez l'image frontend à jour avec la version bilbloke/frontend:2.0

> Note : pour cela vous pourrez avoir besoin de la commande $ kubectl set image .... 

>Note: spécifiez l'option --record afin de conserver l'historique de la mise à jour

```
kubectl set image deployment frontend frontend=bilbloke/frontend:2.0 --record
```

## 3. Historique des mises à jour

Listez les mises à jour (= révisions) du Deployment.

>Note: utilisez la commande kubectl rollout...

```
kubectl rollout history deploy/frontend
```

## 7. Effectuez un rollback

Faites un rollback et vérifier que le Deployment est maintenant basé sur la version précédente de l'image

```
kubectl rollout undo deployment frontend
```
