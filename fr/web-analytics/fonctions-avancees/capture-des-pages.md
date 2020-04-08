lng: fr
hero: Capture des pages
title: Capture des pages
description:  comment utiliser la librairie analytics.js pour capturer et envoyer ces données à AFS Analytics

# Capture des pages

La capture des pages permet de mesurer le nombre de vues et le temps consacré par vos visiteurs à chacune d"elles. 
Ce guide explique comment utiliser la librairie analytics.js pour capturer et envoyer ces données à AFS Analytics,
solution de [web analytics](https://www.afsanalytics.com/fr/).
 
## La commande "Send" pour la capture des pages

Lors de la création du traqueur, plusieurs champs sont définis par les données fournies dans le document. 
Par exemple, le champ title est indiqué dans la balise ==&lt;title&gt;== et l'URL correspond à l'adresse de la page. 

Une fois les données collectées, elles sont modifiable grâce à la commande set, 
et certaines d'entre elles peuvent être remplacées directement dans la commande d'envoi. 

L'envoi des données se fait avec la commande send en utilisant la syntaxe suivante: 
```js
aa("send","pageview",[page],[title],[location] ,[hitCallback],[params]) 
```

Seul le champ ==hitType== est obligatoire. Il doit indiquer pageview comme type d"appel. 

### Champs optionnels 

| Champ | Description
| --- | ---
| page| indique lindex utilisé par AFS Analytics pour trier les pages. Vous pouvez utiliser votre propre méthode d'indexation ou utiliser une méthode prédéfinie comme autoindex, titleindex, urlindex, pageindex. 
| title |  Ce champ spécifie le nom ou le titre de la page.
| location | Ce champ indique l'adresse URL de la page.
| hitCallback | Ce champ définit la fonction de retour callback. Cette fonction sera appelée après l'envoi de la page au serveur d'AFS Analytics. La valeur peut être une fonction, ou une chaine avec le nom de la fonction.
| params | C'est un objet contenant vos propres variables récupérables dans la fonction de retour. 

!!! tip
    Si un champ comporte une chaine vide, la valeur par défaut ou stockée précédemment sera utilisée.


Exemples d"utilisation: 
```js
/* Utilisation sans aucun paramètre */

aa("send","pageview");
```

Utilisation en définissant le titre de la page:
```js
/* Notez la chaine vide pour le champ page */

 aa("send","pageview","","mon titre"); 
```

Utilisation en définissant une fonction de retour:

```js
/* Notez les chaines vides pour les arguments page et url */

aa('send','pageview','','montitre','', 'mafonctionderetour'); 
```


Les champs peuvent être aussi spécifiés dans un objet. 
Vous êtes libres de choisir les champs à renseigner. Seul le champ hitType est obligatoire. 

Définir les champs sous forme d"objet :
```js
aa("send",{
    hitType :"pageview",
    page : "titleindex",
    title : "mapage",
    location : "https://monsite.com",
    hitCallback : "mafonctionderetour",
}) ;
```

## Simplification de l'adresse de la page

Si l'URL de la page contient dans la query string ou dans la partie ancrage des paramètres de campagnes publicitaires,
 AFS les détachera et les traitera avec l'envoi de la page. 

Analytics.js offre également un paramètre ==allowAnchor==, qui permet de sauvegarder 
ou d'ignorer la query string et la partie d'ancrage de l'URL lors de sa transmission.
Cette commande à placer après la création du traqueur demande à AFS d'ignorer les additifs à l'URL. 

```js
aa(set, "allowAnchor", false); 
```

!!! note 
    *allowAnchor* a la valeur false par défaut lors de la création du traqueur. 

## Utilisation de la fonction de retour

Vous trouverez une explication détaillée dans le guide [Envoyer des données à AFS Analytics](../envoi-des-donnees/). 

La fonction de retour ou callback est appelée après l"envoi de la page à AFS Analytics.
 Elle retourne trois paramètres : 

1. Le hitType de la commande exécutée.
2. L"objet tracker.
3. L"objet params défini dans la fonction appelante.

Exemple fonction de retour: 
```js
 //définition de mon propre objet
Var monobjet={
    message:"la page vue a été envoyée a AFA Analytics",
    pagevue:document.title,
    location:window.location.href
};
//définition de ma fonction de retour
function mycallback(commande,tracker,objretour)
{
        console.log("Les informations du traqueur ont été envoyé a AFS Analytics!");
        console.log("La commande était ->",commande);
        console.log("La page était ->",objretour.pagevue,"l'url->",objretour.location);
        console.log ("L'unique ID  du visitor envoyé par AFS est->",tracker.get("visitor.id"));
        console.log ("Le traqueur est nommé ->",tracker.get("name"));
        console.log ("Le cookie du visiteur ->",tracker.get("cookie.str"));
        console.log(tracker);
}

//appels à analytics.js
aa('create', '00000003', 'auto');
aa('send', 'pageview',"autoindex","Test Page","","mycallback",monobjet);
```

Sortie sur la console : 
```sh
Les informations du traqueur ont été envoyé a AFS Analytics!
La commande était -> pageview
La page était -> Test callback 
l'url-> http://127.0.0.1/tc.html
l'unique ID  du visitor envoyé par AFS est-> 31
Le traqueur est nommé -> afstracker0
Le cookie du visiteur -> 3x6226x1191x31x6103x1
```

## Envoi d'une page vue via AutoTrack

Dans les sites avec une seule page, l'accès aux différentes sections est généralement défini à l"aide d'une ancre. 
Pour capturer la visualisation de ces sections comme des pages, vous devez : 

1. Définir l'index avec la valeur titleindex. Référence les sections avec des noms différents. 
2. Utiliser:

 - Soit l'option Autotrack: L'option Autotrack permet de définir des événements spécifiques à exécuter lors d'un click sur un lien. 
Pour cela, on définit les données dans les datasets : 
```js
<a href="#contact-us” 
   data-aa-hitType="pageview"  
   data-aa-title="contact-us" 
>contact-us</a>
```
A chaque clic, la page vue contact-us sera envoyée par anlytics.js à AFS Analytics.
 
- Soit définir votre propre fonction et l"appeler avec onclick : 

```js
/* Utilisation de onclick couplée avec une fonction appelant AFS Analytics */
 function SendPV(name) {
  aa('send','pageview','titleindex',name);  
  return true;
}

<a href="#contact-us" onclick="return sendPV("contact us");">Contact Us!</a>
```