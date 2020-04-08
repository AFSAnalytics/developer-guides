hero: Adding analytics.js to your website
title: Adding analytics.js to your website
description: Get the real measure of your website traffic and analyze your visitors behavior by adding analytics.js to your website




# Adding analytics.js to your website

Analytics.js is a JavaScript library developed by AFS Analytics in order to measure websites traffic and analyze visitors behavior. 

AFS Analytics offers a library compatible with Google Analytics, and which has the same structure and functions. This makes it easy to implement AFS Analytics for those accustomed to Google Analytics. At the end of this guide, you will find a section devoted to the difference between the two implementations, and how to replace quickly Google Analytics  by AFS Analytics. 

## Inserting AFS Javascript

### Location

The AFS Analytics JavaScript tracking code  ( also called JavaScript tracking snippet ) consists of a few code lines 
that should be pasted between the *head* element (highly recommended) or anywhere inside the  *body*  of your website pages. 

```html
<head>
 <!-- Most efficient position for AFS Analytics.js-->
</head>

<body>
<!-- Alternate position -->
</body>
```

### The code


```js
<script type="text/javascript">
(function(i,s,o,g,r,a,m){i['AfsAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//code.afsanalytics.com/js/analytics.js','aa');
aa('create', 'XXXXXXXX', 'auto');
aa('set','autotrack','dataset');
aa('send', 'pageview',);
</script>
```

!!! important 
	Make sure to replace the XXXXXXXX string with your site identifier ID. This unique 8-digit number is created when you register your website on AFS Analytics. You can find it by choosing the *Manage Websites* option appearing in your dashboard *Account* menu. 
 


The above code does the following: 

1. Loads the analytics.js library asynchronously. 
2. Initializes the library and defines the name of the global function, as aa().
3. Creates the aa() global function ( also called the aa() command queue), which saves the commands in a waiting list to be sent to analytics.js.
4. Adds the *create* command to the aa() command queue to create a new tracker object.
5. Adds a second command to the aa() command queue to select the events tracking mode autotrack.
6. Adds one last command to the aa() command queue to send data about the current pageview to AFS Analytics.

This example shows the basic implementation of AFS Analytics on a website. This JavaScript code may require changes or modifications dedicated to your website. 

The aa() function offers numerous additional commands and parameters to help you to track more interactions. 

!!! note
	The HTML/JavaScript tracking code preceding the aa() function doesn’t need to be changed. 

The above javacript code tracks by this data. 

- The time spent by the visitor on the site.
- The time spent and the detail of each page visited (page view).
- The date of their last visit.
- The location of the visitor.
- The configuration used.
- The referring site.
- The events defined by the dataset in the tags.


###  (Optional) Displaying AFS logo

Should yous wish to display AFS Analytics logo on your website, you can do it by adding the following HTML code where you want the logo to appear:


```html
<div id ='afsanalytics'></ div>
```

!!! Note
 	( Free accounts only ) This tag is required if your traffic exceeds the limit. 



### Adavanced customization


For basic activity reports, implementing the previous JavaScript tracking code is sufficient. For an advanced and customized installation, meaning tracking the interactions of the visitors with the content of your site, it is advisable that you read the following guides: 

1. How does analytics.js work?
2. Creating a tracker.
3. Getting and Setting tracker data.
4. Sending data to AFS Analytics.


## Differences between AFS Analytics and Google Analytics code.

There are three differences between the two codes. 

1 - The name of the global object (2nd line of the code)

| AFS Analytics | Google Analytics 
| ------------- | ----------------
| AfsAnalyticsObject | GoogleAnalyticsObject.


2 - The URL of the analytic.js script (5th line)

| AFS Analytics | Google Analytics 
| ------------- | ----------------
|  https://code.afsanalytics.com/js/analytics.js | https://www.google-analytics.com/analytics.js

3 - The name of the main calling function (5th line)

| AFS Analytics | Google Analytics 
| ------------- | ----------------
| aa | ga



## Replacing Google Analytics with AFS Analytics in just a few seconds

Simply change a small portion of the Google code on your site page and keep the name of the call function: 

1. Replace GoogleAnalyticsObject by AfsAnalyticsObject
2. Replace https://www.google-analytics.com/analytics.js by https://code.afsanalytics.com/js/analytics.js
3. Keep *ga* as the name of the calling function in order to get compatibility of calls to the global function.

The original Google Analytics JavaScript tracking snippet. 
```js
<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');
ga('create', 'UA-XXXXX-Y', 'auto');
ga('send', 'pageview');
</script>
```

To be replaced with:
```js
<script>
(function(i,s,o,g,r,a,m){i['AfsAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//code.afsanalytics.com/js/analytics.js','ga');
ga('create', 'XXXXXXXX', 'auto');
ga('send', 'pageview');
</script>
```

!!! important 
	Do not forget to replace XXXXXXXX with your website unique ID. 

## Calls to analytics.js when the function name is "ga"

All calls to analytics.js are done using the ga() command. 
You can add the autotrack command to set the events tracking mode: 

```js
ga('create', 'XXXXXXXX', 'auto');
ga('set','autotrack','dataset');
ga('send', 'pageview');	
```