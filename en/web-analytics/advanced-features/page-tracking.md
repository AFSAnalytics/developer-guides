hero: Page Tracking
title: Page Tracking
description: Page tracking allows you to measure the number of views and the time spent by your visitors on each page.

# Page Tracking

Page tracking allows you to measure the number of views and the time spent by your visitors on each page. 
This guide will explain how to use the analytics.js library for page tracking 
and how to send the data to AFS Analytics [web analytics solution](https://www.afsanalytics.com/). 

## The Send command for page tracking

When creating the tracker, several fields are defined by the data provided in the document. 
For example, the *title* field is specified in the *&lt;title&gt;* tag and the URL is the page address. 

Once the data has been collected, it can be changed using the set command,
and some of them can be replaced directly in the sending command. 
Sending the data is done with the command ==send== using the following syntax: 

```js
aa("send","pageview",[page],[title],[location] ,[hitCallback],[params]) 
```

Only the hitType field is required. It should indicate pageview as the type of call. 

##### Optional fields: 

| Field | Description
| --- | ---
|Page| indicates the index used by AFS Analytics to sort the pages. You can use your own indexing method or use a predefined method like autoindex , titleindex , urlindex , pageindex .
|Title| specifies the name or title of the page.
|Location| address (URL) of the page.
|HitCallback| defines the callback function. This function will be called after the page is sent to the AFS Analytics server. The value can be a function, or a string with the name of the function.
|Params| object containing your own recoverable variables in the return function.

!!! note 
    If a field has an empty string, the default or previously stored value will be used. 



### Examples

Without any parameter: 
```js
aa("send","pageview");
```

Defining the page title (note the empty string for the "page" field) :
```js
aa("send","pageview","","my title");
```
 
Ddefining a return function (note the empty strings for "page" and "url" arguments) : 
```js
aa("send","pageview","","my  title","","mycallback"); 
```


Fields can also be specified in an object. You are free to choose the fields to be filled in. Only the *hitType* field is required. 

Define the fields as an object:
```js
aa("send",{
hitType :"pageview",
page : "titleindex",
title : "my page",
location : "https://mysite.com",
hitCallback : "mycallback",
}) ;
```

###Simplifying the page URL

If the URL of the page contains in the query string or in the anchor part of the parameters of advertising campaigns, AFS will detach them and treat them with the sending of the page. Analytics.js also offers an allowAnchor parameter, which allows you to save or ignore the query string and the anchor part of the URL when it is transmitted. 

This command to be placed after the tracker is created asks AFS to ignore additives to the URL. 
```js
aa("set","allowAnchor","false") ; // we can change false by0 ;
```

!!! note
    ==allowAnchor== is set to false by default when creating the tracker. 

### Using the callback function

Please refer to [Sending data](../sending-data/) for a detailed explanation. 

The callback function is called after the page is sent to AFS Analytics. It returns three parameters: 

1. The hitType of the command executed.
2. The tracker object.
3. The params object defined in the calling function.

Example using the return function: 
```js
 /* custop object */

var myobject={
    message:"the page viewed has been sent to AFS Analytics",
    pagevue:document.title,
    location:window.location.href
};

/* custom callback function */

function mycallback(command,tracker,obj)
{
        console.log("Tracker data has been sent to AFS Analytics!");
        console.log("The command was ->",command);
        console.log("The page was ->",obj.pagevue,"The url->",obj.location);
        console.log ("The unique ID of the visitor sent to AFS is->",tracker.get("visitor.id"));
        console.log ("The tracker is called ->",tracker.get("name"));
        console.log ("The visitor’s cookie ->",tracker.get("cookie.str"));
        console.log(tracker);
}

/* calling analytics.js */

aa("create", "00000003", "auto");
aa("send", "pageview","autoindex","Test Page","","mycallback",myobject);
```

Console output: 
```sh
Tracker data has been sent to AFS Analytics!
The command was -> pageview
The page was -> Test callback 
The url-> http://127.0.0.1/tc.html
The unique ID of the visitor sent to AFS is -> 31
The tracker is called -> afstracker0
The visitor’s cookie -> 3x6226x1191x31x6103x1
```

### Sending Page View through "AutoTrack"
In sites with a single page, access to the different sections 
is usually defined using an anchor. 
To capture the visualization of these sections as pages, you will have to 

1. Set the index with the titleindex value. Reference the page sections with different names.
2. Use:
Either the Autotrack option:
The "Autotrack" option allows you to define specific events to be executed when clicking on a link. To do this, we set the data in the datasets : 
```html
<a href="#contact-us"
 data-aa-hitType="pageview"  
 data-aa-title="contact-us">
    contact-us
</a>
```
On each click, the "contact-us" page will be sent by anlytics.js to AFS Analytics. 
Or set your own function and call it with *onclick* .
Use the *onclick* option coupled with an AFS Analytics calling feature.
```js
 function SendPV(name) {
  aa("send","pageview","titleindex",name);  
  return true;
}
<a href="#contact-us" onclick="return sendPV("contact us");">Contact Us!</a>
```
