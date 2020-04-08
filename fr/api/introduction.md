lng: fr
hero: AFS Analytics API
title: AFS Analytics API
description: Mastering AFS Analytics API



# AFS Analytics API

##  Introduction
    
AFS Analytics met à votre disposition une API *REST*  vous permettant d'accéder 
à différentes données telles que les paramètres de votre compte, les mesures
de trafic et de performances eCommerce sur une période de temps personnalisable.

Une documentation interactive de cette API est disponible [ici](reference.md). 
Celle-ci vous permettra de visualiser et de tester les différentes fonctions disponibles.


## Version

La version actuelle de l'API AFS Analytics est:  ==1.0.0==

| Version | URL
| --- | ---
| 1.0.0 | [https://api.afsanalytics.com/v1/](https://api.afsanalytics.com/v1/)

    


## Identification

Deux modes d'identification sont actuellement supportés:

### Clef API

C'est la méthode à utiliser lorsque vous souhaitez accéder aux informations d'un
de vos comptes.

Vous pouvez créer une clef API [ici](https://dev.afsanalytics.com/manage/api/keys).

    
!!! note
    Une clef API ne permet d'accéder qu'au seul compte spécifié au cours de sa création. Si vous possédez différents comptes, vous devez créer une clef pour chacun des comptes auxquels vous désirez accéder. 

### Identification OAUTH2

Lorsque vous développez  une application, un module ou un service, 
vous devez identifier votre client via le protocole OAUTH2.

| URL Type | URL
| --- |---
| Autorisation | https://dev.afsanalytics.com/api/authorize
| Token | https://dev.afsanalytics.com/api/token/
    
!!! warning 
    La création interactive d'une ID/Clef Client n'est actuellement pas supportée. Afin d'obtenir celles-ci, n'hésitez pas à nous contacter via EMail [api@afsanalytics.com](mailto:api@afsanalytics.com)



## Spécification OpenAPI 

Un fichier JSON  décrivant l'API AFS Analytics 
via la spécification OpenAPI V3.0 est disponible 
à l'URL suivante: [/assets/openapi/v1/afsa.json](https://dev.afsanalytics/assets/openapi/v1/afsa.json).

Ce fichier peut être utilisé afin de générer automatiquement 
des clients pour différents langages grâce à des outils comme [Swagger Tools](https://swagger.io)

Une documentation générique pour les clients générés de cette façon est disponible [ici](../sdk/reference/).


## Contact et Renseignements

Merci d'adresser toute demande / question à [api@afsanalytics.com](mailto:api@afsanalytics.com)

