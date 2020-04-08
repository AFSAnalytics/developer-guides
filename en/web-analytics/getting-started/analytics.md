hero: Analytics.js overview
title: Analytics.js overview
description: All calls to the Analytics.js library are done exclusively via the aa() function. This document explains the use and role of this function. 

# Analytics.js overview

All calls to the Analytics.js library are done exclusively via the ==aa()== function. This document explains the use and role of this 
function. 

!!! note
 	The aa() global function name can be changed inside the tracking code. The same name must be used to communicate with analytics.js. 

!!! tip
	AFS analytics.js uses the same structure as Google Analytics in order to simplify its use for former GA users. 

## The command queue

The aa() function stores in a queue all commands sent to analytics.js prior to its downloading. Once analytics.js is loaded, the pending commands are executed and the list flushed. At this point new commands can be sent to the queue. 

## Inspecting queued commands

All calls to aa() are saved in the *aa.q* array. To view the contents of the queue before the loading of the library, you can display the q array: 

```js
console.log(aa.q);
/*
Outputs (q array):
[
   ['create', 'XXXXXXXX', 'auto'],
   ['send', 'pageview']
]
*/
```


## Why use a queue?

The queue allows the use of the aa() function without having to worry about the download status of the library. Also, it ensures operations in asynchronous mode without any loss of data. 

## Adding commands to the queue

All calls to the aa() function share the same structure composed of at least two arguments. The first argument is the command to execute, the scecond one defines the arguments attached to the command. 

So in the call: 

```js
aa('create', 'XXXXXXXX', 'auto'); 
```

==Create== is the command, ==XXXXXXXX== and ==auto== are the arguments attached to this command. 
A tracker name can be defined with the create command. In this case, if there are several trackers, the send and set commands must be preceded by the name of the tracker (followed by a dot) in order to address the tracker. If no name is defined, only the first tracker, named or not, will be affected by the command. 

Example of creating and accessing a named tracker: 

```js
aa('create', 'XXXXXXXX', 'auto', 'mytracker') ;
aa('mytracker.send','pageview') ;
```

!!! note
 	If the aa() function receives an unknown command, it will just ignore it without generating any error message. 

## Command arguments

Arguments related to a command can be sent in several formats to facilitate the transmission of commonly used fields. 

The following example use the *simplied* format: field names do not appear as they are determined based on the position of the field. 

```js
aa('create', 'XXXXXXXX', 'auto');
aa('send', 'pageview','titleindex' , 'home page', 'https://www.mysite.com');
```

The *create* command accepts as arguments a trackingId, CookieDomain, and other optional fields such as name, callback or params. The send command accepts various parameters depending on the send type defined by hitType. For example, for pageview, the fields page, title, location, hitCallback and params can be filled in. AFS Analytics also accepts the url, index, callback fields as an alternative to the location, page and hitCallback fields. 


All commands can accept one or more objects that define the different fields. The previous code could be written this way. 

```js
aa('create', {
	trackingID : 'XXXXXXXX' ,
	cookieDomain : 'auto'
}) ;

aa('send', {
	hitType: 'pageview',
	page: 'titleindex' 
	title :'home page',
	location :'https://www.mysite.com' 
});
```

