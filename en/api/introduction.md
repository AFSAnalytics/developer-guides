hero: AFS Analytics API
title: AFS Analytics API
description: Mastering AFS Analytics API



# AFS Analytics API

##  Introduction
    
We currently offer a REST API wich allow you to retrieve various information
such as your account information, traffic and eCommerce metrics for a specified period of time.


An interactive API documentation is available [here](reference.md) that will allow you
to visualize and test the different endpoints available.

## Current Version

Current API version is  ==1.0.0==

| Version | URL
| --- | ---
| 1.0.0 | [https://api.afsanalytics.com/v1/](https://api.afsanalytics.com/v1/)

    


## Authorisation

Two different authentification methods are currently supported:

### API Key

This is the authentification method to use when you want to access one of  your account data.

API Keys for existing accounts can be created [here](https://dev.afsanalytics.com/manage/api/keys).
    
!!! note
    An API Key will only allow access to the account specified when the key was created. If you own several account, you will need to create an API key for each account you will want to access via the API. 

### OAUTH2 Identification

When developping Apps or Plugins you will need to identify your client via 
OAUTH2 protocol.

| URL Type | URL
| --- |---
| Authorization | https://dev.afsanalytics.com/api/authorize
| Token | https://dev.afsanalytics.com/api/token/
    
The interactive creation of Cliend ID/Secret is currently not supported. To request
those please do not hesitate to contact us via email at [api@afsanalytics.com](mailto:api@afsanalytics.com)



## OpenAPI Specification

A JSON File describing our API via the OpenAPI V3.0 Specification is available 
at the following URL [/assets/openapi/v1/afsa.json](https://dev.afsanalytics/assets/openapi/v1/afsa.json).

You can use this file to quickly generate API Clients for different langages via external tools like 
[Swagger Tools](https://swagger.io)

API usage reference for Clients generated with Our OpenAPI File can be found [here](../swagger/sdk/).


## Contact and Requests

Please direct any question or request to [api@afsanalytics.com](mailto:api@afsanalytics.com)

