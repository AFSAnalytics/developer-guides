lng: fr
hero: Ajouter le code analytics.js à votre site
title: Ajouter le code analytics.js à votre site
description: All calls to the Analytics.js library are done exclusively via the aa() function. This document explains the use and role of this function. 



# Ajouter le code analytics.js à votre site
Analytics.js est une librairie JavaScript permettant de mesurer la fréquentation d'un site et d’analyser le comportement de ses visiteurs. 

AFS Analytics propose une librairie compatible avec celle de Google Analytics, c'est-à-dire qui reprend la même structure et les mêmes fonctions. Cette compatibilité facilite l’implémentation de notre solution de [web analytics](https://www.afsanalytics.com/fr/) pour les habitués de Google. A la fin de ce document, une section est consacrée aux différences entre le "tracking code" de Google et celui d’AFS Analytics. 

## Le code Javascript à ajouter à votre site.

Le code javascript, aussi appelé, code de suivi ou de capture , se compose de quelques lignes. Il peut être copié entre les balises &lt;head&gt; et &lt;/head&gt; (fortement recommandé) ou les balises &lt;body&gt; et &lt;/body&gt; des pages HTML de votre site internet.


```html
<head>
 <!-- Emplacement recommandé du script AFS Analytics.js-->
</head>

<body>
<!-- Position alternative -->
</body>
```


## Le code basique d’AFS Analytics


```js
<script>
(function(i,s,o,g,r,a,m){i["AfsAnalyticsObject"]=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,"script","//code.afsanalytics.com/js/analytics.js","aa");
aa("create", "XXXXXXXX", "auto");
aa("set","autotrack","dataset");
aa("send", "pageview");
</script>
```

!!! note
 	La chaine de caractères "XXXXXXXX" doit être remplacée par l’identification de votre site ID. Ce numéro unique composé de 8 chiffres a été créé lors de l’enregistrement de votre site internet sur AFS Analytics. Vous pouvez le trouver en choisissant l’option Gérer les sites dans le menu votre compte sur le tableau de bord. 



Le code précédent exécute les taches suivantes:

1. Chargement asynchrone de la librairie analytics.js. 
2. Initialisation de la librairie et définition du nom de la fonction principal : ici aa(). 
3. Création d’une fonction temporaire permettant de stocker dans une liste d’attente les appels à la fonction aa() intervenant avant le chargement de la librairie. 
4. Appelle la fonction « aa() » pour la création d’un nouveau traqueur (ou capteur). Remarque: la chaine XXXXXXXX doit être remplacée par l’ID de votre site. 
5. Ajout d’un second appel à la fonction aa() pour définir le mode de collecte automatisé des événements (variable:autotrack). 
6. Ajout d’un dernier appel à la fonction aa() pour envoyer les informations sur la page vue actuelle à AFS Analytics. 


L’exemple ci-dessus est une installation simplifiée d’AFS Analytics. La fonction aa() propose de nombreuses options et paramètres supplémentaires. 

!!! note 
	Le code HTML/Javascript précédant les appels aux fonctions d’analytics.js n’a pas besoin d’être changé. 

### Données capturées par le code basique 

- Le temps passé par le visiteur sur le site. 
- Le temps passé et le détail de chaque page visitée (page vue). 
- La date de sa dernière visite. 
- La localisation du visiteur. 
- La configuration utilisée. 
- Le site référent. 
- Les événements définis par les datasetsdans les balises. 

### (Optionel) Afficher le logo AFS sur votre site
La nouvelle version n’affiche plus le logo AFS sur votre site. Toutefois, si vous souhaitez l'afficher, vous pouvez indiquer son emplacement grâce a la balise suivante: 

```js
<div id='afsanalytics'></div> 
```

!!! note 
	Pour la version gratuite, cette balise est utile si votre trafic dépasse la limite fixée. 

## Les prochaines étapes

Pour des rapports d’activité basiques, le code précédent est suffisant. Pour continuer votre formation, la consultation des guides suivants est souhaitable : 

1. [Comment analytics.js fonctionne](../comment-analytics-js-fonctionne/). 
2. [Création d’un traqueur ou capteur](../../fonctions-avancees/creation-des-traqueurs/). 
3. [Comment configurer Analytic.js pour être en conformité avec la loi européenne sur la dépose des cookies](../rgpd/) 
4. [Obtenir et définir les données d’un capteur ou traqueur](../../fonctions-avancees/utilisation-des-traqueurs/). 
5. [Envoyer les données à AFS Analytics](../../fonctions-avancees/envoi-des-donnees/). 

## Différence entre le code de Google analytics et AFS analytics.

Il existe 3 différences entre les deux codes

- Le nom de la variable globale de l’objet (2eme ligne du code).

| AFS Analytics | Google Analytics 
| ------------- | ----------------
| AfsAnalyticsObject | GoogleAnalyticsObject.

- L’adresse du script analytic.js : (5eme ligne)

| AFS Analytics | Google Analytics 
| ------------- | ----------------
|  https://code.afsanalytics.com/js/analytics.js | https://www.google-analytics.com/analytics.js

- Le nom de la fonction d’appel. (5eme ligne)

!!! tip
	La définition du protocole https est optionnelle.

| AFS Analytics | Google Analytics 
| ------------- | ----------------
| aa | ga





## Remplacez Google Analytics par AFS Analytics en 30 secondes.

Si vous souhaitez remplacer Google Analytics par AFS analytics, vous avez simplement à changer une petite portion du code copié sur les pages de votre site en gardant le nom de la fonction d’appel. 

1. Remplacer GoogleAnalyticsObject par AfsAnalyticsObject 
2. Remplacer https://www.google-analytics.com/analytics.js par https://code.afsanalytics.com/js/analytics.js 
3. On garde ga comme nom de la fonction d’appel afin d’obtenir une compatibilité des appels a la fonction globale. 


Le code original de Google Analytics.
```js
<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');
ga('create', 'UA-XXXXX-Y', 'auto');
ga('send', 'pageview');
</script>
```

A remplacer par: 
```js
<script>
(function(i,s,o,g,r,a,m){i['AfsAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//code.afsanalytics.com/js/analytics.js','ga');
ga('create', 'XXXXXXXX', 'auto');
ga('send', 'pageview');
</script>
```
!!! note 
	N'oubliez pas de changer *XXXXXXXX* par l’identification (ID) de votre site. 

## Les appels à analytics.js lorsquer le nom de la fonction est ga

Tous les appels à la librairie analytics.js se font à l’aide de ga()  Vous pouvez ajouter l'option autotrack pour définir le mode de capture des événements : 

```js
<script>
ga('create', 'XXXXXXXX', 'auto');
ga('set','autotrack','dataset');
ga('send', 'pageview');	
</script>
```