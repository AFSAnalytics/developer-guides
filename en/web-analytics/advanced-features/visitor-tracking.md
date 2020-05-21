hero: Sending visitor data
title: Sending visitor data
description: send or share data about your website users.


# Sending visitor data

Analytics.js allows you to send or share data about your website users. For example, when a visitor fills a form or logs in, the collected data can be sent to AFS Analytics. These will be attached to the user's profile and will appear on each of his visits. 
Sending data to AFS Analytics requires two steps: 

1. Data storage by analytics.js
    
    Storage is done via the command ==set== followed by the key visitor

2. Sending data to server

    Transmission to the server is done through the command ==send== followed by the key visitor. 


!!! note
    If the AFS Analytics WordPress plugin is installed on your website, the data will be automatically sent when users log in. These features are only available with the Silver and Gold plans. 

## Data Storage

The ==set== command is used to store visitor data. It accepts object or string indicating witch variable to set. 

Syntax: 
```js
aa("set","visitor",[object])

/* Or */
aa("set","visitor.[variable]",[value])
```

Example: 
```js
aa("set","visitor",{firstname:"christophe";lastname:"Durand"};

/* Which is the equivalent to */
aa("set","visitor.firstname","Christophe");
aa("set","visitor.lastname","Durand");
```

### Accepted fields

!!! note 
    All following fields are optional. 

| Field | Description
| --- | ---
|job| "create" for profile creation. "update" for profile update. "delete" for profile deletion. By default, it is set to update mode. The "create" mode saves the data only if it’s a new user. The "update" mode updates the data or creates the profile if it does not exist. The "delete" mode deletes the user's profile. 
|logged| visitor has logged-in to the website. Value must be 1 or greater.
|afsid| visitor unique identifier ( created by AFS Analytics ). By default, this is the current visitor id
|yourid| your own visitor unique identifier
|username| username used for the login
|displayedname| name to display on the visitor list. By default, the username is displayed
|role| user role as a string ( for example: administrator, member, etc.) It's up to you to define it
|firstname| user first name
|listname| user last name
|company| company name
|address| address line 1
|addressplus| address line 2
|city| city
|tate| state or region
|country| country
|zipcode| postal code
|email| email
|phone| phone number
|sms| mobile/sms phone number
|birthday| birthay date (format: yyyy-mm-dd)
|gender| M for men, F for women
|photourl| URL of the user profile picture (https only)
|yournote| custom note about the user
|yoururl| custom lin related to the visitor
|followlist| list(s) attached to the user. This can be the numeric identifier of the list, or the name of the list. If there are multiple lists, they must be separated by a comma. You can create the lists, or find their identifier displayed in the visitor profile box
|addtolist| Set to "yes" if followlist value should be added to previous lists, or to "no" if it should replace them. Default value: "no".


## Sending data 
The data transmission is done with the ==send== command. Once the data sent, all field values are reseted. 

Syntax: 
```js
aa("send","visitor");
```

For example: 
```js
var data = {
  job : "update";
  firstname : "Christophe";
  lastname : "Durand";
  username : "chris277";
  displayedname : "The Boss";
  birthday : "1989-12-31";
  photourl : "https://www.afsanalytics.com/images2/profile/demo.png";
  role : "Administrator";
  followlist : "Developer team, support";
};

aa("set","visitor",data); //set visitor data
aa("create", "xxxxxxxx", "auto"); 
aa("send", "pageview");
aa("send","visitor");
```

### Visitor logins 

By way of exception, when a visitor logs in, the Send visitor command is not required after the setting of the logged variable (visitor.logged), if the variable is defined before the line sending page data. 

For example: 
```js
aa("create", "xxxxxxxx", "auto"); 
aa("set","visitor.logged",1); //not needed to add a send visitor line.
aa("send","pageview");
```