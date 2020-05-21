lng: fr
hero: Capture des visiteurs
title: Capture des visiteurs
description:  comment utiliser la commande send pour l’envoi des événements à AFS Analytics

# Capture des visiteurs

La librairie analytics.js vous permet d’envoyer et d’échanger vos données sur les utilisateurs de votre site. 
Par exemple, lorsque un visiteur remplit un formulaire ou se connecte, 
vous pouvez transmettre des informations à AFS Analytics. 
Celles-ci seront attachées au profil du visiteur et apparaitront à chacune de ses visites.
 
L’envoi des données aux serveurs d’AFS s’effectue en deux étapes: 

1. Le stockage des données par analytics.js: Le stockage s’effectue grâce la commande ==set== suivit du mot clé *visitor*.
2. La transmission des données au serveur : La transmission au serveur s’effectue grâce à la commande ==send== suivit du mot clé *visitor*. 


!!! note
    Si vous avez installé l’extension WordPress d’AFS Analytics sur votre site, celle-ci transmettra automatiquement les données à AFS Analytics lors de la connexion des utilisateurs. Ces fonctions sont seulement disponibles avec l'abonnement aux plans Silver et Gold. 

## Le stockage des données
La commande ==set== permet de stocker les données grâce à un objet, ou une chaine indiquant la variable. 

Syntaxe: 
```js
aa("set","visitor",[object])

/* Ou */
aa("set","visitor.[variable]",[value])
```

Exemple: 
```js
aa("set","visitor",{firstname:"christophe";lastname:"Durand"};

/* Qui est équivalent à */

aa("set","visitor.firstname","Christophe");
aa("set","visitor.lastname","Durand");
```

### Variables disponibles

!!! note 
    Toutes les variables sont optionnelles. 

|Variable|Description
|---|---
|job| "create" pour la création du profil. "update" pour la mise à jour du profile. "delete" pour la suppression du profile. Par défaut, la valeur est définie à update,mode de mise à jour. Le mode création enregistre les données seulement si l'utilisateur est nouveau. Le mode « mise à jour » met à jour les données ou effectue la création du profil si il n’existe pas. Le mode « suppression » supprime le profil de l’utilisateur 
|logged| Le visiteur s’est authentifié (logged) sur le site.
|afsid| L’identifiant unique du visiteur créé par AFS Analytics. Par défaut, c’est l'ID du visiteur connecté.
|yourid| C’est votre propre identifiant unique.
|username| C’est le pseudo de l’utilisateur ou son identifiant utilisé pour la connexion.
|displayedname| Le nom à afficher sur la liste des visiteurs. Par défaut c’est l’username qui est affiché.
|role| La fonction ou le rôle de l’utilisateur. C’est une chaine de caractère. Exemple administrateur, membre, etc. A vous de le définir.
|firstname| Le prénom de l’utilisateur.
|listname| Le nom de famille.
|company| Le nom de la société.
|address| Numéro et nom de la rue.
|addressplus| Adresse ligne 2.
|city| La ville.
|state| La région ou l'état.
|country| Le pays.
|zipcode| Le code postal.
|email| Email
|phone| Le numéro de téléphone (fixe de préférence)
|sms| Le numéro de téléphone mobile qui peut recevoir des SMS
|birthday| La date de naissance sous la forme AAAA-MM-JJ.
|gender| M pour masculin, F pour féminin.
|photourl| Adresse URL de l'image représentant l’utilisateur (https).
|yournote| Vos remarques sur le visiteur.
|yoururl| Le lien pour l’identifiant que vous avez fourni "yourid".
|followlist| Liste(s) à attacher à l’utilisateur. Cela peut être l’identifiant numérique des listes, ou le nom des listes. S’il y a plusieurs listes, elles doivent être séparées par une virgule. Vous pouvez créer les listes, ou noter leur identifiant en cliquant sur  lorsque le profil d’un visiteur est affiché. 
|addtolist| Indique si followlist est un ajout aux listes déja existantes (valeur = "yes") ou doit remplacer les listes existantes (valeur = "no"). Valeur par défault: "no".



## Transmission des données au serveur

La transmission des données s’effectue avec la commande ==send==. Après la transmission des données analytics.js réinitialise les données. 

Syntaxe: 
```js
aa("send","visitor");
```

Exemple d'envoi des données: 
```js
data = { 
    job:"update",
    firstname:"Christophe",
    lastname:"Durand",
    username:"chris277",
    displayedname:"The Boss",
    birthday: "1989-12-31",
    photourl:"https://www.afsanalytics.com/images2/profile/demo.png",
    role:"Administrator",
    followlist:"Developer team, support"
    };

/* définit les variables du visiteur */
aa("set","visitor",data); 
aa("create", "xxxxxxxx", "auto"); 
aa("send", "pageview");
aa("send","visitor");
```

### Authentification des utilisateurs
Exception: quand un utilisateur se connecte, la commande Send visitor 
n’est pas obligatoire après la définition de la variable *logged* (visitor.logged), 
si celle-ci est définit avant la ligne envoyant les données de la page. 

Par exemple: 
```js
aa("create", "xxxxxxxx", "auto"); 
aa("set","visitor.logged",1); 

/* pas besoin d'ajouter send visitor */

aa("send","pageview");
```