lng: fr
hero: Interagir sur les traqueurs avec GET et SET
title: Interagir sur les traqueurs avec GET et SET
description: Interagir sur les traqueurs avec GET et SET


# Interagir sur les traqueurs avec GET et SET

La librairie analytics.js d’AFS vous permet d’interagir avec les traqueurs, c"est-à-dire d’obtenir ou de définir les données qui leurs sont assignées. Pour cela, il existe deux commandes:

- la commande ==get== est utilisée pour l’obtention des données.
- la commande ==set== pour définir ou changer des données. 

## La commande GET

Puisque les appels à la fonction ==aa== sont sauvegardés dans une file d’attente et que le téléchargement d’analytics.js se fait de façon asynchrone, il est nécessaire d’obtenir la confirmation de la création du traqueur avant de pouvoir accéder à ses données avec la commande get. 

Il existe deux possibilités pour réaliser cela: 

- La première consiste à définir une fonction de retour callback lors de la création du traqueur avec la commande create. (Voir le guide sur la fonction create pour plus de détails.) 

- La seconde est d’appeler la fonction ready callback après la création du traqueur. 

### La fonction "Ready Callback"

Ready Callback est une fonction que vous définissez en appelant la fonction aa(). Comme toutes les commandes de la liste d’attente sont exécutées dans l’ordre, cette fonction sera exécutée après la création du traqueur. Ready Callback envoie en retour l’objet tracker. 


!!! note
    La fonction Ready Callback peut être également appelée après l’envoie de la commande send, vous aurez alors accès aux données envoyés par les serveurs d’AFS, comme l’ID du visiteur. 

Le code suivant montre l’accès au traqueur par défaut grâce à Ready Callback. 
```js
aa("create", "XXXXXXXX", "auto");
/* ajout de la function ready callback */
aa(function(tracker) {
	/* Affiche les données du traqueur par défaut sur la console. */
	console.log(tracker);
});
```

### Accéder à un traqueur grâce à son nom

Si vous utilisez plusieurs traqueurs, vous pouvez accéder à un traqueur spécifique grâce a la commande ==getByName==. 

```js
getByName("nom") ;
```

La fonction ==getByName== renvoie l’objet tracker avec le *nom* spécifié. Si le champ nom est vide le traqueur par défaut sera renvoyé. 

```js
aa("create", "XXXXXXXX", "auto", "moncapteur");
aa(function() {
/* affiche les données du traqueur nommé "mon capteur" */
console.log(aa.getByName("moncapteur"));
});
```


### Obtenir la liste de tous les traqueurs

La fonction ==getAll== retourne dans un tableau la liste de tous les traqueurs (objets) créés. 
```js
aa("create", "XXXXXXXX", "auto");
aa("create", "YYYYYYYY", "auto", "moncapteur");
aa(function() {
	// affiche un tableau avec tous les traqueurs
	console.log(aa.getAll());
});
```

### Obtenir les données d’un traqueur grâce à la commande Get 

Les données des traqueurs peuvent être obtenues grâce à la commande get. 
```js
aa("create", "XXXXXXXX", "auto");
aa(function(tracker) {
  /* affiche le nom et le référant  du traqueur */
    console.log(tracker.get("name"));
    console.log(tracker.get("referrer"));   
});
```

En utilisant la fonction getByName 
```js
aa("create", "XXXXXXXX", "auto","moncapteur");
aa(function() {
    /* affiche les données du traqueur 'mon capteur' */
    var tracker=aa.getByName("moncapteur");
    console.log(tracker.get("name"));
    console.log(tracker.get("referrer"));   
});
```

## Mettre à jour les données stockées avec SET

Grâce à la commande SET les données des traqueurs peuvent être changées ou actualisées. La commande peut être couplée à un nom de traqueur ou envoyée seule. 

La transmission de la commande SET s’effectue via la fonction de file d’attente aa(). Les arguments peuvent être définis de deux façons distinctes : 
- Une paire de paramètres : le premier spécifie le champ à modifier, le second : la valeur de remplacement.
- Par un objet.

L’exemple suivant modifie le titre du traqueur par défaut : 
```js
aa("set","title","Home page") ;
```

Modifier l’URL et le titre du traqueur via un objet.:
```js
aa("set ",{
  title :"Home Page",
  location:"https://www.afsanalytics.com"
});
```

### Mettre à jour un traqueur grâce à son nom.

Vous pouvez définir une donnée d’un traqueur via son nom. 
```js
aa("moncapteur.set","title","About Us");
```

Utiliser la commande get directement sur l’objet tracker

```js
aa(function() {
  /* affiche les données du traqueur nommé "mon capteur" */
    var tracker=aa.getByName("moncapteur")
    tracker.set("title","About");
    console.log(tracker.get("name"));
    console.log(tracker.get("title"));  
})
```