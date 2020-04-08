hero: Getting and Setting tracker data
title: Getting and Setting tracker data
description: Getting and Setting tracker data



#Getting and Setting tracker data

AFS's analytics.js library allows you to interact with the trackers, which is to say to get or set the data stored by them. In order to do this, two commands are available: 

- ==GET== is used to obtain the data.
- ==SET== to define or modify data. 


## The Get command

Since the calls to the *aa()* function are saved in a queue and the download of analytics.js is done asynchronously, it is necessary to get confirmation that the tracker has been successfully created  before being able to access its data with the command get. 

To do this you can: 

1. Define a callback function when creating the tracker with the ==create== command -- see [Creating trackers](../creating-trackers/).
2. Or call the ==Ready callback== function after the tracker has been created.

### Ready Callback function

Ready Callback is a function that you define by calling the aa() function. As all waitlist commands are executed in order, this function will be executed after the tracker is created. Ready Callback returns the tracker object. 

!!! note 
    The Ready Callback function can also be called after sending the send command, you will then have access to the data sent by the AFS servers, such as the visitor ID. 

The following code shows access to the default tracker object using Ready Callback function :
```js
aa('create', 'XXXXXXXX', 'auto');	

/* adding the ready callback function */
aa(function(tracker) {

/* Display the default tracker data on the console. */
console.log(tracker);
});
``` 

### Access a tracker by name

If you use multiple trackers, you can access a specific tracker by using the getByName() function. 

```js
getByName('name');
```
The GetByName() function returns the tracker object with the specified name. If the name field is empty, the default tracker will be returned. 

```js
aa('create', 'XXXXXXXX', 'auto', 'mytracker');
aa(function() {
  /* displays data from the tracker called 'mytracker'. */
  console.log(aa.getByName('mytracker'));
});
```

### Getting a list of all trackers

The function getAll() returns an array containing the list of all the trackers (objects) created. 

```js
aa('create', 'XXXXXXXX', 'auto');
aa('create', 'YYYYYYYY', 'auto', 'mytracker');
aa(function() {
  // displays a table containing all the trackers
    console.log(aa.getAll());
});
```

### Getting tracker data using the GET command

Tracker data can be obtained using the get command. 

```js
aa('create', 'XXXXXXXX', 'auto');
aa(function(tracker) {
  // display the name and reference of the tracker.
    console.log(tracker.get('name'));
    console.log(tracker.get('referrer'));   
});
```

Using getByName(): 
```js
aa('create', 'XXXXXXXX', 'auto','mytracker');
aa(function() {
    /* displays data from the “mytracker“ tracker. */
    var tracker=aa.getByName("mytracker");
    console.log(tracker.get('name'));
    console.log(tracker.get('referrer'));   
});
```

## Updating tracker data with SET command

Ttracker data can be changed or updated via the ==set== command. The command can be linked to a tracker name or sent alone. 
The set command is sent via the function aa(). Arguments can be defined in two distinct ways: 

1. Two parameters: the first specifies the field to be modified and the second, the replacement value.
2. By an object.

Changing the default tracker title: 
```js
aa('set','title','Home page') ;
```

Changing the tracker's URL and title through an object:
```js
aa('set ',{
  title :'Home Page',
  location:'https://www.afsanalytics.com'
});
```

### Updating a tracker using its name

You can set a tracker variable by using its name. 

```js
aa('mytracker.set','title','About Us');
```

Use the get command directly on the tracker object 

```js
aa(function() {
    /* displays data from the tracker named mytracker */
    var tracker=aa.getByName("mytracker")
    tracker.set("title","About");
    console.log(tracker.get('name'));
    console.log(tracker.get('title'));  
})
```