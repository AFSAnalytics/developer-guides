hero: Creating trackers
title: Creating trackers
description: Learn how to create trackers to collects data.



# Creating trackers

A tracker is an object that collects and sends data to AFS Analytics. 

When creating a tracker, the website ID, the storage mode and the domain of the cookies must be specified.
 
## Finding a website ID

The ID of a website consists of 8 digits. It is created when you add a new website to your AFS Analytics profile. To find the ID, select the option Manage websites in the Account menu available on your AFS dashboard. 

## How cookies are stored

AFS Analytics offers several ways to store cookies:

- The auto mode (recommended) creates a cookie attached to the domain and all subdomains of the website.
- The afs mode creates a cookie attached to the afsanalytics.com domain. Known as third-party cookies, this type of cookies is only recommended for sites that do not have their own domain name. Data from third-party cookies can be inacurrate because some browsers disable them to preserve users' privacy.
- The third mode allows you to specify the domain name attached to the cookies. Generally, the domain name of your website. eg ".mysite.com"
- The disabled mode doesn't use/write cookie. This option is not recommended because the returning visitors will no longer be recognized.

### How cookies work

For each new visitor, AFS generates a unique ID and saves it in a cookie. 
This process allows the visitor to be identified on each new visit. 

## Creating trackers with the "create" command

Using the create command creates a new tracker object. 
It is followed by two mandatory parameters: the first is the identification of the site trackingID. 
The second is the name of the domain attached to the cookie, called cookieDomain. This argument also accepts the predefined values auto, afsor disabled. 

```js
aa('create', 'XXXXXXXX', 'auto');
```
!!! note
    When creating a tracker, data is collected such as the title and URL of the page, 
    the referring site, and the configuration used by the visitor. 

## Optional parameters

### Naming a tracker 

You can name a tracker by adding the name parameter in fourth position. 

```js
aa('create', 'XXXXXXXX', 'auto','mytracker');
```

If the ==name== field is not specified, the tracker will be automatically named ==afstracker0==.
The next one created will be named ==afstracker1== and so on. 

### Setting a callback function 

In fifth position you can define the name of a return function, known as the ==callback== function. 
the specified function will be executed after the tracker is created. 

In the sixth position, the parameter ==params== accepts an object that will be sent to your callback function. 

Example of code setting a callback function and a returning object: 
```js
function createcallback(command,t,myobject)
{
        console.log("tracker created!");
        console.log("callback command ->",command);
        console.log ("Tracker object access! Tracker name ->",t.name);
        console.log ("Object return "params" sent by function aa() ->",myobject);
}

aa('create', '00000003', 'auto','mytracker','createcallback',{string:'my parameters'});
```


Console output: 
```sh
tracker created!
Callback type -> 
Tracker object access! Tracker name -> mytracker
Object return "params" sent by function aa() -> 
Object {string: "my parameters"}
```

The callback function returns 3 parameters: 
1. A character string with the command or hitType of the calling function.
2. The tracker object giving you access to all the data stored by the tracker.
3. The return of the object defined with the parameter params in the function aa().

### Passing arguments via an object 

Setting the *create* command parameters can also be done via an object when calling the aa() function. 

```js
aa("create", {
  trackingId: "00000003",
  cookieDomain: "auto",
  name: "myTracker1",
  callback : "createcallback",
  params : {string:"mes parametres"}
});
```

## Creating and working with several trackers

It is possible to create and work with several trackers on the same page. This can be useful when the site belongs to several owners, and each of them wants to get reports on different sections of the site. 
To get two separate reports, you must already have two different IDs and create trackers with different names. 

```js
aa('create', 'XXXXXXXX', 'auto');
aa('create', 'YYYYYYYY', 'auto', 'clientTracker');
```

### Sending information to a specific tracker.

To send information to a specific tracker, its name, followed by a period must be added, before the command to be executed. Remember the default tracker name is afstracker0. 

For example, to send "hitType" ==pageview== to the two trackers defined above: 
```js
aa('afstracker0.send', 'pageview');
aa('clientTracker.send', 'pageview');
```
!!! note 
    ==aa('send', 'pageview');== is equivalent to ==aa('afstracker0.send', 'pageview');==