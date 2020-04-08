lng: fr
hero: Capture des événements
title: Capture des événements
description:  comment utiliser la commande send pour l’envoi des événements à AFS Analytics


#La capture des événements

La capture des événements par AFS Analytics permet de mesurer les interactions 
entre les visiteurs et les pages d’un site internet. 
Ces informations révèlent les erreurs de conception et permettent d’améliorer l’expérience utilisateur et la navigation des visiteurs. 

Les événements sont envoyés à AFS Analytics via la commande Send ou détectés automatiquement par l’activation de l’option autotrack. 

Ce guide explique l’utilisation de la commande send pour l’envoi des événements à AFS Analytics. 

!!! impportant
    Les catégories, actions ou types doivent être spécifiés en Anglais. 

## La capture des événements avec la commande SEND


L’utilisation de la commande send couplé au type d’appel event envoie un événement à AFS Analytics. 

Syntaxe simplifiée:
 
```js
aa("send","event",[category], [action],[label], [type],[url], [callback],[params]) ; 
```

| Champs obligatoires | Description
| --- | ---
| category| définit la catégorie de l’événement (par exemple : Video). Le champ alternatif : eventCategory est accepté afin d’assurer la compatibilité avec Google Analytics. 
| action | spécifie le type d’action attachée à la catégorie (par exemple play). L’appellation eventAction pour ce champ est accepté assurant la compatibilité avec Google Analytics. 
| label | donne un titre à l’événement (par exemple: Ma vidéo de vacance). eventLabel est accepté afin d’assurer la compatibilité avec Google Analytics. 

| Champs optionnels | Description
| --- | ---
| type | Ce champ définit le type ou une information supplémentaire à propos de l’événement. Champ optionnel. 
| url | Ce champ définit une location à l’événement. Champ optionnel. 
| callback | Fonction de retour à appeler après la transmission de l’événement aux serveurs d’AFS Analytics. La fonction renvoie trois paramètres. Le hitType, l’objet event et l’objet params. Ce paramètre peut être une fonction ou une chaine de caractères contenant le nom de la fonction. Champ optionnel 
| params | Un objet définit dans la fonction appelante à retourner comme paramètres dans la fonction de retour. Champ optionnel 

!!! tip
    Une chaine de caractères vide comme paramètre indique à analytics.js d’utiliser la valeur par défaut. 


Exemple d’envoi d’un événement: 

```js
/* indique qu’un visiteur à débuté la visualisation d’une vidéo  */

aa("send", "event", "video", "play", "Ma video");
```

La même commande avec un objet comme argument: 

 
```js

/* utilisation de champs compatibles avec Google Analytics. */

aa("send", {
  hitType: "event",
  eventCategory: "Video",
  eventAction: "play",
  eventLabel: "Ma video"
});

/* Version avancée utilisant des champs spécifiques  à AFS Analytics  */


function mycallback(a,b,c) { console.log(a,b,c); }

aa("send", {
  hitType: "event",
  eventCategory: "video",
  eventAction: "stop",
  eventLabel: "Ma video test",
  eventType:"all",
  eventUrl: "http://www.afsanalytics/mavideo.avi",
  hitCallback: mycallback,
  params:{message:"this has been sent"}
});
```

!!! important
    Ne pas confondre le champ hitType avec le champ type. 

## L’option "Autotrack" et les "datasets"

Dans les exemples suivants, vous trouverez une version utilisant ==autotrack== et les ==datasets==.
Les exemples fonctionnent si l’option autotrack est activée en mode Dataset ou On. 

Si vous avez un doute sur le réglage de l’option autotrack, 
ajoutez la ligne suivante activant autotrack en mode dataset après la création du traqueur. 

```js
aa( "Set" ,"autotrack", "dataset") ;
```

### Définir les datasets

La syntaxe d’un ==dataset== dans une balise HTML est la suivante : 
```js
data-[datasetprefix]-[nom du champ à renseigner]="valeur du champ"
```
!!! note 
    datasetprefix est une variable définie avec la valeur par défaut aa dans analytics.js. Elle est modifiable grâce à l’option set. 

Exemple d’initialisation du champ category 
```js
data-aa-category="click"
```

Les champs datasets sont ceux propre à AFS Analytics. 
C'est-à-dire *hittype*, *category*, *action*, *label*, *url*, *callback*, *params*. 

Dans les datasets seul les champs *category* et *label* sont obligatoires. 
Le champ action peut être recommandé pour certains types d’événements. 
Les autres champs sont généralement détectés. Par défaut le champ *hitType* est réglé sur event. 

### Les balises détectées par Autotrack

L’option ==autotrack== détecte les datasets des balises *a*, *div*, *button*, *iframe*, *form*.
 
Exemple d’utilisation de dataset dans une iframe de youtube. 
```js
<iframe width="480" height="280" src="https://www.youtube.com/embed/cnBtRh08ShQ?rel=0" frameborder="0"  
    data-aa-category="video" 
    data-aa-action="start" 
    data-aa-label="Advanced visitor tracking">
</iframe>
```
A chaque clic sur la vidéo, l’événement sera capturé par AFS Analytics. 


## L’événement Click

Si le champ action est vide, analytics.js détectera automatiquement le type du clic: 
*inside* ou *outbound*. Si le champ url n’est pas renseigné, il sera remplacé par *none*. 
```js
aa("send", "event", "click", "inside", "Mon clic’);
```

Pour un clic sortant : 
```js
aa("send", "event", "click", "outbound", "Mon clic’);
```

### La détection des clics avec "Autotrack" et les "datasets".

```js
<a href="https://afsanalytics.com" 
    data-aa-hitType="event" 
    data-aa-category="click" 
    data-aa-label="mon super click" >
mon super clic</a>
```
!!! note 
    AFS Analytics détectera automatiquement les champs url, type et action, s’ils ne sont pas définis dans les *datasets*. 

## L’événement Download

L’envoi d’un fichier téléchargé se transmet à analytics.js via la catégorie *Download*. 
Le champ *type* n’étant pas utile on indique la valeur *none*, 
le champ *URL* indique l’emplacement du fichier. 

```js
aa(
    "send", 
    "event", 
    "download", 
    "successful", 
    "Mon fichier",
    "non",
    "http://monsite.com/monfichier.pdf"
);
```

### La détection des téléchargements avec Autotrack et les Datasets

Avec l’option autotrack et les datasets, les champs url et type n’ont pas besoin d’être renseignés 

```js
<a href="http://monsite.com/monfichier.pdf" 
   data-aa-hitType="event" 
   data-aa-category="download" 
   data-aa-label="mon super fichier pdf" 
   data-aa-callback="mycallback" data-aa-params="{message:"test"}" >
monfichier.pdf</a>
```

!!! note
    Avec l’option autotrack et les datasets, les champs url et type n’ont pas besoin d’être renseignés 


!!! note 
    Notez le passage de la fonction de retour (callback) qui sera appelée après l’envoi de l’événement à analytics.js. L’url n’a pas besoin d’être spécifiée dans les « dataset», elle est déjà renseignée dans la balise a href. 


## L’événement Form

AFS Analytics permet de détecter les événements liés au remplissage des formulaires. 
Si les événements sont envoyés correctement, 
AFS calculera le temps moyen de remplissage et le taux d’abandon. La catégorie form est réservé au formulaire. 

### Différentes étapes du remplissage d’un formulaire 

- l’ouverture du formulaire : open 
```js
aa("send", "event", "form", "open", "Mon formulaire");
```

- la soumission du formulaire : submit
```js
aa("send", "event", "form", "submit", "Mon formulaire");
```

- Le résultat de la soumission 

```js
/* *En cas de succès */
aa("send", "event", "form", "successful", "Mon formulaire");

/* En cas d’échec */
aa("send", "event", "form", "failed’, "Mon formulaire");
```

- La fermeture du formulaire: close
```js
aa("send", "event", "form", "close", "Mon formulaire");
```

Dans le cas ou le formulaire est fermé avec un bouton d’annulation:
```js
aa("send", "event", "form", "cancel", "Mon formulaire");
aa("send", "event", "form", "close", "Mon formulaire");

/* ou en utilisant l’action: cancelandclose */

aa("send", "event", "form", "cancelandclose", "Mon formulaire");
```

Si les actions open et close ont été correctement définies. 
Le temps moyen de visualisation de la fenêtre sera affiché sur le tableau de bord. 

### Les valeurs du champ type associées au formulaire

En ajoutant le paramètre type vous pouvez définir le type de la forme. 
Les options disponibles sont : 

- information
- settings
- signup
- login
- contact
- logout

### Capture des formulaires avec "autotrack"
!!! note
    Cette partie sera ajoutée ultérieurement. 

## L’événement Window

L’événement window offre deux actions : open et close. 

Ouverture de la fenêtre : open 
```js
aa("send", "event", "window", "open", "Ma fenêtre");
```

Fermeture avec close :
```js
aa("send", "event", "window", "close", "Ma fenêtre");
```
Si les actions open et close ont été correctement définies, 
le temps moyen de visualisation de la fenêtre sera affiché sur le tableau de bord. 

## L’événement Video

Quatre actions sont proposées pour l’événement Video: 

- start
- pause
- resume 
- stop

!!! tip 
    L’action start peut être remplacée par play, la librairie analytics.js accepte les deux possibilités. 

- Quand un utilisateur commence la lecture de la video:
```js
aa("send", "event", "video", "start", "Ma vidéo");
```

- Quand un utilisateur clique sur le bouton pause: 
```js
aa("send", "event", "video", "pause", "Ma vidéo");
```

- Quand un utilisateur reprend la lecture de la vidéo: 
```js
aa("send", "event", "video", "resume", "Ma vidéo");
```

- Lorsque La vidéo est achevée ou interrompue par l’utilisateur:
```js
aa("send", "event", "video", "stop", "Ma vidéo");
```

### Capture de la lecture d’une vidéo YouTube avec "autotrack" et les datasets.

Comme mentionné ci-dessus, l’action play peut être utilisé comme alternative à l’action start. 

```js
<iframe src="https://www.youtube.com/embed/cnBtRh08ShQ?rel=0" frameborder="0" 
    data-aa-category="video" 
    data-aa-action="play" 
    data-aa-label="AFS Analytics vidéo">
</iframe>
```

## L’événement Alert

L’événement *alert* est particulièrement util pour envoyer des messages d’alertes personnalisés. 
De nombreuses entreprise utilisent un compte AFS Analytics dédié à la capture d'erreurs sure leur site. 
Cette option, utilisée par les agences web pour assurer la fiabilité des sites développés, 
permet pour chaque alerte de consulter la fiche et la configuration du visiteur qui a généré l’erreur. 

Actions disponibles pour l’événement alert: 

| Type | Description
| --- | ---
| Post | Toujours vrai, l’alerte apparait dans le rapport regroupant les alertes
| Email | L’alerte est transmise par email à l’adresse email définie dans AFS Analytics
| SMS| L’alerte est transmise par SMS
| EmailandSms | L’alerte est transmise par SMS et EMAIL

Pour le type d’alerte, il est possible de choisir entre *warning*, *debug*, *error* ou *fatal*. 
```js
aa("send", "event", "alert", "post", "Erreur routine javascript", "fatal");
```

## L’événement Campaign

L’événement campaign est généré automatiquement par analytics.js 
grâce aux paramètres utm présents dans la query string de la page. 
Veuillez consulter le guide [Comment mesurer le trafic des campagnes publicitaires](../comment-utiliser-les-variables-utm/) pour plus de renseignements. 

##Les événements liés à l’e-commerce.

La capture des ventes et des transactions liées à l’e-commerce sont décrites dans le guide 
[Capture des ventes et E-commerce](../fonctions-liees-au-commerce-electronique/)


Les options prédéfinies acceptées par AFS Analytics.

AFS Analytics accepte seulement des "catégories", "actions" et "types" prédéfinis. Voici une liste non exhaustive
des valeurs acceptées:

| Type | Valeur acceptée
| --- | ---
|  catégories des événements | click, download form, video, window, alert, navigation 
| Les actions | None, Open, Close, Outbound, Inside, Send, Submit, Cancel, Cancelandclose, Successful, Failed, Start, End, Proceed, View, Post, Email,SMS, EmailAndSMS, Play, Pause, Stop, Resume 
| Les types | None, Button, Link, Div, iframe, Page, Information, Alert, Setting, Signup, Login, Warning, Fatal, Debug, Error, Contact, Logout, Menu

