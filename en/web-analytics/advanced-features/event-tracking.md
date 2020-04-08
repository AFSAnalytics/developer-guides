hero: Events Tracking with AFS Analytics
title: Events Tracking with AFS Analytics
description: Tracking events allows you to measure the interactions between the visitors and the pages of a website.


# Event Tracking with AFS Analytics

Tracking events allows to monitor with more accuracy interactions between the visitors of your website and different pages.
By helping detecting design flaws, it allows you to optimise user experience. 

Events are sent to AFS Analytics via the ==send== command or automatically 
detected when activating the ==autotrack== option. 
This guide explains how to use the send command to send events to AFS Analytics. 

!!! note
    Categories, actions or types must be specified in English. 

## Capturing events with the SEND  command 

Use the ==send== command coupled to the call type event to send an event to AFS Analytics. 

Simplified syntax: 
```js
aa(
    "send", 
    "event", 
    [category], 
    [action], 
    [label], 
    [type], 
    [url], 
    [callback], 
    [params]
);
```

| Required fields | Description
| --- | ---
| category | defines the category of the event (eg video). The alternate field eventCategory is supported to ensure compatibility with Google Analytics.
| action|  specifies the type of action attached to the category (eg play). The name eventAction for this field is supported for compatibility with Google Analytics.
| label |  gives a title to the event (eg My holiday video). EventLabel is supported to ensure compatibility with Google Analytics.

| Optional fields | Description
|--- | ---
| type | defines the type or additional information about the event. 
| url |  This field defines a location for the event. 
| callback | Return function to call after transmission of the event to AFS Analytics servers. The function returns three parameters. The hitType, the event object and the params object. This parameter can be a function or a string containing the name of the function. 
| params | An object defined in the calling function to return as parameters in the return function.

!!! tip
    When an empty string is used as a parameter, the default value of the corresponding field will be used. 


Example sending an event:

```js
 /*The following function tells AFS Analytics 
   that a visitor has started to watch a video */

aa ("send", "event", "video", "play", "My video");
```

The same command with an object as argument :
```js

/* With only Google Analytics compatible fields  */

aa ("send", {
  HitType: "event",
  EventCategory: "Video",
  EventAction: "play",
  EventLabel: "My video"
});


/* Enhanced version including specific AFS Analytics field */ 

Function mycallback (a, b, c) {console.log (a, b, c); }
aa ("send", {
  HitType: "event",
  EventCategory: "video",
  EventAction: "stop",
  EventLabel: "My video test",
  EventType: "all",
  EventUrl: "http: //www.afsanalytics/myvideo.avi",
  HitCallback: mycallback,
  Params: {message: "this has been sent"}
});
```


!!! note
    *HitType* object property should not be confused with the type field. 


## Autotrack option and datasets

All the following examples are using autotrack and datasets. 
It is assumed that the autotrack option has been set to either ==dataset== or ==on==. 

If you have any doubt about setting the autotrack option, 
add the following line after the tracker is created  to initialize autotrack in dataset mode. 

```js
aa("Set", "autotrack", "dataset");
```

### Setting the the datasets

Dataset syntax in an HTML tag: 

```js
data-[datasetprefix]-[name of the field]="value of the field"
```

!!! note 
    *datasetprefix* is a variable defined with the default aa in analytics.js. 
    It can be modified using the set option. 

Example of initializating the category field :
```js
data-aa-category="click"
```

The datasets fields are those specific to AFS Analytics. 
That is to say *hittype*, *category*, *action*, *label*, *url*, *callback*, and *params*. 
In the datasets, only the category and label fields are mandatory. 
The action field may be recommended for certain types of events. 
Other fields are usually detected. By default hitType field is set to *event*. 

### Tags detected by autotrack

The Autotrack option detects any datasets attached to *a*, *div*, *button*, *iframe*, and *form* tags. 

Example of using dataset in a youtube iframe:
```html
<Iframe width="480" height="280" src="https://www.youtube.com/embed/cnBtRh08ShQ?rel=0" frameborder="0" 
  data-aa-category="video" 
  data-aa-action="start" 
  data-aa-label="Advanced visitor tracking"> 
</ iframe>
```

Each click on the video will now be captured by AFS Analytics. 



## Click events

If the action field is empty, analytics.js will automatically detect the type of the click
( *inside* or *outbound*). If the url field is not specified, it will be replaced by *none*. 

For an inside click: 
```js
aa{"send", "event", "click", "inside", "My click");
```
For an outbound click: 
```js
aa("send", "event", "click", "outbound", "My click");
```

### Click detection using Autotrack and dataset

```html
<a href="https://afsanalytics.com" 
  data-aa-hitType="event" 
  data-aa-category="click" 
  data-aa-label="my link" 
>
  my link
</a>
```

!!! note 
    AFS Analytics will automatically detect the url, type and action fields if they are not defined in the datasets. 

## Download events

Downloads events are transmitted to analytics.js using the category *Download*. 
As the type field is not used, the value *none* is indicated. 
Finally, the URL field indicates the location of the file. 

```js
aa(
    "send", 
    "event", 
    "download", 
    "successful", 
    "My file",
    "none","
    http://mysite.com/mypdf.pdf"
);
```

### Detection of downloads via Autotrack and dataset

When using autotrack option, the url and type fields do not need to be filled in.

```html
<a href="http://mysite.com/myfile.pdf" 
  data-aa-hitType="event" 
  data-aa-category="download" 
  data-aa-label="my pdf file" 
  data-aa-callback="mycallback" 
  data-aa-params="{message:"test"}" 
>
  myfile.pdf
</a>
```


!!! note
    The downloaded file URL does not need to be specified in the dataset, as it is set as href source. 

!!! note 
    In the example above, an optional callback function is passed in order to be executed after the event is sent.



##  Form events
AFS Analytics can detect events related to filling forms. If the events are sent correctly, AFS will calculate the average fill time and the dropout rate. The form category is reserved for the form. 

The various steps of filling in a form are: 

- Opening the form: open action 
```js
aa("send", "event", "form", "open", "My form");
```

- Submitting the form: submit action 
```js
    aa("send", "event", "form", "submit", "My form");
```

-  Submission results:   
```js
/* On success: */
 aa("send", "event", "form", "successful", ‘My form’);

/* On Failure */
 aa("send", "event", "form", "failed", ‘My form’);
```

- Closing the form: close 
```js
aa("send", "event", "form", "close", "My form");


/* If the form is closed with a cancel button: cancel and close */

aa("send", "event", "form", "cancel", "My form");
aa("send", "event", "form", "close", "My form");

/* or using the action: cancelandclose */

aa("send", "event", "form", "cancelandclose", "My form");
```

If the open and close actions were correctly defined, the average viewing time of the window will be displayed on the dashboard. 

### values of the type field associated with the form

By adding the "type" parameter you can define the form type. 
Available options are: 

- Information
- Setting
- Signup
- Login
- Contact
- Logout

### Capturing forms with Autotrack

!!! note 
    This section of the document will be added later. 

## Window related events

Window events can be either *open* or *close*. 

On window opening:
```js
aa("send", "event", "window", "open", "My window");
```

On closing:
```js
aa("send", "event", "window", "close", "My window");
```

When both actions *open* and *close* are sent, the average view time of the corresponding document will be displayed on the dashboard. 



## Video events

Four actions are offered to track Video events: 

- start 
- pause
- resume
- stop 

!!! tip
    *start* action can be replaced by *play*, both names are accepted 

- Whenever a user starts playing the video: 
```js
aa("send", "event", "video", "start", "My video");
```

- When user clicks the pause button: 
```js
aa("send", "event", "video", "pause", "My video");
```

- When user resumes playback of the video: 
```js
aa("send", "event", "video", "resume", "My video");
```

- When the video has ended or has been stopped:
```js
aa("send", "event", "video", "stop", "My video"); 
```


### Capturing the playback of a YouTube video with Autotrack and datasets.

As mentioned above, the play action can be used as an alternative to the start action. 

```js
<iframe src="https://www.youtube.com/embed/cnBtRh08ShQ?rel=0" frameborder="0" 
 data-aa-category="video" 
 data-aa-action="play" 
 data-aa-label="AFS Analytics video"
</iframe>
```

## Alert events

Alert events are used to send custom alert messages to AFS Analytics. 
Many global companies use a dedicated AFS Analytics account to capture bugs occuring on their properties. 
This option, used by web agencies to ensure the reliability of the sites they have developed, 
allows, each time an alert is received, 
to check the origin of an error as well as the profil of the visitor who generated it. 


| Event action | Description 
| --- | ---
| Post | Always true, the alert appears in the report grouping the alerts
| Email| Alert will be sent to the email address defined in AFS Analytics
| SMS | Alert is transmitted by SMS
| EmailandSms | Alert will be sent by both SMS and EMAIL


Alert type should be set to *warning*, *debug*, *error* or *fatal*. 

```js
aa("send", "event", "alert", "post", "JavaScript routine error", "fatal");
```

## Campaign events

Campaign events are automatically generated by analytics.js 
using the ==utm== parameters appearing in a request query string. 

Please refer to the [Measuring online marketing campaign performance](../using-utm-variables/) guide for more information. 


## ECommerce events

Capture of sales and transactions events related to eCommerce are described in the guide [E-commerce Tracking](../e-commerce-tracking/)


## Predefined options accepted by AFS Analytics.

AFS Analytics only accepts predefined *categories*, *actions* and *types*. 
Here is a non-exhaustive list of accepted values: 

| Type | Accepted values
|---|---
| Events Categories | click, download, form, video, window, alert, and navigation 
| Actions | None, Open, Close, Outbound, Inside, Send, Submit, Cancel, Canceledclose, Successful, Failed, Start, End, Proceed, View, Post, Email, SMS, EmailAndSMS, Play, Pause, Resume 
| Types | None, Button, Link, Div, iframe, Page, Information, Alert, Setting, Signup, Login, Warning, Fatal, Debug, Error, Contact, Logout, Menu 