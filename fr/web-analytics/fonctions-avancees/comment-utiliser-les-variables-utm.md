lng: fr
hero: Comment utiliser les variables UTM
title: Comment utiliser les variables UTM
description: Comment définir les paramètres UTM dans les liens pour mesurer l’efficacité de vos campagnes. 

# Utilisation des variables UTM

AFS Analytics détecte et collecte les paramètres UTM pour analyser les performances de vos campagnes marketing. Ce guide va vous apprendre à définir les paramètres UTM dans les liens et à vous en servir pour mesurer l’efficacité de vos campagnes. 

## Définition des paramètres UTM

Les paramètres UTM permettent d’identifier le trafic entrant d’un site provenant d’une source spécifique. 

Les paramètres UTM sont des variables que l’on ajoute à un lien afin d’identifier sa provenance. Ils sont généralement inclus dans la query string de l’URL ou, après l’encre # de celle-ci. L’abréviation "UTM" signifie "URCHIN Tracking module". C’est la société "Urchin Software Corporation" qui a est à l’origine de ce système. 

## Utilité des variables UTM

On utilise ce procédé pour mesurer l’impact et les performances d’une publicité, d’une newsletter, d’un courriel, ou tout simplement d’un lien sur un site référant. 

Exemple de lien avec des variables UTM
Ce lien est utilisé pour mesurer la performance d’une campagne Google Adword . 

```html
https://www.afsanalytics.com?utm_source=google&utm_medium=cpc&utm_campaign=AFS%20Analytics%20January%202017&utm_term=Web%20Analytics&utm_content=text01&utm_calc=cpc&utm_cost=0.20
```

Vous remarquez dans le lien plusieurs paramètres commençant par le préfix ==utm_== , ce sont les paramètres UTM. 

!!! note 
    AFS Analytics à ajouté deux paramètres à cette norme. Les variables *utm_calc* et *utm_cost*. Ce sont des paramètres optionnels utilisés pour calculer le coût total d’une campagne marketing. 

## Générateur de lien UTM

AFS fournit un outil de création qui ajoute les paramètres UTM à un lien. 
Il est disponible ici : [Générateur de lien marketing UTM](https://www.afsanalytics.com/generateur-de-lien-marketing-utm.php)

## Les variables UTM

Dans cette partie nous expliquons le rôle joué par chaque variable UTM. 

### *utm_source:
La variable utm_source indique d’où vient le trafic. C'est-à-dire le référent. Dans note example le référant est "google". 

### *utm_medium:
Indique le moyen utilisé pour obtenir le trafic. C’est à dire le support marketing utilisé. Dans notre exemple nous précisons qu’il s’agit d’un clic (cpc), nous aurions pu avoir comme valeur : bannière, email, lettre d’information, réseau social, etc.… 

### *utm_campaign:
Cette variable indique le nom donné à la campagne publicitaire. 

### utm_content (optionnel)
Cette variable indique le conteneur de la campagne. Cela peut être image, une taille de bannière. En gros ce que vous voulez. 

### utm_term (optionnel)
Permet de définir les mots clés payant utilisés pour une campagne sur moteur de recherche. Dans notre exemple : "web analytics" 

### utm_calc (optionnel)
Cette variable précise le mode de calcul du coût de la campagne. 

Les valeurs acceptées sont:

|Valeur|Description
|---|---
|cpc| Cout par clic.
|cpm| Le coût pour mille impression. 
|cps| Coût par vente. Il s’agit d’une commission fixe par vente.
|cpspercent| Coût par vente. Mais il s’agit d’un pourcentage sur la vente.
|total| C’est le coût total de la campagne. 

!!! important
    l’option *cpm* dans utm_calc, est actuellement ignorée puisqu'il  n'est pas possible de connaître pas le nombre exact d’impressions de la publicité. Utilisez plutôt l’option *total* en précisant le coût total de la campagne publicitaire avec *utm_cost*. 



### utm_cost (optionnel)

Ce paramètre doit être défini si utm_calc est défini. C’est la valeur liée à la variable. 

| Valeur utm_calc |  Significationde de la valeur utm_cost
|---|---
|cpc | coût unitaire du clic. 
|cpm | coût par mille impressions. 
|cps | coût unitaire par vente. 
|cpspercent |pourcentage sur la vente. 
