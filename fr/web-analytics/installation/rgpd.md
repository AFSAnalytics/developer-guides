lng: fr
hero: Comment configurer analytic.js pour être en conformité avec la loi européenne sur la dépose des cookies
title: Comment configurer analytic.js pour être en conformité avec la loi européenne sur la dépose des cookies 
description: Comment configurer analytic.js pour être en conformité avec la loi européenne sur la dépose des cookies.




# Information RGPD destinée aux éditeurs utilisant AFS Analytics
 
## Les Cookies : Que dit la loi ?

En application de la directive européenne dite paquet télécom et à la RGPD, les internautes doivent être informés et donner leur consentement préalablement à l’enregistrement de cookies. Les éditeurs ont donc l'obligation d’obtenir ce consentement. Ce consentement est valable 13 mois maximum. 

Certains cookies sont cependant dispensés du recueil de ce consentement. 

## Cookies ne nécessitant pas le consentement préalable des utilisateurs

- Cookies identifiants de session, pour la durée d'une session, ou les traceurs persistants limités à quelques heures dans certains cas.
- Cookies de mesure d'audience en respectant certaines conditions. Voir paragraphe ci-dessous.
- Cookies strictement nécessaires pour la délivrance d'un service expressément demandé par l'abonné ou l'utilisateur.
- Cookies de panier d'achat pour un site marchand.
- Cookies d'authentification de l'internaute.
- Cookies de session créés par un lecteur multimédia.
- Cookies de session d'équilibrage de charge (" load balancing ").
- Cookies persistants de personnalisation de l'interface utilisateur.


## Cas des cookies de solutions de mesures d'audience ou de web Analytics

Pour être exemptés de demande de consentement, les cookies de mesure d'audience doivent respecter les conditions suivantes : 

1. Une information doit être donnée aux utilisateurs qui doivent pouvoir s'opposer au traitement (Opt-out).
2. Les données collectées ne doivent pas être recoupées avec d'autres traitements : Cookies partagés.
3. Le cookie doit servir qu'à la production de statistiques anonymes et ne doit pas permettre le suivi de la navigation sur différents sites. Sa durée de vie doit être limitée de 13 mois.
4. Anonymiser l’adresse IP : Pour éviter de remonter à une personne physique, on conservera uniquement les deux premiers octets de l’adresse IP.

Les solutions de web analytics qui ne respectent pas les conditions ci-dessus doivent faire l'objet du recueil du consentement préalable des utilisateurs. 

## Comment configurer AFS Analytics pour être en conformité

AFS Analytics dispose seulement des cookies *first* (ou internes en français), c'est-à-dire des cookies déposés depuis le domaine de votre site. Le contenu des cookies internes ne peut être transmis qu’à partir de votre site et ne sont pas accessibles en dehors de votre site. 

Il existe trois possibilités pour mettre votre site en conformité:

- Demander à AFS Analytics de ne pas déposer de cookies.
- Configurer AFS Analytics pour l’exemption de demande de consentement.
- Obtenir le consentement de l’internaute via analytics.js ou informer AFS sur le consentement.

## Solution 1: Demander à AFS Analytics de ne pas déposer de cookies.

C’est la solution la plus radicale. AFS ne déposera pas de cookies sur les terminaux des internautes. Seuls les cookies de sessions autorisés par la loi seront utilisés. L’inconvénient de cette solution est l’impossibilité de savoir si le visiteur est nouveau ou ancien comme d’accéder à la liste de ses précédentes visites. 

### configurer analytics.js pour ne plus déposer de cookies.

#### a. Activer la règle de consentement
On active la règle de consentement avec le paramètre ==nocookie==.

#### b. Définir la région à qui s’applique la règle de consentement.
| Region | Code
| --- | ---
| Europe | eu
| USA | us
| Toutes | all


Dans notre exemple la loi s’applique seulement aux Européens. 
```js
aa("set","cookieconsent_mode", "nocookie")
aa("set","cookieconsent_audience", "eu") ;
```

#### Comment ça marche?
AFS détecte le pays d'origine de l’internaute.
- S’il est Européen, les cookies ne sont pas déposés.
- Dans le cas contraire, les cookies sont enregistrés normalement. 
!!! note
	Le service de localisation de l’internaute rendu par AFS Analytics est garanti seulement pour les comptes premiums. Pour les comptes gratuits, vous devez informer AFS Analytics de la localisation de l’internaute. 

## Solution 2: L’exemption de demande de consentement aux internautes.

Cette solution vous permet d’être exemptée de consentement en conformité avec la réglementation. La duré du cookie est de 12 mois à partir de la première visite. 

#### a. Informer l’internaute de la présence de cookies de mesure d’audience
Prévenir dans les mentions légales de votre site que celui-ci utilise AFS Analytics comme solution d’analyse d’audience afin d’obtenir des statistiques sur la fréquentation. Vous pouvez utiliser le message suivant : 

<div class=wraptext>
```html
Afin de mieux vous servir et améliorer l’expérience utilisateur, nous analysons l'audience de notre site grâce à la solution de <a href="https://www.afsanalytics.com/fr/info/105/mesure-audience-site-internet.html">Web Analytics</a> :  <a href="https://www.afsanalytics.com/fr/">AFS Analytics</a>. Ce service conforme au règlement général sur la protection des données peut être amené à sauvegarder en tant que sous-traitant des informations personnelles (selon la définition de la RGPD) notamment un numéro unique composé de caractères alphanumérique vous identifiant. Ces données cryptées sont sauvegardées sur des serveurs sécurisés localisés en France, ou au Canada. Le Canada apporte les garanties appropriées à la protection des données selon les articles 44 et 46 du RGPD. Aucune information bancaire n'est transmise ou sauvegardée par AFS Analytics. Nous sommes les seuls propriétaires de ces données, AFS Analytics s'est engagé à ne pas divulguer, partager ou vendre ces données. La durée de stockage de ces données est limitée à 365 jours par défaut. Vous avez la possibilité de nous demander l'effacement ou la modification de ces données, veuillez contacter notre responsable des données ou la société <a href="https://www.datasense.fr">DataSense</a>, responsable des données pour AFS Analytics. Pour la collecte des données nous utilisons la librairie <a href="https://www.afsanalytics.com/fr/info/113/ajouter-code-analytics-js.html">analytics.js</a> développé par AFS Analytics. Cette librairie utilise la technologie des cookies. Les cookies sont exclusivement attachés à notre nom de domaine, "First Cookies", et nous permettent d'obtenir des données statistiques de fréquentation. Ces cookies ne sont pas partagés et ne sont pas utilisés à des fins publicitaires. Nous sommes les seuls propriétaire de ces cookies, et vous pouvez vous opposer à leur enregistrement : <a href='javascript: aa("set","cookiesconsent","optout");'> Cliquez ici pour vous opposer aux cookies de mesure d’audience d'AFS Analytics</a>
```
</div>

#### b. Inclure une option de retrait ou Opt-Out. Voir texte ci-dessus

#### c. Activer la règle de consentement dans analytics.js.
#### d. Définir la localisation des internautes concernés.
#### e Anonymiser l’adresse IP de l'internaute

Pour éviter de remonter à une personne physique, analytics.js anonymisera l’adresse IP, seul les deux premiers octets de l’adresse IP seront conservés. 

```js
/* Dans cet exemple la loi s’applique seulement aux internautes européens.  */
aa("set", "cookieconsent_mode", "exemption")
aa("set", "cookieconsent_audience", "eu") ;
```

Le paramètre de la variable cookieconsent_anonymizeipaccepte les paramètres suivants : 

| Valeur | Description
| --- | ---
| true | Seul le dernier octet est supprimé. L’IP 8.8.8.8 devient 8.8.8.0
| false | L’adresse redevient 8.8.8.8
| 1 | Dernier octet est supprimé -> 8.8.8.0 (équivalent à true)
| 2 | Les deux derniers octets sont supprimés -> 8.8.0.0
| 3 | Les trois derniers octets sont supprimés -> 8.0.0.0

!!! note 
	Il ne faut pas confondre la variable cookieconsent_anonymizeip avec anonymiseip. La première concerne seulement sur les internautes définis par cookieconsent_audience. La seconde concerne tous les visiteurs du site. 

##Solution 3 La demande de consentement aux internautes


### 1 Vous avez déjà demandé le consentement de l’internaute

Comme nous l’avons indiqué précédemment AFS Analytics via analytics.js dépose seulement des cookies first, c'est-à-dire des cookies attachés au nom de domaine de votre site. Pour cette raison, vous n’avez pas à demander un consentement spécifique pour AFS Analytics. Le consentement obtenu précédemment par le visiteur est valable pour la dépose des cookies gérés par AFS Analytics. Dans ce cas, vous devez juste mette à jour vos mentions légales ou mentions d’utilisations. 

<div class=wraptext>
```html
Afin de mieux vous servir et améliorer l’expérience utilisateur, nous analysons l'audience de notre site grâce à la solution de <a href="https://www.afsanalytics.com/fr/info/105/mesure-audience-site-internet.html">Web Analytics</a> :  <a href="https://www.afsanalytics.com/fr/">AFS Analytics</a>. Ce service conforme au règlement général sur la protection des données peut être amené à sauvegarder en tant que sous-traitant des informations personnelles (selon la définition de la RGPD) notamment un numéro unique composé de caractères alphanumérique vous identifiant. Ces données cryptées sont sauvegardées sur des serveurs sécurisés localisés en France, ou au Canada. Le Canada apporte les garanties appropriées à la protection des données selon les articles 44 et 46 du RGPD. Aucune information bancaire n'est transmise ou sauvegardée par AFS Analytics. Nous sommes les seuls propriétaires de ces données, AFS Analytics s'est engagé à ne pas divulguer, partager ou vendre ces données. La durée de stockage de ces données est limitée à 365 jours par défaut. Vous avez la possibilité de nous demander l'effacement ou la modification de ces données, veuillez contacter notre responsable des données ou la société <a href="https://www.datasense.fr">DataSense</a>, responsable des données pour AFS Analytics. Pour la collecte des données nous utilisons la librairie <a href="https://www.afsanalytics.com/fr/info/113/ajouter-code-analytics-js.html">analytics.js</a> développé par AFS Analytics. Cette librairie utilise la technologie des cookies. Les cookies sont exclusivement attachés à notre nom de domaine, "First Cookies", et nous permettent d'obtenir des données statistiques de fréquentation. Ces cookies ne sont pas partagés et ne sont pas utilisés à des fins publicitaires. Nous sommes les seuls propriétaire de ces cookies, et vous pouvez vous opposer à leur enregistrement : <a href='javascript: aa("set","cookiesconsent","optout");'> Cliquez ici pour vous opposer aux cookies de mesure d’audience d'AFS Analytics</a>
```
</div>

### 2 Vous n’avez pas demandé le consentement de l’internaute

Vous devez informer l’internaute de la dépose de cookies et ajouter une mention dans votre page vie privée ou mentions légales. 
Quand le consentement de l’internaute est valable? 

Dans la mesure où le consentement ne doit pas être ambigu, le bandeau de consentement ne doit pas disparaître tant que la personne n'a pas poursuivi sa navigation, c'est-à-dire tant qu'elle ne s'est pas rendue sur une autre page du site ou n'a pas cliqué sur un élément du site (image, lien, bouton " rechercher "). 

#### Les étapes à respecter:
a. Afficher un bandeau informant sur la dépose de cookies: 
En poursuivant votre navigation sur ce site, vous acceptez l’utilisation de Cookies pour réaliser des statistiques de visites. 
b.La mention En Savoir Plus est lié à une page d’information: 
Optionnellement vous pouvez ajouter un lien en savoir plus envoyant sur une page détaillant le rôle des cookies enregistrés et une option opt-out (retrait de cookies). 
b.Informer les internautes sur l'utilisation des cookies: 
Utilisez ce message dans la page en savoir plus ou dans vos mentions légales: 

<div class=wraptext>
```html
Afin de mieux vous servir et améliorer l’expérience utilisateur, nous analysons l'audience de notre site grâce à la solution de <a href="https://www.afsanalytics.com/fr/info/105/mesure-audience-site-internet.html">Web Analytics</a> :  <a href="https://www.afsanalytics.com/fr/">AFS Analytics</a>. Ce service conforme au règlement général sur la protection des données peut être amené à sauvegarder en tant que sous-traitant des informations personnelles (selon la définition de la RGPD) notamment un numéro unique composé de caractères alphanumérique vous identifiant. Ces données cryptées sont sauvegardées sur des serveurs sécurisés localisés en France, ou au Canada. Le Canada apporte les garanties appropriées à la protection des données selon les articles 44 et 46 du RGPD. Aucune information bancaire n'est transmise ou sauvegardée par AFS Analytics. Nous sommes les seuls propriétaires de ces données, AFS Analytics s'est engagé à ne pas divulguer, partager ou vendre ces données. La durée de stockage de ces données est limitée à 365 jours par défaut. Vous avez la possibilité de nous demander l'effacement ou la modification de ces données, veuillez contacter notre responsable des données ou la société <a href="https://www.datasense.fr">DataSense</a>, responsable des données pour AFS Analytics. Pour la collecte des données nous utilisons la librairie <a href="https://www.afsanalytics.com/fr/info/113/ajouter-code-analytics-js.html">analytics.js</a> développé par AFS Analytics. Cette librairie utilise la technologie des cookies. Les cookies sont exclusivement attachés à notre nom de domaine, "First Cookies", et nous permettent d'obtenir des données statistiques de fréquentation. Ces cookies ne sont pas partagés et ne sont pas utilisés à des fins publicitaires. Nous sommes les seuls propriétaire de ces cookies, et vous pouvez vous opposer à leur enregistrement : <a href='javascript: aa("set","cookiesconsent","optout");'> Cliquez ici pour vous opposer aux cookies de mesure d’audience d'AFS Analytics</a>
```
</div>


####Comment configurer analytics.js:

AFS Analytics via la librairie analytics.js vous propose d’effectuer toute la partie technique pour vous.

AFS Analytics, effectue les opérations suivantes : 

- AFS utilise son service de localisation pour définir l’internaute est européen.

- L’internaute a-t-il donné son consentement. 
	Si Oui, le cookie cookieconsent_status existe il?
		Oui, lire son contenu:

	Si deny or optout. Pas de consentement, pas de cookies enregistrés. Seul un cookie de session est déposé.
allow : Les cookies sont déposés normalement.

Si l'internaute n'a pas déjà donné son consentement, un bandeau de demande sera affiché automatiquement: mode automatisé consent_auto; ou pourra être affiché par votre propre routine: mode consent. 

!!! note  
	Dans le mode automatisé, les messages de consentement affichés par analytics.js sont en Français ou en Anglais selon l’origine de l’internaute. 

Exemple de code avec le mode automatisé:

Si vous souhaitez l’affichage automatisé du bandeau par analytics.js, vous devez définir le mode de consentement avec consent_auto. 

```js
/* Exemple de code avec le mode automatisé: */

aa("set","cookieconsent_mode", "consent_auto")
aa("set","cookieconsent_audience","eu") ;
```


Optionnellement dans ce mode vous pouvez définir votre propre message, le texte du bouton et une fonction callback: 

| Argument | Description
| --- | ---
|cookieconsent_message| le message à afficher.
|cookieconsent_button| le message du bouton.
|cookieconsent_callback| votre propre fonction, vous pouvez changer les attributs de la boite ou du texte.

Exemple: 
```js
aa("set", "cookieconsent_mode", "consent_auto")
aa("set", "cookieconsent_audience", "eu") ;
aa("set", "cookieconsent_message", "En poursuivant votre navigation, vous acceptez l’utilisation de Cookies pour réaliser des statistiques et vous proposer des publicités") ;
aa("set", "cookieconsent_button", "J'accepte") ;
```
 
La fonction callback permet de modifier les attributs des éléments. 

```js
/* exemple avec fonction callback */


aa("set", "cookieconsent_mode", "consent_auto")
aa("set", "cookieconsent_audience", "eu") ;
aa("set", "cookieconsent_message", "En poursuivant votre navigation, vous acceptez l’utilisation de Cookies pour réaliser des statistiques et vous proposer des publicités") ;
aa("set", "cookieconsent_button", "J'accepte") ;
aa("set", "cookieconsent_callback", "mafonction") ;
```


En mode normal, l'affichage de la boite par analytics.js. L’affichage est géré par votre propre routine. 
```js
/* exemple de code avec le mode normal */

aa("set", "cookieconsent_mode", "consent")
aa("set", "cookieconsent_audience", "eu") ;
aa("set", "cookieconsent_callback", "askconsent") ;
```


#### Fonction de localisation d'AFS Analytics

!!! note 
	Si vous utilisez le service de localisation d’AFS Anlaytics, un cookie aa_country sera créé contenant le pays de l’internaute. 

#### Fonction d'affichage du bandeau de consentement utilisée dans analytics.js

```js
function consentbox()
 {
   var m=this.cookieconsent_message;
   var b=this.cookieconsent_button;
    var l=0; 
     
  if (m==-1)
   {
   
   var l0 = navigator.language || navigator.userLanguage; 
   var l1 =document.getElementsByTagName('html')[0].getAttribute('lang');
   var l2=document.getElementsByTagName('html')[0].getAttribute('xml:lang');
   if (l0=="fr" || l1=="fr" || l2=="fr") l=1;
   m="This site uses cookies. By continuing to browse the site you are agreeing to our use of cookies.";
   b="Accept";
    if (l==1)
    {
    var m="En poursuivant votre navigation, vous acceptez l’utilisation de Cookies pour réaliser des statistiques et vous proposer des publicités.";
    b="J'accepte";
    }
   } 
   
   var div=document.createElement('div');
    div.id = 'consent_box';
    document.body.appendChild(div);
    div = document.getElementById("consent_box");
    div.style.width="100%";
    div.style.margin="0";
    div.style.background="rgba(0, 0, 0, 0.80)";
    div.style.padding="5px";
    div.style.color="#FFF";
    div.style.position="fixed";
    div.style.display="none";
    div.style.bottom="0";
    div.style.right="0";
    div.style.left="0";
    div.style.zIndex="9999";
    div.style.fontSize="13px";
    div.style.fontFamily="sans-serif"; 
    var text='<div class="consent_design">';
    text+='<div id="consent_text">'+m+'</div>';
    if (b!=-1) text +='<div id="consent_button"  onclick="document.getElementById('consent_box').style.display='none';aa('set','cookieconsent_status','allow');">'+b+'</div>';
    text+='</div>';
    div = document.getElementById("consent_box");
    div.innerHTML=text;
    var div1=document.getElementById("consent_text");
    div1.style.minheight="20px";
    div1.style.padding="10px";
    div1.style.width="70%";
    div1.style.display="inline-block";
    div1.style.cssFloat="left";
    
    if (b!=-1) 
    {       
    div1=document.getElementById("consent_button");
    div1.style.fontFamily="sans-serif";
    div1.style.fontSize="13px";
    div1.style.margin="10px";
    div1.style.marginRight="20px";
    div1.style.display="inline-block";
    div1.style.cssFloat="right";   
    div1.style.border="2px solid rgba(255,255,255,1)";
    div1.style.borderRadius="2px";
    div1.style.padding="5px 10px";
    div1.style.fontWeight="400";
    div1.style.opacity=".90";
    div1.style.cursor="pointer";
    }
         
      div.style.display ="block";
   };
 ```

### Les options supplémentaires

#### Changer le nom du cookie de consentement
```js
aa("set", "cookiesconsent_name", "nameofcookieconsent") ; 
```
#### Le service de localisation d’AFS Analytics

A chaque connexion de l’internaute, analytics.js fait appel à son service de localisation pour détecter l’origine du visiteur et dépose le cookie aa_country contenant le code de son pays. Ce cookie est exempté de la demande de consentement de l’internaute. Toutefois la disponibilité de ce service est exclusivement assurée à nos abonnés aux plans premium. 

Pour les comptes gratuits, nous vous conseillons de désactiver ce service, et de renseigner AFS sur le pays du visiteur. 

```js
aa(set, "localisation", "disable") ;
aa(set, "country", "FR") ;
```