lng: fr
hero: L’E-Commerce Amélioré (Enhanced E-commerce)
title: L’E-Commerce Amélioré (Enhanced E-commerce)
description: Ce document décrit les fonctions dédiées au commerce électronique amélioré disponibles dans analytics.js 


# Integrer l'E-Commerce amélioré à votre site

Ce document décrit les fonctions dédiées au commerce électronique amélioré disponibles dans analytics.js.

## Aperçu

Les fonctions dédiées au commerce électronique amélioré d’analytics.js permettent de mesurer les interactions des utilisateurs avec les produits proposés dans la boutique, et d’analyser leur comportement lors des différentes étapes du processus d’achat.  

On mesure entre autres les données suivantes :

* Le volume d'impressions des produits
* Les clics sur les produits
* Les vues détaillées des produits
* L'ajout et la suppression des produits dans les paniers d'achat
* L'inventaire des paniers d'achat
* Le passage à la caisse.
* Les transactions et les remboursements.
* Les étapes du processus d'achat.


## Compatibilité avec les fonctions d’E-commerce basiques

Les fonctions de l’E-commerce amélioré ne doivent pas être utilisées avec celles de l’E-Commerce basique. Les deux systèmes ne doivent pas cohabiter. 

Si vous avez déjà implémenté les fonctions de l’E-commerce basique et souhaitez commencer à utiliser le commerce électronique amélioré, vous devez supprimer de votre site tout le code faisant appel aux fonctions de l’E-commerce basique.

## Les données et actions disponibles pour l’E-commerce amélioré

Il existe plusieurs objets utilisés par analytics.js : 
* Les données d’impression, 
* Les données de produits, 
* Les données attachées aux actions.

### Les données d’impression

Les données d’impression sont utilisées lors de l’affichage d’un produit sur l’une des pages de la boutique. 

Les données disponibles pour les impressions sont les suivantes :

|   Clé     |	Type    |   Obligatoire     | 	Description     |
|:----------|:----------|:------------------|:------------------|
|  **id**	|   texte   | **Oui**              |	L'ID du produit ou SKU (exemple : P67890).|
|  **name** |	texte 	| **Oui** 	            |	Nom du produit (exemple : Pantalon battle).|
|  **list**	|	texte 	| Non		        |   le nom de la liste ou la collection à laquelle appartient le Produit. (Exemple : pantalon homme.)|
|  **brand**|	texte	| Non               |	La marque du produit (exemple : Lewis).|
|  **category**| texte 	| Non               |	La catégorie à laquelle appartient le produit. Utilisez / pour spécifier les niveaux de hiérarchie (par exemple, Vêtements / Hommes / T-shirts).|
|  **variant**  | 	texte   |	Non         |	La déclinaison du produit (par exemple : noir).|
|  **position** |	entier  |	Non		    |   La position du produit dans la liste d’affichage.|
|  **price**    |	nombre	|   Non	        |	Le prix de vente produit  (exemple : 29.20).|	
|  **currency** |	devise	|   Non		    |   Devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217).|



### Les données de produits

Ce sont les données décrivant un produit individuel.  Ces données sont utilisées lors de la consultation de la page du produit, de son ajout ou suppression du panier, de son achat, etc...

L’objet des données d’un produit contiennent les valeurs suivantes :

|Clé            |Type       | Obligatoire |	Description                                 |
|:--------------|:----------|:----------|:---------------------------------------------|
|**id**         |texte      |	**Oui**     |L'ID du produit ou SKU (par exemple P67890).   |
|**name**       |texte 	    | **Oui**     |Le nom du produit (par exemple, T-shirt Android).| 
|**brand**      |texte      |   Non 	|La marque associée au produit.|
|**category**   |texte 	    |   Non		|La catégorie à laquelle appartient le produit. Utilisez / pour spécifier les niveaux de hiérarchie (par exemple, Vêtements/Hommes/T-shirts). |
|**variant**    |texte      |	Non     |La variante du produit (par exemple : noir). |
|**price**      |nombre     |	Non     |Le prix du produit (exemple : 29.20). Hors Taxes |
|**quantity**   |entier     |	Non     |La  quantité (exemple 2). |
|**coupon**     |texte      |  	Non     |Le coupon code associé au produit. |
|**position**   |entier     |	Non     |La position du produit dans la liste d’affichage. |
|**currency**   |devise	    |   Non     |Devise [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) |




### Les données relatives aux actions

Ce sont les données attachées à une action.

|Clé            |Type       | Obligatoire| 	Description                                | 
|:--------------|:----------|:----------|:---------------------------------------------|
|**id**		    |texte	    |**Oui**   |L’ID de la transaction. Obligatoire pour une action « purchase » où « refund »|
|**affiliation**|texte      |Non		|La boutique ou la filiale à partir duquel cette transaction a eu lieu.|
|**revenue**	|nombre     |Non        |Spécifie le montant total TTC de la transaction.|
|**shipping**	|nombre     |Non		|Spécifie le montant TTC du transport.|
|**tax**		|nombre	    |Non		|TVA incluant la TVA sur le transport.|
|**currency**	|devise	    |Non		|Devise ISO 4217 (wikipedia.org/wiki/ISO_4217)|
|**coupon**		|texte	    |Non		|Le coupon lié à la transaction |
|**list**		|texte	    |Non		|La liste à laquelle les produits sont associés. |
|**step**	    |entier	    |Non		|Un entier représentant une étape lors du processus de passage en caisse.  Utilisé avec l'action "checkout". |
|**option**		|texte	    |Non		|champ supplémentaire pour les actions « checkout » et checkout_option. |
|**revenue_tax**  |nombre	|Non		|TVA sur le montant de la transaction| 
|**shipping_tax** |nombre	|Non		|TVA sur le montant du transport|
|**revenue_net**  |nombre	|Non		|Montant HT de la transaction|
|**shipping_net** |nombre	|Non		|Montant HT du transport|

### Les actions

Une action spécifie la commande à effectuer sur les données des produits définis préalablement. 

|Action         |Description                                     |
|:--------------|:-----------------------------------------------|
|**click**     |Un clic sur un produit.                         |
|**detail**    |Une vue en détail du produit.                   |
|**add**       |Ajouter un ou plusieurs produits à un panier    |
|**remove**    |Supprimer un ou plusieurs produits d'un panier  |
|**checkout**  |Passage en caisse pour un ou plusieurs produits |
|**checkout_option**| 	Envoi d'options pour une étape de paiement donnée |
|**purchase**  |La vente d'un ou plusieurs produits                      |
|**refund**    |Le remboursement d'un ou plusieurs produits              |   


## L’implémentation de l’E-Commerce amélioré

Les sections suivantes décrivent comment implémenter le commerce électronique amélioré sur un site internet avec la bibliothèque analytics.js.

### Envoi de données de commerce électronique améliorées

Les commandes et les données spécifiques au e-commerce amélioré sont intégrées dans analytics.js.  Il est conseillé de les appeler après l’envoie des données relatives à la page. 

### Mesurer les activités du commerce électronique amélioré

Nous allons étudier les différentes mesures disponibles à travers l’E-commerce amélioré.

* Mesurer les impressions des produits.
* Mesurer les actions.
* Combiner les impressions et les actions.
* Mesurer les transactions.
* Mesurer les remboursements.
* Mesurer le processus de paiement

### Mesurer les impressions des produits

Les impressions des produits sont mesurées en utilisant la commande ==ec:addImpression==. Les données de l’impression sont envoyées via un objet javascript. L’objet doit avoir un nom *name* et une *id*, les autres valeurs sont facultatives.

```javascript
aa('ec:addImpression', {                 // Impression d'un produit.
  'id': 'P12345',                        // ID du produit (chaine).
  'name': 'Android Smartphone',          // Nom du produit (chaine).
  'category': 'High-tech/smartphones',   // Categorie du produit (chaine).
  'brand': 'Samsung',                    // Le constructeur (chaine).
  'variant': 'Black',                    // La variante du produit (chaine).
  'list': 'Search Results',              // Le nom de la liste (chaine).
  'position': 1,                         // La position dans la liste (entier).
 });
```

### Mesurer les actions

La première étape consiste à ajouter le produit à l’aide de la commande ==ec:addProduct== suivit des données du produit. 

La seconde étape consiste à spécifier l’action à exécuter avec la commande ==ec:setAction==.

```javascript
aa('ec:addProduct', {                   // Ajoute le produit.
  'id': 'P12345',                       // ID du produit (chaine).
  'name': 'Android Smartphone',         // Nom du produit (chaine).
  'category': 'High-tech/smartphones',  // Categorie du produit (chaine).
  'brand': 'Samsung',                   // Le constructeur (chaine).
  'variant': 'Black',                   // La variante du produit (chaine).
  'position': 1,                        // La position du produit dans la liste (nombre).
 
});

aa('ec:setAction', 'click', {       // Clic action.
  'list': 'Search Results'          // Le nom de la liste (chaine).
});
```

### Combiner impressions et action

Dans les cas où vous avez à la fois des impressions de produit et une action, il est possible de les combiner.

```javascript

// Impression d'un produit de la liste "produits semblables"

aa('ec:addImpression', {                // Impression d'un produit.
  'id': 'P12345',                       // ID du produit (chaine).
  'name': 'Android Smartphone',         // Nom du produit (chaine).
  'category': 'High-tech/smartphones',  // Categorie du produit (chaine).
  'brand': 'Samsung',                   // Le constructeur (chaine)
  'variant': 'Black',                   // La variante du produit (chaine).
  'list': 'produits semblables',        // Le nom de la liste (chaine).
  'position': 1                         // La position dans la liste (nombre).
});

// La fiche du produit est vue.

aa('ec:addProduct', {                 // Ajoute le produit.
  'id': 'P67890',                     // Produit ID.
  'name': 'Organic T-Shirt',          // Nom du produit.
  'category': 'Apparel/T-Shirts',     // Catégorie.
  'brand': 'Levis',                   // Le constructeur.
  'variant': 'gray',                  // La variante.
  'position': 2                       // La position dans la liste.
});
aa('ec:setAction', 'detail');         // Detail action.
```

### Définir plusieurs produits

Si plusieurs produits ont été définis, l’action s’appliquera à tous les produits.

```javascript
// Le premier produit 

aa('ec:addProduct', {                 // Ajoute le produit.
  'id': 'P67890',                     // ID du produit (chaine).
  'name': 'AFS T-Shirt',              // Nom du produit (chaine).
  'category': 'Apparel/T-Shirts',     // Categorie du produit (chaine).
  'brand': 'AFS',                     // Le constructeur (chaine).
  'variant': 'gray',                  // La variante du produit (chaine).
  'price': '22'                       // Le tarif du produit.
});

// le second produit 

aa('ec:addProduct', {                
  'id': 'P47891',                    
  'name': 'AFS Hat',  
  'category': 'Apparel/Hat/',     
  'brand': 'AFS',
  'variant': 'black',             
  'price': ’48.50’                
});

// le troisième produit

aa('ec:addProduct', {                
  'id': 'P47892',                    
  'name': 'Datasense T-Shirt',  
  'category': 'Apparel/T-Shirts',  
  'brand': 'Datasense',            
  'variant': 'white',              
  'price': '18.50'
});

aa('ec:setAction', 'detail');       // Detail action.
```

### Combiner plusieurs actions

Une fois la commande action exécutée, la liste des produits est vidée. Toutefois il existe l'option ==clear== qui permet de combiner plusieurs actions sans redéfinir à chaque fois les produits.

L’option ==clear== avec la valeur ==no== permet de désactiver la suppression de la liste après l'exécution de la commande action.
  
```javascript
// Ajout du produit 

aa('ec:addProduct', {                 
  'id': 'P47892',                    
  'name': 'Datasense T-Shirt',  
  'category': 'Apparel/T-Shirts',  
  'brand': 'Datasense',            
  'variant': 'white',              
  'price': '18.50'  
});

aa("ec:SetOption", { "clear": "no"}); // Ne pas effacer la liste des produits
aa('ec:setAction', 'detail');         // Produit vu 
aa('ec:setAction', 'add');           //  Produit ajouté au panier.
```

### Mesurer les transactions

L’action ==purchase== est utilisé avec la commande ==ec:setAction== pour définir un achat. Le troisièmes paramètre et un objet contenant les données de la transaction et doit avoir une valeur id. Toutes les autres valeurs sont facultatives.

```javascript
aa('ec:addProduct', {                   // Ajout du produit
  'id': 'P860605',                      // ID du produit (chaine).
  'name': 'iPhone 11',                  // Nom du produit (chaine).
  'category': 'High-tech/smartphones',  // Catégorie du produit (chaine).
  'brand': 'AFS',                       // Variante (chaine).
  'price': '29.20',                     // Prix du produit (nombre).
  'coupon': 'APPARELSALE',              // Coupon attaché au produit (chaine).
  'quantity': 1                         // Quantité (nombre).
});

aa('ec:setAction', 'purchase', {          // Action achat.
  'id': 'T12345',                         // ID de la Transaction *obligatoire (chaine)
  'affiliation': 'My Store',              // Nom de la filiale (chaine).
  'revenue': '37.39',                     // Revenue TTC (nombre).
  'tax': '2.85',                          // TVA (nombre).
  'shipping': '5.34',                     // Shipping (nombre).
  'coupon': 'SUMMER2013'                  // Transaction coupon (chaine).
});
```

### Mesurer les remboursements

Pour le remboursement d’une transaction en totalité, on envoie une action ==refund== avec l'ID de transaction. Si la transaction n’existe pas, le remboursement sera ignoré.

```javascript
// Remboursement d'une transaction.
aa('ec:setAction', 'refund', {
  'id': 'T12345'    // L'ID de la transaction est obligatoire pour le remboursement complet.
});
```

Pour un remboursement partiel, on spécifie l'ID de transaction puis à l’aide de ==addProduct== l'ID de produit et les quantités de produit à rembourser.

```javascript
// Remboursement d'un produit.
aa('ec:addProduct', {
  'id': 'P12345',       // L'ID du produit est obligatoire pour un rempboursement partiel.
  'quantity': 1         // La quantité est obligatoire. 
});

ga('ec:setAction', 'refund', {
  'id': 'T12345',       // L'ID de la transaction est obligatoire.
});
```

## Le tunnel de vente

Pour mesurer chaque étape d'un tunnel de vente, vous devez :

1.  Ajouter du code spécifique à chaque étape.
2.  Si nécessaire, ajouter du code pour définir les options.
3.  Définir les étiquettes pour chaque étape dans les paramètres du tunnel de conversion sur AFS Analytics.

### Mesurer les étapes

A chaque étape du tunnel, vous devrez implémenter un code spécifique pour envoyer les données à AFS Analytics.

#### La variable "Step" spécifie le numéro l’étape

A chaque progression du visiteur dans le tunnel, vous devez spécifier une valeur d'étape. Cette valeur représente le numéro de l’étape que vous avez configurée dans les paramètres du tunnel de conversion.

#### La variable "option"

Si vous devez spécifier une information supplémentaire pour l'étape, vous pouvez utiliser le champ ==option==. Par exemple, pour l’étape *"information sur le paiement"*, la méthode de paiement peut être spécifiée : *"Visa"*.

#### Mesurer une étape

Utilisez ==ec:addProduct== pour  définir chaque produit puis ==ec:setAction== comme action suivi du numéro de l’étape avec le champ ==step== et le champ ==option== pour l’option si nécessaire.

L'exemple suivant montre comment envoyer les données à analytics.js lors du choix de la méthode de paiement.

Le tunnel de vente est le suivant :

1. Ajout du produit dans le panier	
2. Validation du panier par l'acheteur
3. Collecte des données du paiement
4. Collecte des informations sur le transport
5. Validation de la commande et du paiement


```javascript
aa('ec:addProduct', {               // Ajout du produit.
  'id': 'P12345',                   // Product ID (string).
  'name': 'Warhol T-Shirt',         // Product name (string).
  'category': 'Apparel',            // Product category (string).
  'brand': 'Google',                // Product brand (string).
  'variant': 'black',               // Product variant (string).
  'price': '29.20',                 // Product price (number).
  'quantity': 1                     // Product quantity (number).
});

// Ajout du numéro de l'étape et de l'option attachée.
aa('ec:setAction','checkout', {
    'step': 3,
    'option': 'Visa'
});
```

#### L’action "checkout_option"

L’action ==checkout_option== vous permet de d’ajouter des informations supplémentaires sur une étape déjà envoyée.  Par exemple, dans le cas où une information deviendrait seulement disponible après avoir envoyé l’action ==checkout==.

```javascript
// L’action checkout a été envoyée sans spécifier le moyen de paiement 
aa('ec:setAction', 'checkout_option', {'step': 3, 'option': 'PAYPAL'});
```

#### Configurer le tunnel de vente

Chaque étape du tunnel de vente peut recevoir un nom descriptif qui sera utilisé dans vos rapports. Pour configurer ces noms, sélectionnez le menu "ecommerce enhanced  -> funnel settings" sur la page du tableau de bord.


## Les Options liées à l’E-commerce amélioré 

Présentation des différentes options de l'E-commerce amélioré.


### L’option "currencyCode"

Cette option définit la devise par default utilisée par le site d’E-Commerce.

```javascript
aa("ec:SetOption", { "currencyCode": "USD"});
```

!!! note 
Vous pouvez également définir la devise du compte avec l’option standard.

```javascript
aa('set', 'currencyCode', 'EUR'); // Défini l'Euro comme devise principale.
```
 

### L’option "clear"

Cette option permet de définir si la liste des produits ajoutés avec ==addProduct== doit être réinitialisée après l’exécution de l’action.  Par défaut l’option est réglée sur "yes"

```javascript
aa("ec:SetOption", { "clear": "no"}); // La liste n’est pas réinitialisée 
aa("ec:SetOption", { "clear": "yes"}); // La liste est réinitialisée 
```

### L’option "beacon"

L'option Beacon permet de forcer l’envoi de la commande "action" via l’[API Beacon](https://developer.mozilla.org/en-US/docs/Web/API/Beacon_API).  Cette option est nécessaire si l’envoi de la commande "action" est déclenchée lors du déchargement de la page.  

```javascript
aa("ec:SetOption", { "beacon": "enabled"}); // Force l’envoi via l’api beacon
aa("ec:SetOption", { "beacon": "disabled"}); // Envoi via XMLHttpRequest
```

## Example Complet

Les extraits de code, ci-dessous montrent les différentes étapes de mesure avec l’e-commerce amélioré sur un produit.

### Impression du produit

```javascript
//xxxxxxxx est l'id de votre site internet.

aa("create", "xxxxxxxx", "auto") 

aa('ec:addImpression', {
  'id': 'P12345',                   
  'name': "NoteBook",
  'category': 'high-tech/notebook/',
  'brand': 'IBM',
  'variant': 'black',
  'list': 'Search Results',
  'position': 1                    
});

aa('send', 'pageview');              
```

### Clic sur le produit

Ensuite, l'acheteur potentiel clique sur le produit pour obtenir sa fiche détaillée.

```javascript
// Fonction à appeler lors du clic.

function onProductClick() {
  aa('ec:addProduct', {
  'id': 'P12345',
  'name': "NoteBook",
  'category': 'high-tech/notebook/',
  'brand': 'IBM',
  'variant': 'black',
  'position': 1,
  "price": "399"
  });
  aa("ec:SetOption", { "beacon": "enabled"}); // Pour s'assurer que les informations soient envoyées si le client quitte la page.
  aa('ec:setAction', 'click', {list: 'Search Results'});
}
```

Sur la fiche détaillée:

```javascript
  //xxxxxxxx est l'id de votre site internet.
aa("create", "xxxxxxxx", "auto")

aa('send', 'pageview');          
aa('ec:addProduct', {
  'id': 'P12345',
  'name': "NoteBook",
  'category': 'high-tech/notebook/',
  'brand': 'IBM',
  'variant': 'black',
  "price": "399"
  });
  aa('ec:setAction', 'detail');

```

### Clic sur le bouton "Ajouter dans le panier" sur la fiche du prduit

```javascript
// Appelé lorsque le visiteur clic sur le produit. Product est un objet contenant les caractéristique du produit.

function addToCart(product) {
  aa('ec:addProduct', {
    'id': product.id,
    'name': product.name,
    'category': product.category,
    'brand': product.brand,
    'variant': product.variant,
    'price': product.price,
    'quantity': product.qty
  });
  aa("ec:SetOption", { "beacon": "enabled"}); // Seulement si la pression du bouton entraine le chargement d'une nouvelle page.
  aa("ec:SetOption", { "clear": "no"});  // On envoie 2 actions, donc on doit désactivé l'effacement du produit.
  aa('ec:setAction', 'add'); // Ajout dans le panier
  aa("ec:SetOption", { "clear": "yes"}); // On active l'effacement du produit apres l'exécution de la commande "checkout".
  aa('ec:setAction','checkout', {'step': 1}); // C'est la premiere étape du tunnel de vente.
  // Seulement si autotrack est OFF
  aa("send", "event", "click", "inside", "Add To Cart" + product.name);
}


```

Le bouton "Ajouter dans le panier" (HTML)

```html
<button onclick='addToCart({id:"P12345", name: "NoteBook",category:"high-tech/notebook/",brand:"IBM",variant: "black",price:"399", quantity:1})' data-aa-label="Ajout de NoteBook dans le panier">Ajouter dans le panier</button>
```

### Validation du panier par l'acheteur (cart.html) 

```javascript
/**
 * Cette fontion est appelée lorsque l'utilisateur a validé son panier d'achat.
 * @param {Array} cart Tableau contenant le panier du visiteur.
 */

function checkout(cart) 
{
  // Nécessaire au cas ou l'utilisateur quitte la page 
  aa("ec:SetOption", { "beacon": "enabled"});
	
  // Obtenir les produits contenus dans le panier
  for(var i = 0; i < cart.length; i++) {
    var product = cart[i];
    aa('ec:addProduct', {
      'id': product.id,
      'name': product.name,
      'category': product.category,
      'brand': product.brand,
      'variant':  product.variant,
      'price': product.price,
      'quantity': product.qty
    });
  }

  aa('ec:setAction','checkout', {
    'step': '2'            // La valeur 2 indique l'étape du passage en caisse.
    });

}

aa("create", "xxxxxxxx", "auto")  //xxxxxxxx est l'id de votre site internet.
aa('send', 'pageview');    

```

### Page du paiement (payment.html) 

```javascript
/**
  * Fonction appelée lorsque le visiteur valide le paiement
  * @param {Array} cart Tableau contenant le panier du visiteur.
 */
function checkout(cart,option,step) {
  for(var i = 0; i < cart.length; i++) {
    var product = cart[i];
    aa('ec:addProduct', {
      'id': product.id,
      'name': product.name,
      'category': product.category,
      'brand': product.brand,
      'variant':  product.variant,
      'price': product.price,
      'quantity': product.qty
    });
  }

  aa("ec:SetOption", { "beacon": "enabled"}); // Si risque de chargement d'une nouvelle page.
  aa('ec:setAction','checkout', {
    'step': step,            // Etape 3 page paiement
    'option': option      // Méthode de paiement.
    });

}

aa("create", "xxxxxxxx", "auto")  //xxxxxxxx est l'id de votre site internet.
aa('send', 'pageview');     

// Appel de la fonction lorsque que le formulaire est validé.
checkout(cart,"visa",3);

```

### Choix du transporteur (shipping.html) 

```javascript
/**
  * Fonction appelée lorsque le visiteur valide le paiement
  * @param {Array} cart Tableau contenant le panier du visiteur.
 */
function checkout(cart,option,step) {
  for(var i = 0; i < cart.length; i++) {
    var product = cart[i];
    aa('ec:addProduct', {
      'id': product.id,
      'name': product.name,
      'category': product.category,
      'brand': product.brand,
      'variant':  product.variant,
      'price': product.price,
      'quantity': product.qty
    });
  }

  aa("ec:SetOption", { "beacon": "enabled"}); // Si risque de chargement d'une nouvelle page.
  aa('ec:setAction','checkout', {
    'step': step,            // Etape 4 page paiement
    'option': option      // Méthode de paiement.
    });

}

aa("create", "xxxxxxxx", "auto")  //xxxxxxxx est l'id de votre site internet.
aa('send', 'pageview');     

// Appel de la fonction lorsque que le formulaire est validé.
checkout(cart,"fedex",4);
```


### Commande acceptée et payée, page de remerciements (thanks.html)

```javascript
 for(var i = 0; i < cart.length; i++) {
    var product = cart[i];
    aa('ec:addProduct', {
      'id': product.id,
      'name': product.name,
      'category': product.category,
      'brand': product.brand,
      'variant':  product.variant,
      'price': product.price,
      'quantity': product.qty
    });
 }

  aa("create", "xxxxxxxx", "auto")  //xxxxxxxx est l'id de votre site internet.
  aa('send', 'pageview');     
  
  // Ne pas effacer aprés l'exécution de la commande purchase
  aa("ec:SetOption", { "clear": "no"}); 
  // Envoi de la transaction
  aa('ec:setAction', 'purchase', {
  'id': 'T12345',
  'affiliation': 'My Online Store',
  'revenue': '318.25',
  'tax': '68.50',
  'shipping': '15.34',
  'coupon': 'SUMMER2020'    // Le client a utilisé un coupon.
  });

  // Dernière étape du passage en caisse. Vente réussie.
  aa('ec:setAction','checkout', {
    'step': 5,            // Etape 5 vente réussie 
    });
```

