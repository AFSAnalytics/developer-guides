lng: fr
hero: Comment fonctionne Analytics.js 
title: Comment fonctionne Analytics.js 
description: Tous les appels à la librairie Analytics.js se font exclusivement par la fonction globale aa( ). Ce document explique l’utilisation et le rôle de cette fonction.



# Comment fonctionne Analytics.js 

Tous les appels à la librairie Analytics.js se font exclusivement par la fonction globale ==aa( )==. Ce document explique l’utilisation et le rôle de cette fonction. 
!!! note
	Le nom de la fonction globale aa peut être changé dans le code de suivi, dans ce cas vous devez utiliser ce nouveau nom pour communiquer avec analytics.js. 

La librairie analytics.js d’AFS Analytics utilise la même structure que celle fournie par Google Analytics simplifiant son utilisation auprès des utilisateurs de Google Analytics. 

## La fonction de file d’attente aa()

La fonction globale ==aa()== définie dans le code de suivi ajoute dans une file d’attente tous les appels reçus à la librairie analytics.js précédent son téléchargement. Une fois analytics.js chargé, les commandes en attente sont exécutées et la liste vidée. Puis, la fonction aa() est remplacée par une nouvelle version disponible dans analytics.js. 

## Afficher la file d’attente avant le chargement d’analytics.js

Les appels sont sauvegardés dans le tableau q. Pour visualiser le contenu de la liste d’attente avant le chargement de la librairie, on affiche le tableau q: 

```sh
console.log(aa.q);
Sortie console: (q array):
[
   ['create', 'XXXXXXXX', 'auto'],
   ['send', 'pageview']
]
```

## Pourquoi utiliser une file d’attente?
La file d’attente permet l’utilisation de la fonction aa() sans se soucier de l’état du téléchargement de la librairie. D’autre part, elle assure un fonctionnement en mode asynchrone sans aucune perte de données. 

## Ajouter une commande à la fonction aa()

Tous les appels à la fonction aa() partagent la même structure composée de deux arguments minimum. Le premier est la commande à exécuter, les suivants définissent les arguments attachés à la commande. 

Dans l’appel: 
```js
aa('create', 'XXXXXXXX', 'auto');
```
*create* est la commande, *XXXXXXXX* et *auto* sont les arguments à appliquer à cette commande. 

Un nom de traqueur peut être défini lors de la création avec la commande create. Dans ce cas, si il existe plusieurs traqueurs, les commandes send et set devront être précédées du nom du traqueur (suivi d’un point) afin de s’adresser à celui-ci. Si aucun nom n’est défini, seul le premier traqueur, nommé ou pas, sera concerné par la commande. 

Exemple de création et d’adressage à un traqueur nommé:
```js
aa("create", "XXXXXXXX",auto,"mytraker") ;
aa("mytraker.send","pageview") ;
```
!!! note 
	Si la fonction aa() reçoit une commande inconnue, elle sera ignorée et aucune erreur sera générée.

## Les arguments attachés à la commande.

Les arguments liés à une commande peuvent être envoyés dans plusieurs formats afin de faciliter la transmission des champs les plus utilisés. 

## Appel Simplifié
Dans l’exemple suivant, les noms des champs n’apparaissent pas car ils sont déterminés en fonction de la position des arguments dans la fonction. 
```js
aa('create', 'XXXXXXXX', 'auto');
aa('send', 'pageview','titleindex’ , 'home page', 'https://www.mysite.com');
```	
La commande create accepte les champs trackingId, CookieDomain, et d’autres optionnels comme name, callback ou params. La commande send accepte divers paramètres selon le type d’envoi défini par hitType. Par exemple pour pageview , les champs page, title, location , hitCallback » et params peuvent être renseignés. AFS Analytics , accepte aussi les champs url, index, callback comme alternative aux champs location, page et hitCallback. 

## Appel avec un objet

Toutes les commandes peuvent accepter un objet (ou plusieurs) définissant les différents champs. Le code précédent pourrait être écrit de cette façon. 
```js
aa('create', {
	trackingID : 'XXXXXXXX' ,
	cookieDomain : 'auto'
}) ;
aa('send', {
	hitType: 'pageview’,
	page :'titleindex’ 
	title :'home page',
	location :'https://www.mysite.com'
});
```