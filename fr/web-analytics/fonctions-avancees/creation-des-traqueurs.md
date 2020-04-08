lng: fr
hero: Création de traqueurs
title: Création de traqueurs
description: Comment configurer analytic.js pour être en conformité avec la loi européenne sur la dépose des cookies.

# Création de traqueurs

Un traqueur (tracker) ou capteur est un objet chargé de collecter les données des visiteurs puis de les envoyer à AFS Analytics. 
Lors de la création du traqueur, l’identification (ID) du site et le mode de stockage des cookies doivent être spécifiés. 

## Récupérer l’ID d’un site

L’ID d’un site se compose de 8 chiffres. Elle est créée lors de l’ajout d’un site à un compte d’AFS Analytics. Pour trouver l’ID d’un site, sélectionner l’option "gérer les sites" dans le menu votre compte disponible sur le tableau de bord d’AFS Analytics. 

## Mode de stockage des cookies

AFS Analytics propose plusieurs modes de stockage des cookies. 

- Le mode *auto* (valeur recommandée) crée un cookie attaché au domaine et à tous les sous domaines du site internet.
- Le mode *afs* crée un cookie attaché au domaine afsanalytics.com. Appelé cookie tiers , ce type de cookies est seulement recommandé pour les sites ne possédant pas leur propre nom de domaine. Les cookies tiers sont peu fiables car certains navigateurs les désactivent pour préserver la vie privée des utilisateurs.
- Le mode *nocookie* n"écrit pas de cookies sur le terminal de l"utilisateur. Seul des cookies de sessions sont utilisés.
- Le dernier mode permet de spécifier le nom de domaine attaché aux cookies.

 [configurer Analytic.js pour être en conformité avec la loi européenne sur la dépose des cookies]()

## Le fonctionnement des cookies

Pour chaque nouveau visiteur, AFS génère une ID unique et la sauvegarde dans un cookie. Ce procédé permet l’identification du visiteur à chaque nouvelle visite. 

## Création de traqueurs avec la commande "create"
L’utilisation de commande « create » permet de créer un nouveau traqueur. Elle est suivie de deux paramètres obligatoires : le premier l’identification du site trackingID , le second : le nom du domaine attaché au cookie cookieDomain. Cet argument accepte aussi les valeurs prédéfinies auto ou afs 
```js
aa("create", "XXXXXXXX", "auto");
```
!!! note 
	Lors de la création d’un traqueur, de nombreuses données sont collectées comme le titre et l’URL de la page, le site référant et la configuration utilisée par le visiteur. 

## Les paramètres optionnels

### Nommer un traqueur

Vous pouvez nommer un traqueur en ajoutant le paramètre name en quatrième position. 
```js
aa("create", "XXXXXXXX", "auto","mytracker");
```

Si le champ name n’est pas spécifié, le traqueur sera nommé automatiquement afstracker0. Le second créé sera nommé afstracker1 et ainsi de suite. 

### Définir une fonction de retour (callback) 

En cinquième position vous pouvez définir le nom d’une fonction de retour callback. Elle sera exécutée après création du traqueur. 

En sixième position le paramètre params accepte un objet qui sera transmis à votre fonction de retour. 
Exemple de code exécutant une fonction de retour renvoyant un objet défini : 
```js
function createcallback(command,t,myobject)
{
        console.log("traqueur créé");
        console.log("Commande de callback ->",command);
        console.log ("Accès à l"objet tracker: Nom du tracker ->",t.name);
        console.log ("Retour de l"objet "params" transmis pas la fonction aa() ->",myobject);
}

aa("create", "00000003", "auto","mytracker","createcallback",{string:"mes parametres"});
```
Sortie sur la console : 
```sh
Traqueur créé
Type de callback -> 
Accès à l"objet tracker: Nom du tracker -> mytracker
Retour de l"objet "params" transmis pas la fonction aa() -> 
Object {string: "mes paramètres"}
```

La fonction callback retourne 3 paramètres: 

1. Une chaine de caractères avec la commande ou le hitType de la fonction appelante. 
2. L’objet tracker vous donne accès à toutes les données stockées par le traqueur.
3. Le retour de l’objet défini avec le paramètre params dans la fonction aa()

### Transmettre les arguments via un objet

La transmission des paramètres de la commande create peut se faire aussi via un objet lors de l’appel à la fonction aa(). 

```js
aa("create", {
  trackingId: "00000003",
  cookieDomain: "auto",
  name: "myTracker1",
  callback : "createcallback",
  params : {string:"mes parametres"}
});
```

### Créer et travailler avec plusieurs traqueurs

Il est possible de créer et de travailler avec plusieurs traqueurs sur la même page. Cela peut être utile lorsque le site appartient à plusieurs propriétaires, et que chacun d’eux souhaite obtenir des rapports sur des sections différentes du site. 
Pour obtenir deux rapports distincts, vous devez déjà être en possession de deux ID différentes et créer des traqueurs avec des noms différents. 
```js
aa("create", "XXXXXXXX", "auto");
aa("create", "YYYYYYYY", "auto", "clientTracker");
```

### Envoyer des informations à un traqueur spécifique

Pour envoyer des informations à un traqueur spécifique, son nom suivi d’un point doit être ajouté devant la commande à exécuter. Rappelez-vous le traqueur par défaut à pour nom afstracker0 . 
Exemple d’envoi de page vue aux deux traqueurs définis ci-dessus :
```js
aa("afstracker0.send", "pageview");
aa("clientTracker.send", "pageview");
```
!!! note 
	aa("send", "pageview"); est équivalent à aa("afstracker0.send", "pageview"); 