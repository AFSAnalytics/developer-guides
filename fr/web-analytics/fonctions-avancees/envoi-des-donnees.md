lng: fr
hero: Interagir sur les traqueurs avec GET et SET
title: Interagir sur les traqueurs avec GET et SET
description: Interagir sur les traqueurs avec GET et SET

# Envoyer des données à AFS Analytics

Dans le code de suivi fourni par AFS analytics, vous pouvez remarquer après la création du traqueur, une ligne ajoutant la commande send à la fonction aa() . La commande "send" envoie au serveur d’AFS Analytics les données précédemment stockées par le traqueur (object tracker). 
Ce guide décrit comment les traqueurs communiquent avec AFS Analytics. 

## Les différents types d’appels ou de "hits"
Un *"hit"* se produit à chaque envoi de données d’analytics.js au serveur d’AFS Analytics: 
lorsqu’un traqueur envoie des données à AFS Analytics, il envoie un *"hit"*. 

Il existe plusieurs sortes de *hit* : 

| Type | Description
| --- | ---
| pageview | Envoi de données sur la page vue.
| event | Envoi de données sur un événement.
| ecommerce | Envoi de données sur une vente.
| visitor | Envoi de données liées à l’identification d’un visiteur.

Les "hits" sont envoyés via la commande send ou déclenchés automatiquement par l’option autotrack. 

## La commande SEND

La syntaxe de la commande send via la fonction aa() est la suivante : 

```js
aa("send", "hitType" ,[fieldslist] , [fieldsobject]) ;
```

Comme les champs dépendent du type de hit hitType envoyé, vous devez consulter son guide dédié pour connaitre la syntaxe précise à utiliser. 

!!! note 
    Dans la suite de ce document, nous allons prendre comme exemple l’envoi d’une page vue :pageview 

Dans l’exemple suivant nous utilisons un objet pour la transmission des données. 
```js
 aa("send", {
  hitType: "pageview",
  page: "titleindex",
  title: "home page",
  location: "https://www.afsanalytics.com"
 });
```

Les champs sont définis dans un objet passé en second argument de la fonction aa(). 

## Les différents types de champs

| Type | Action
| --- | ---
| hitType | Definition du type de hit.
| page ou index (optionnel) | Définition du mode d’indexation utilisé par AFS Analytics. Plusieurs sont disponibles comme autoindex, titleindex, pageindex, urlindex. Ce champ accepte deux appellations différentes *page* et *index*, le champ nommé *page* assure la compatibilité avec Google Analytics.
| title (optionnel) | défini le titre de la page. 
| location ou url(optionnel) | spécifie l’URL de la page. Ce champ accepte deux appellations différente. *location* assure la compatibilité avec Google Analytics. 

!!! important
    La version actuelle d’AFS ignore la valeur de ce champ et utilise toujours le titre des pages pour construire l’index. Dans une version ultérieure, cette option sera implémentée. 



Pour des raisons de simplification, les valeurs peuvent être transmises sans la spécification des champs. La position de l"argument détermine le champ. 

L’exemple précédent peut être écrit de la façon suivante : 
```js
aa(
    "send", 
    "pageview",
    "titleindex",
    "homepage","https://www.afsanalytics.com"
);
```


## Utiliser un traqueur spécifique.
Comme pour la commande set, il est possible de spécifier le nom du traqueur. 
```js
aa( 
    "montraqueur.send", 
    "pageview",
    "titleindex",
    "home page",
    "https://www.afsanalytics.com"
);
```

Ou en utilisant l’objet traqueur : 
```js
tracker.send("pageview","titleindex","home page","https://www.afsanalytics.com");
```

## Spécifier une fonction de retour (callback)

La fonction de retour (ou callback) sera appelée après l’exécution de la commande send. Elle renvoie trois paramètres : 

1. Une chaine contenant le type de hit: pageview,event,transaction , visitor, etc.. 
2. l’objet tracker pour le type pageview. 
3. l’objet défini contenant vos propre paramètres (champ params) 

La fonction *callback* est définie par le champ ==callback== ou ==hitCallback== 
(compatible avec Google Analytics). La valeur définie peut être 
une chaine de caractères contenant le nom de la fonction ou la fonction elle-même. 
Le champ ==hitCallback== se trouve à la cinquième position dans liste des arguments de la fonction aa() si le hitType est pageview. 

Le champs params est l’objet contenant vos propres paramètres. Dans l’appel simplifié, ce champ se positionne en sixième position si le type d’appel est pageview. 

Dans l’exemple suivant, nous créons notre propre objet et une fonction de retour. Nous appelons ensuite la commande send. La fonction mycallback sera exécutée une fois la transmission des données terminée. 

```js
/* définition d'un objet */
var monobjet={
    message:"la page vue a été envoyée a AFA Analytics",
    pagevue:document.title,
    location:window.location.href
};

/* définition d'une fonction de retour */
function mycallback(commande,tracker,objretour)
{
        console.log("Les informations du traqueur ont été envoyé a AFS Analytics!");
        console.log("La commande était ->",commande);
        console.log("La page était ->",objretour.pagevue,"l"url->",objretour.location);
        console.log ("L'unique ID  du visitor envoyé par AFS est->",tracker.get("visitor.id"));
        console.log ("Le traqueur est nommé ->",tracker.get("name"));
        console.log ("Le cookie du visiteur ->",tracker.get("cookie.str"));
        console.log(tracker);
}

/* appels à analytics.js */

aa("create", "00000003", "auto");
aa("send", "pageview","autoindex","Test Page","","mycallback",monobjet);
```

Sortie sur la console : 
```
Les informations du traqueur ont été envoyé a AFS Analytics!
La commande était -> pageview
La page était -> Test callback 
l"url-> http://127.0.0.1/tc.html
l"unique ID  du visitor envoyé par AFS est-> 31
Le traqueur est nommé -> afstracker0
Le cookie du visiteur -> 3x6226x1191x31x6103x1
```

La même commande envoyée sous forme d’objet: 
```js
aa("send", {
    hitType: "pageview", 
    page: "autoindex", 
    title: "Test Page", 
    hitCallback: "mycallback", 
    params: monobjet 
});
```

## Prévoir un timeout en cas d’erreur. 
Une fonction de retour est très utile pour exécuter des taches après l’envoi 
de données à AFS Analytics. Malheureusement, en cas de problèmes, 
la fonction risque de n’être jamais appelée. 

Pour cette raison, si des tâches importantes sont prévues dans cette fonction, prévoyez toujours une solution alternative.
La fonction setTimeout en JavaScript peut vous être utile dans la vérification de l’exécution de la fonction de retour. 
