lng: fr
hero: Capture des événements automatisés
title: Capture des événements automatisés
description: Comment configurer analytic.js pour être en conformité avec la loi européenne sur la dépose des cookies.

#  Capture des événements automatisés

## Introduction 

AFS Analytics offre une option permettant la capture automatique des interactions entre les visiteurs et les pages d’un site web. Nommée AutoTrack, cette fonctionnalité est un atout majeur de notre solution [web analytics](https://www.afsanalytics.com/fr/). 

## Quels sont les événements capturés par l’option "Autotrack" ?

L’option ==autotrack== capture les clics associés aux liens, aux éléments HTML et aux iframes contenus dans une page web. Une fois détecté, l’élément associé au clic est analysé afin de définir ses attributs et l’action déclenchée. Il peut s’agir du téléchargement d’un fichier, de la visualisation d’ une vidéo, de l’ouverture d’une fenêtre, de la soumission d’un formulaire ou tout simplement d’un clic sur un lien. 

L’envoi d’une page vue peut aussi être déclenché par l’option autotrack . Cela permet d’obtenir un rapport détaillé sur les sections les plus visualisées des sites composés d’une seule page. 

Autotrack détecte automatiquement les caractéristique d’un événement, mais la spécification d’informations via les *datasets* augmente la fiabilité et l’efficacité de cette fonctionnalité. 

## DataSets

### Introduction

HTML5 donne la possibilité d’associer à un élément HTML des données grâce à l’attribut data- appelé dataset . Pour utiliser cette fonctionnalité, votre page HTML doit être compatible avec HTML5, c'est-à-dire, quelle doit inclure le doctype HTML5:
```html
<!DOCTYPE html>. 
```

La syntaxe d’un *DataSet* se compose du nom de la variable précédé du préfixe ==data-== suivi de sa valeur placée dans une chaine de caractères. 

```html
<element data-category="valeur">…</element>
```
Dans notre exemple, le dataset est *category* et sa valeur est *valeur*. 

### Intérêt 

L’intérêt des datasets réside dans la simplification du stockage des données dans les documents HTML et plus particulièrement dans les éléments. Grâce aux dataSets, vous pouvez fournir à Autotrack de nombreuses données sur un événement ou une interaction. 

## Les différents modes de l’option AutoTrack

L’option AutoTrack accepte trois modes différents. Le mode souhaité est transmis avec la commande set via la fonction aa(). Ce réglage doit suivre la création du traqueur. 

### Mode "off"
Dans cet état, l’option Autotrack est complétement désactivée. Il n’y a aucune capture automatique des évènements. 

### Mode "dataSet"
Dans ce mode, seul les éléments avec des datasets définis sont capturés. 

### Mode "on"
Dans ce mode, tous les évènements sont capturés, même si aucun dataset n’est défini. 


##Les sous-réglages d’AutoTrack

AFS Analytics vous permet de désactiver certaines fonctionnalités d’ AutoTrack. Cela s’avère utile si vous ne souhaitez pas capturer certains événements ou éléments. 

!!! note 
	Ces réglages doivent s’effectuer après la spécification du mode principal d’ autotrack. Dans le cas contraire, ils seront ignorés. 

Trois modes sont disponible pour les sous réglages: 

| Mode | Action
| --- | ---
| off | Désactive complètement
| dataset | Capture seulement si les *dataset* sont définis
| on |Capture de tous les événements


Pour définir un sous réglage, on ajoute un point à ==autotrack==suivi du nom du sous-réglage. 

```js
aa ("set","autotrack.category",[state]);

/* capturer seulement les clics sortants. (a href) */
aa ("set","autotrack","off");
aa ("set","autotrack.outboundclick","on");

/* désactiver les clics sortants provenant des  iframes */
aa ("set","autotrack.iframe","off");
```

!!! note 
	Il existe une hiérarchie dans la définition des sous réglages. Vous devez en premier lieu définir le réglage général autotrack, puis en second les sous-réglages insideclicks, outboundclick, download,video et en dernier les sous-réglages des éléments *iframe*, *div*, et *button*. 
```js

/* first setting */
aa ("set","autotrack","on");

/* disable inside clicks (second setting) */
aa ("set","autotrack.insideclick","off");

/* disable iframe tracking (last setting) */
aa ("set","autotrack.iframe","off");
```

### Autotrack: Vidéo

Change le mode de capture des vidéos. 

```js
aa("set","autotrack.video","off");

/* la même chose avec un objet */
aa("set","autotrack",{"video":"off"});
```	

!!! note 
	Le sous réglage "iframe" prendra la valeur du sous-réglage vidéo si "iframe" est réglé sur "off". 


## Autotrack: Download

Change le mode de capture des téléchargements. 

```js
aa("set","autotrack.download","off");
```

!!! note 
	Les sous réglages *iframe*, *div* et *button* prendront la valeur du sous-réglage *download* si ils sont réglés sur *off*. 

### Autotrack: Clicks sortants

Change le mode de capture des clics sortants ou *Exit clicks*. 
```js
aa("set","autotrack.outboundclick","off");
```
!!! note 
	Les sous réglages *iframe*, *div* et *button* prendront la valeur du sous-réglage *outboundclick* si ils sont réglés sur *off*. 

### Autotrack: Clicks entrants

Change le mode de capture des clicks ayant pour destination une page du site. 

```js
aa("set","autotrack.insideclick","off");
```
!!! note 
	Les sous réglages *iframe*, *div* et *button* prendront la valeur du sous-réglage *insideclick* si ils sont réglés sur *off*. 

### Autotrack: IFrame

Change le mode de capture des éléments iframe. 

```js
aa("set","autotrack.iframe.off");

```
### Autotrack: Div

Change le mode de capture des éléments div. 

```js
aa("set","autotrack.div","off");
```
### Autotrack: Button

Change le mode de capture des éléments button. 

```js
aa("set","autotrack.button","off");
```

Réglages de plusieurs options avec une seule ligne de code:
```js
aa("set","autotrack","dataset");
aa("set","autotrack",{"insideclick":"off", "iframe":off});
```

## Définir les attributs Datasets pour l’option Autotrack

La syntaxe d’un dataset défini pour autotrack est la suivante : 
```js
data-[datasetprefix]-[nom du champ à renseigner]='valeur du champ'
```
!!! note 
	*datasetprefix* est une variable définie avec la valeur par défaut aa. 

Exemple pour le champ catégorie: 
```js
data-aa-category='click'
```

## Les différents champs "dataset" disponibles
| Champ | Descriptions
| --- | ---
|  hitType (optionnel) |Ce champ spécifie le type de hit. Il peut prendre deux valeurs : event ou pageview. S’il n’est pas défini, il sera configuré avec event. 
| label (obligatoire)| Ce champ spécifie le titre de l’évènement. Si le hitType est pageview, le champ label peut être remplacé par title. 
| category | indique la catégorie de l’évènement : click, download, form, video, window, alert et navigation 
| action |  spécifie l’action. Par exemple pour un clic : Inside or outbound . Pour obtenir la liste des actions disponibles, veuillez consulter le document [Capture des événements](../capture-des-evenements/). 
|type | Ce champ spécifie le type de l’événement. Ne pas confondre avec le hitType. 
|url |  spécifie la destination de l’évènement. 
| callback |  spécifie une fonction de retour (callback).
| params | Ce champ spécifie une chaine de caractère à transmettre à la fonction de retour. 


## Exemples d’utilisation de l’option AutoTrack

### La détection des clics avec autotrack et les datasets

```html
<a href="https://www.mysite.com" 
	data-aa-hitType="event" 
	data-aa-category="click" 
	data-aa-label="mon click" >
mon clic</a>
```
!!! note
	AFS Analytics détectera automatiquement les champs *url*, *type* et *action*, s’ils ne sont pas définis dans les datasets. 

### La détection des téléchargements avec autotrack et les datasets

Avec l’option autotrack et les datasets, les champs url et type n’ont pas besoin d’être renseignés 
```html
<a href="http://monsite.com/monfichier.pdf" 
	data-aa-hitType="event" 
	data-aa-category="download" 
	data-aa-label="mon fichier pdf" 
	data-aa-callback="mycallback" 
	data-aa-params="{message:'test'}">
monfichier.pdf</a>
```
!!! note
	Le passage de la fonction de retour (callback) qui sera appelée après l’envoi de l’événement à analytics.js. L’url n’a pas besoin d’être spécifiée dans les dataset, elle est déjà renseignée dans la balise a href. 

### Capture de la lecture d’une vidéo YouTube avec autotrack et les datasets.

L’action play peut être utilisée comme alternative à l’action start. 

```html
<iframe src="https://www.youtube.com/embed/cnBtRh08ShQ?rel=0" frameborder="0" *
	data-aa-category="video" 
	data-aa-action="play" 
	data-aa-label="AFS Analytics vidéo">
</iframe>
```

## Conclusion
Utilisé à bon escient, l’option AutoTrack permet de capturer la plupart des interactions entre les visiteurs et les pages d’un site web sans aucune ligne de code. 

