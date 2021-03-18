# Exercice

Dans cet exercice, vous allez effectuer un scaling update ainsi qu'un rolling update sur un *deployment*

## 2. Scaling

Changez le nombre de replicas du deployment *frontend* de façon à en avoir 10.
>Note: pour cela vous pourrez avoir besoin de la commande $ kubectl scale .... 

>L'aide en ligne $ kubectl scale --help donne quelques exemples d'utilisation.

## 3. Mise à jour de l'image
Mettez l'image nginx à jour avec le version nginx:1.16-alpine

>Note: spécifiez l'option --record afin de conserver l'historique de la mise à jour

## 5. Liste des ressources
Une nouvelle fois, listez les ressources.Que constatez vous ?

## 6. Historique des mises à jour
Listez les mises à jour (= révisions) du Deployment.
>Note: utilisez la commande kubectl rollout...

## 7. Effectuez un rollback
Faites un rollback et vérifier que le Deployment est maintenant basé sur la version précédente de l'image (nginx:1.16)

##8. Cleanup
Supprimez le Deployment www