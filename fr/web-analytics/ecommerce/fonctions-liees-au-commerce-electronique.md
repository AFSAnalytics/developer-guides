lng: fr
hero: Les fonctions liées au commerce électronique
title: Les fonctions liées au commerce électronique
description: Comment utiliser les différentes fonctions liées au commerce électronique. 


!!! warning
    Cette section est uniquement conservé à titre de référence. Si vous désirez implémenter le suivi des transactions E-Commerce sur votre site internet veuillez vous référer à la section [E-Commerce Amélioré](../ecommerce_ameliore/)


#Implémenter les fonctions liées au eCommerce

AFS Analytics offre de nombreuses fonctionnalités facilitant le suivi des sites d’E-Commerce. 
C'est-à-dire, la capture des transactions et la génération d’analyses, 
permettant de suivre les performances et l’évolution des revenus générés. 
L’installation d’AFS Analytics permet de booster l’efficacité et le retour sur investissement des boutiques en ligne. 

Ce guide explique comment utiliser les différentes fonctions liées au commerce électronique proposées par la librairie analytics.js. 
 
## Bénéfices de l’implémentation des fonctions de suivi de l’eCommerce

L’implémentation du suivi des transactions sur votre site vous permet d'accéder à de nombreux rapports : 

- Total des recettes générées.
- Recettes générées pour chaque produit.
- Liste et la quantité des produits vendus.
- Total des produits vendus.
- Nombres de transactions.
- Détail des transactions par magasin ou rayon.
- Taux de conversion.
- Retour sur investissement des campagnes marketing.
- Coût d’acquisition d’un client.
- Nombre de jours menant à une transaction.
- Profil des acheteurs.

Grâce à l'ensemble de ces analyses, vous serez capables d'observer en temps réel les tendances du jour, 
les articles dont les ventes augmentent comme ceux que se vendent moins.
 
## Etapes d’une transaction réussie

Examinons brièvement les étapes amenant à l’envoi d’une transaction à AFS Analytics. 

1. Le visiteur valide la commande. 
2. Traitement du paiement par votre plate-forme eCommerce. Il s’agit de la vérification et de l’acceptation du paiement.
3. La transaction est acceptée, l’acheteur est redirigé sur la page de remerciement Thank you page ou page de réception de votre site. La page de réception peut être générée par la plateforme d’eCommerce et affichée par votre site.

!!! note
    la page de réception ou de remerciement est très importante car c’est sur cette page que vous devez ajouter le code d’AFS Analytics permettant l’envoi des données. Une fois les données reçues par AFS, elles seront traitées en temps réel. 

## Le code à ajouter à la page de remerciement ou de réception.

La transmission des données d’une transaction s’effectue en trois étapes. Vous devez auparavant vérifier que le code de suivi d’AFS Analytics est présent sur la page. 

Différentes étapes de l’envoi d’une transaction:

1. Ajouter la transaction.
2. Ajouter les produits.
3. Envoyer les données à AFS Analytics

### Ajouter la transaction
La première étape est de spécifier les données de la transaction. On utilise la commande SET suivie du mot clé addTransaction. Le troisième argument est un objet détaillant la transaction. 

Syntaxe: 
```js
aa("set ","addTransaction",{
    "id" : "1234567",
    "affiliation" : "storename",
    "revenue" : "120.90",
    "shipping" :"12.65",
    "tax": "5.55",
    "currency": "EUR"
}) ;
```

!!! note
    Seuls les champs id, affiliation et revenue sont obligatoires. Si les champs tax ou shipping ne sont pas renseignés, ils seront initialisés avec la valeur 0. La variable Currency prend par défaut la devise mentionnée dans votre compte AFS Analytics. 

| Champ | Description
|---|---
|id| identifiant unique de la transaction. Si la valeur est -1, 0 ou auto, AFS Analytics générera un identifiant unique. 
|affiliation | nom du magasin ou l’affiliation d’où provient la transaction. Exemple : "Toys and Co" 
|revenue |revenu total de la transaction hors taxe et hors frais de transport. AFS calcul le total de la transaction en additionnant le revenue + shipping + tax. C’est une valeur numérique, la partie décimale est séparée par un point (par exemple : 118.95). 
|shipping| coût du transport. C’est une valeur numérique, la partie décimale est séparée par un point. 
|tax | total des taxes. En Europe, c’est la taxe sur la valeur ajoutée TVA ou VAT. C’est une valeur numérique 
|currency | indique la devise de la transaction. C’est le code ISO 4217, c'est-à-dire un code fr 3 lettres. Par exemple : USD pour US Dollar, EUR pour EURO, GBP pour livre sterling. 

Syntaxe simplifiée: 
```js
/* aa("set","addTransaction", id, affiliation, revenue, shipping, tax, devise); */

aa("set",
    "addTransaction",
    "1234567",
    "storename",
    "120.90",
    "12.65",
    "5.55",
    ’eur’
);
```
### Ajouter la liste des produits commandés.
Une fois les données spécifiées de la transaction, vous pouvez indiquer les articles commandés. 
On utilise la commande ==set== suivie du mot clé ==addItem==. 
Le troisième argument est un objet détaillant les spécifications du produit. 

Syntaxe:
```js
aa("set","addItem",
{
    "id":"0",
    "name": "Product1",
    "sku": "001",
    "category": "cat1",
    "price": "100",
    "quantity":"1"
});
```
| Champ | Description
|---|---
| id | identifiant de la transaction. L’identifiant est donc le même que celui spécifié pour addTransaction . Si la valeur ID est 0 ou -1 , l’identifiant sera initialisé avec la valeur définie précédemment dans addTransaction. 
| name |  nom de l’article
| sku |  référence ou le code de l’article. 
| category | la catégorie à laquelle l’article appartient. 
| price |  le prix de l’article à l’unité. La partie décimale doit être séparée par un point. 
| quantity | quantité achetée. Cette une valeur entière. 

!!! note 
    Les champs *id* et *name*sont obligatoires. Les champs *price*, *quantity* sont optionnels mais fortement recommandés. Si ils ne sont pas renseignés, le prix sera fixé à 0 et la quantité à 1. Les champs *sku* et *category* sont recommandés. Le champ *currency* est optionnel. 

Version simplifiée:
```js
/* aa("set","addItem", id, name, sku, category, price, quantity); */
aa("set",
    "addItem",
    "1234567",
    "Drone Avion",
    "SKU00358",
    "Drone",
    "256.56",
    "1"
);
```

### L’envoi des données à AFS Analytics

Une fois toutes les données spécifiées, il est temps d’envoyer le tout à AFS Analytics. C’est la dernière étape et l’envoi se fait à l’aide de la commande SEND suivie du mot clé ecommerce. 

```js
aa("send","ecommerce" ,  [callback], [params] ;
```
Les arguments *function callback* et *params* sont optionnels. 

Envois de toutes les données: 
```js
aa("send","ecommerce");
```

Exemple de code complet sur une page de réception: 
```js
<script type="text/javascript">
(function(i,s,o,g,r,a,m){i["AfsAnalyticsObject"]=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,"script","//code.afsanalytics.com/js/analytics.js","aa");
aa("create", "XXXXXXXX", "auto");
aa("send", "pageview",’titleindex’,’Thank You’);
aa("set","addTransaction","1234567","Toys Shop","417.55","15.50","86.61");
aa("set","addItem",{"id":"1234567","name": "Poupée magique","sku": "00252","category": "jouet fille","price": "125.56","quantity":"1"});
aa("set","addItem",{"id":"1234567","name": "Peluche Ours","sku": "00582","category": "Peluches","price": "35.99","quantity":"1"});
aa("set","addItem","1234567","Drone Avion","00358","Drones","256","1");
aa("send","ecommerce");
</script>
```
!!! note 
    Le cookie placé sur l’ordinateur de vos visiteurs par AFS Analytics n’est accessible qu’à partir de votre propre nom de domaine. 



### Cas ou la page de remerciement est hébergée sur la plateforme de paiement

Si la page de remerciement est hébergée par la plateforme de paiement, vous devez ajouter 
le code AFS Analytics sur cette page et spécifier le cookie du visiteur. 
Généralement lorsque la page est générée par la plateforme de paiement, 
vous pouvez ajouter du code et récupérer des variables précédemment transmis à la plateforme de paiement. 

#### 1. Récupération du cookie du visiteur sur la page de votre site internet envoyant sur la plateforme de paiement:
```js
<script type="text/javascript">
(function(i,s,o,g,r,a,m){i['AfsAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//code.afsanalytics.com/js/analytics.js','aa');

/* récupération du cookie du visiteur sur la page bon de commande de votre site
   on place le cookie dans la variable visitorCookie. */

var visitorCookie; 
aa('create', '00000003', 'auto');
aa('send', 'pageview');
aa(function(tracker){
visitorCookie=tracker.get('cookie.str');

});
</script>
```

#### 2. Envoi du cookie à la plateforme de paiement:

Lors de l’envoi des données à la plateforme de paiement, vous ajouter une variable contenant le cookie. Consultez les guides de votre plateforme de paiement pour connaitre le mode de transmission des variables personnalisées. 
```html
https://www.maplateformedepaiement.com/?.... &mavariable=visitorCookie 
```

#### 3. Récupération et transmission de la variable visitorCookie

Récupération de la variable visitorCookie et transmission du cookie à AFS Analytics sur la page de remerciement hébergée par la plateforme de paiement. 

```js
/* code sur la page  sur la "thank page" hébergée par la plateforme de paiement. */
<script>
/* le moyen de récuperer la variable dépend de la plateforme de paiement */
var visitorCookie=GetVariable("mavariable");
</script>

...
...

/* On ajoute le code d"afs analytics  */
<script type="text/javascript">
(function(i,s,o,g,r,a,m){i["AfsAnalyticsObject"]=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,"script","//code.afsanalytics.com/js/analytics.js","aa");
aa("create", "00000003", visitorCookie); //Astuce ici, on transmet le cookie à AFS Analytics.
aa("send", "pageview","titleindex","Thank page");
//on envoie les données de la transaction
aa("set","addTransaction","1234567","Toys Shop","417.55","15.50","86.61");
aa("set","addItem",{"id":"1234567","name": "Poupée magique","sku": "00252","category": "jouet fille","price": "125.56","quantity":"1"});
aa("set","addItem",{"id":"1234567","name": "Peluche Ours","sku": "00582","category": "Peluches","price": "35.99","quantity":"1"});
aa("set","addItem","1234567","Drone Avion","00358","Drones","256","1");
aa("send","ecommerce");
</script>
```

##L’API PHP

Dans certain cas, il n’est pas possible d’exécuter du code *Javascript*, 
par exemple quand les transactions sont gérées par un WebHook. 
Il existe une API en développement pour transmettre les informations à AFS Analytics via PHP, 
n’hésitez pas à contacter le support pour l’obtenir. 