hero: Sending data to AFS Analytics
title: Sending data to AFS Analytics
description: Sending data to AFS Analytics


#Sending data

In the JavaScript tracking snippet provided by AFS analytics you may notice, 
located after the command creating the tracker, 
a line adding the ==send== command to the aa() function. 
The send command sends the data previously stored by the tracker to the AFS Analytics server. 
This guide describes how the data is sent to AFS Analytics. 

## Different types of calls or hits

A hit occurs every time a tracker sends data to the AFS Analytics server. 
This is an HTTP request between the library analytics.js and AFS Analytics. 

There are several types of hits: 

| Hit | Data sent
| --- | ---
| Pageview | Page view data
| Event |  data related to an event
| Ecommerce |  sends sale data (ecommerce)
| Visitor | visitor details

Hits are sent via the *send* command or triggered automatically by the *autotrack* option. 

## The SEND command
The syntax of the *send* command via the *aa()* function is as follows: 

```js
aa("send", "hitType" ,[fieldslist] , [fildsobject]) ;
```

As the fields list depends on the hit type hitType setting, you should consult its dedicated guide to know the exact syntax to use. 
!!! note
    In the rest of this document, we will use the sending of the pageview hitType as an example 


Example: using an object for passing arguments
```js
aa("send", {
  hitType: "pageview",
  page: "titleindex",
  title: "home page",
  location: "https://www.afsanalytics.com"
 });
```
Fields are defined in the object passed as second argument. 


#### Fields description

|type|Action
|---|---
| hitType|  Set the hit type
| page or index (optional)| Defines the indexing mode used by AFS Analytics. Several are available, like autoindex, titleindex, pageindex, urlindex. This field accepts two different names: ==page== and ==index==. The field named ==page== ensures compatibility with Google Analytics. 
| title (optional)|  Sets the page title.
| location or url (optional)| specifies the URL of the page. This field accepts two different names: ==location== ensures compatibility with Google Analytics.


!!! important 
    The current version of AFS ignores the value of the *page or index* field and always uses the page title to build the index. In a future version, this option will be implemented. 




For the sake of simplicity, the values can be passed without the specification of the field name. The position of the argument determines the field. 

The previous example can be written as follows: 
```js
aa("send","pageview","titleindex","homepage","https://www.afsanalytics.com");
```

Please refer to [Parameters accepted by the analytics.js library]() for the complete list of fields. 

## Using a specific tracker

As with the set command, it is possible to specify the tracker name. 

```js
aa("mytracker.send", "pageview","titleindex","home page","https://www.afsanalytics.com");
```
Or using the tracker object:
```js
tracker.send("pageview","titleindex","home page","https://www.afsanalytics.com");
```

## Specify a callback function

The callback function will be called after executing the send command. 
It returns three parameters: 

1. A string containing the hit type: *pageview* , *event* , *transaction* , *visitor* , etc.
2. The tracker object for *pageview* hit.
3. The defined object containing your own variables (params field)

The callback function is defined by the *callback* or *hitCallback* fields. The defined value can be a string containing the name of the function or the function itself. The hitCallback field is located in the fifth position in the argument list of the aa() function if the hitType is pageview . 
The params field is the object containing your own parameters. In the simplified call, this field is placed in sixth position if the call type is pageview . 

In the following example, we create our own object and a callback function. We then call the send command. The mycallback function will be executed after data transmission is complete. 

```js
/* call own object */
var myobject={
    message:"The page view was sent to AFS Analytics",
    pagevue:document.title,
    location:window.location.href
};

/* return function */
function mycallback(commande,tracker,objretour)
{
        console.log("The tracker information was sent to AFS Analytics");
        console.log("The command was ->",commande);
        console.log("The page was ->",objretour.pagevue,"The url->",objretour.location)The unique visitor ID sent by AFS is ->",tracker.get("visitor.id"));
        console.log ("The tracker is named ->",tracker.get("name"));
        console.log ("The visitor cookie ->",tracker.get("cookie.str"));
        console.log(tracker);
}

/* calls to analytics.js */
aa("create", "00000003", "auto");
aa("send", "pageview","autoindex","Test Page","","mycallback",myobject);
```

Console output : 
```sh
The tracker information was sent to AFS Analytics
The page was -> Test callback 
The url-> http://127.0.0.1/tc.html
The unique visitor ID sent by AFS is -> 31
The tracker is named -> afstracker0
The visitor cookie -> 3x6226x1191x31x6103x1
```

The same command using an object: 
```js
aa("send", {
hitType: "pageview", 
page: "autoindex", 
title: "Test Page", 
hitCallback: "mycallback", 
params: myobject });
```

## Plan for a timeout in the event of an error. 

A callback function is very useful for performing tasks after sending the data to AFS Analytics. Unfortunately, if a problem arises, the function may never be called. 

This is why, when important tasks are executed by this function, it is important that you plan an alternative solution. The setTimeout JavaScript function can be useful for checking the execution of the callback function. 