hero: AutoTrack - Automated Event Tracking
title: AutoTrack - Automated Event Tracking
description: AFS Analytics offers an option to automatically track the interactions between visitors and the pages of a website. 




# AutoTrack 

## Introduction

AFS Analytics offers an option to automatically track the interactions between 
visitors and the pages of a website. This feature, named AutoTrack, is one of the key components 
of our [web analytics solution](https://www.afsanalytics.com/).

## What events are tracked by the Autotrack option?

The _Autotrack_ option tracks the clicks associated with links, 
HTML elements and iframes present in a web page. Once detected, 
the element associated with the click is analyzed in order to define 
its attributes and the triggered action. 
It can be downloading a file, viewing a video, opening a window, 
submitting a form or simply clicking on a link.

Sending a page view can also be triggered by the autotrack option. 
This provides a detailed report about the most viewed sections of single-page websites.

Autotrack automatically detects the characteristics of an event, 
but specifying attributes via *datasets* increases the accuracy and effectiveness of this feature.

## DataSets

### Introduction

HTML5 enables the association of an HTML element with data by using the *data-* attribute called *dataset*.
To use this feature, your HTML page must be HTML5 compliant, that is, it must include the HTML5 doctype:
```hmtl
<!DOCTYPE html>
```

The syntax of a dataSet consists of the name of the variable preceded by the prefix *data-* followed 
by its value placed in a string.

```hmtl
<div data-category = "value"> ... </div>
```
In this example, the dataset is *category* and its value is *value*.

### Purpose

The purpose of datasets is the simplification of the storage of data in HTML documents, 
especially in the elements. Thanks to datasets, you can supply autotrack 
with a lot of data about the properties of an event.

## AutoTrack option modes

The AutoTrack option supports three different modes. 
The desired mode is transmitted with the *set* command via the *aa()* function. 



### Mode "on" 

In this mode, all events are tracked, even if no dataset is defined.

### Mode "dataset" 

In this mode, only those elements with defined datasets are tracked.

### Mode "off"

In this state, the Autotrack option is completely deactivated. 
There is no automatic capture of events.


## AutoTrack sub-settings

AFS Analytics allows you to disable some features of AutoTrack.
This is useful if you do not want to track certain events or items.

!!! note
     These settings must be declared after specifying the main mode of autotrack. Otherwise, they will be ignored.

Three modes are available for sub-settings:

 | Mode  | Action
 | :----- | :--------
 | Off   | Deactivates completely
 | Dataset | Tracks only if the "dataset" is defined 
| On | Tracks all events 


To set a sub-setting, we add a dot to "autotrack" followed by the sub-setting name .

```js
aa ('set','autotrack.subsetting',[state]);

/* Track only outbound click */
aa ('set','autotrack','off');
aa ('set','autotrack.outboundclick','on');

/* but not into iframe */
aa ('set','autotrack.iframe','off');
```

!!! note
 	There is a hierarchy in the definition of sub-settings. You must first set the general autotrack setting, then second the sub-settings insideclicks, outboundclick, download,video and lastly the sub-settings of the elements. *iframe*, *div*, and *button*.


```js

/* first setting */
aa ('set','autotrack','on');

/* disable inside clicks (second setting) */
aa ('set','autotrack.insideclick','off');

/*disable iframe tracking (last setting)*/
aa ('set','autotrack.iframe','off');

```





### Video setting

Sets *Video* tracking mode.

```js

aa('set',"autotrack.video","off");

/* same thing with an object */
aa('set',"autotrack",{"video":"off"});

```

!!! note
	The *iframe* sub-setting takes the value of the video sub-setting if *iframe* is set to *off*.

### Download setting

Sets *Downloads* tracking mode.

```js
aa('set',"autotrack.download","off");
```
!!! note
	The *iframe*, *div* and *button* sub-settings take the value of the *download* sub-setting if they are set to *off*.


### Outboundclick setting

Sets _Exit clicks_ tracking mode.

```js
aa('set',"autotrack.outboundclick","off");

```
The *iframe*, *div* and *button* sub-settings take the value of the *outboundclick* sub-setting if they are set to *off*.

### Insideclick setting

Sets tracking mode for clicks targeted to a site page.

```js
aa('set',"autotrack.insideclick","off");
```
The "iframe", "div" and "button" sub-settings take the value of the "insideclick" sub-setting if they are set to "off".

### Iframe setting

Sets *iframe* elements tracking mode.

```js
aa('set',"autotrack.iframe","off");
```

### Div setting

Sets *div* elements tracking mode.

```js
aa('set',"autotrack.div","off");
```

### Button setting

Sets *button* elements tracking mode.

```js
aa('set',"autotrack.button","off");
```


## Available Dataset fields 

| Field | Description
| :--- | :---
| *hitType* (optional) | Specifies the type of hit. It can accept two values: event or pageview. If it is not defined, it will be configured with event.
| *label* (required) | Specifies the title of the event. ( If the hitType is pageview, the label field can be replaced by title.)
| *category* | Indicates the category of the event: click, download, form, video, window, alert and navigation
| *action* |  Specifies the action. For example, for a click: Inside or outbound. For a list of available actions, please refer to the document "Event Tracking"
| *type* |  The type of the event. Not to be confused with hitType.
| *url* | The destination of the event.
| *callback* |  To set a callback function. 
| *params* | A string to be passed to the return function.


## Examples

### Setting several options with a single line of code:

```js
aa('set',"autotrack","dataset");
aa('set',"autotrack",{"insideclick":"on","iframe":"off"});
```

### Setting the datasets attributes for the Autotrack option:

The syntax of a dataset defined for autotrack is as follows:
```js
data-[datasetprefix]-[name of the field to be filled in]='field value'
```
!!! note
	datasetprefix is a variable defined with the default value aa.


### Category field

```js
sata-aa-category = 'click'
```


### Tracking clicks with autotrack and datasets

```html
<a href="https://www.mysite.com" 
   data-aa-hitType="event" 
   data-aa-category="click" 
   data-aa-label="mygreatclick" >
   my great click </a>
```
!!! note 
	AFS Analytics will automatically detect the url, type and action fields if they are not defined in the datasets. Tracking the downloads with autotrack and the datasets

```html
<a href="http://mysite.com/myfile.pdf"
   data-aa-hitType="event" 
   data-aa-category="download" 
   data-aa-label="My PDF" 
   data-aa-callback="mycallback" 
   data-aa-params="{message:'test'}" >
   myfile.pdf</a>
```
!!! note 
 	The callback function "mycallback" will be called after sending the event to analytics.js. The URL doesn't need to be specified in the dataset, it is already within the a href tag.

### Tracking the playback of a YouTube video with Autotrack and dataset.



```html
<iframe src="https://www.youtube.com/embed/cnBtRh08ShQ?rel=0" frameborder="0" 
	data-aa-category='video' 
	data-aa-action='play' 
	data-aa-label='AFS Analytics vidéo'>
</iframe>
```
!!! note
	The play action can be used as an alternative to the start action.






