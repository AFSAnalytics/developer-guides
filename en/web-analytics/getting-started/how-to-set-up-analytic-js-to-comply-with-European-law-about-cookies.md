hero: Information for European publishers using AFS Analytics.
title: How to set-up analytic.js to comply with the European law on the deposit of cookies
description: How to set-up analytic.js to comply with the European law on the deposit of cookies

# Information for European publishers using AFS Analytics.
## Cookie: What does the law says?

In application of the European directive called telecom package, internet users must be informed and give their consent prior to use cookies. Publishers are therefore obliged to obtain this consent. This consent is valid for a maximum of 13 months.In other words, the website must ask users if they agree to most cookies and similar technologies before the site starts to use them. 
However, some cookies are exempt from this requirement 

## Which cookies do not require the prior consent of users?

1. Session identifying cookies (session-id) such as first‑party cookies to keep track of the user's input when filling online forms, shopping carts, etc., for the duration of a session or persistent cookies limited to a few hours in some cases
2. Web analytics or audience measurement cookies, under certain conditions. See paragraph below;
3. Cookies strictly necessary for the delivery of a service expressly requested by the subscriber or the user;
4. Shopping cart cookies for a merchant site;
5. Authentication cookies;
6. Multimedia player session cookies;
7. Load balancing session cookies;
8. UI customization cookies: User interface customization cookies are used to store a user’s preference regarding a service across web pages and not linked to other persistent identifiers such as a username. They are only set if the user has explicitly requested the service to remember a certain piece of information, for example, by clicking on a button or ticking a box. They may be session cookies or have a lifespan counted in weeks or months, depending on their purpose

## About web analytics cookies

To be exempt from a consent request, audience measurement cookies must meet the following conditions 

1. Information must be given to users who must be able to oppose the treatment. (Opt-out);
2. The data collected should not be cross-checked with other treatments: Shared cookies.
3. The cookie must only be used for the production of anonymous statistics and must not allow navigation to be monitored by different sites. Its life should be limited to 13 months.
4. Anonymized IP address: To avoid going back to a physical person, only the first two bytes of the IP address will be kept.

Analytics solutions that do not comply with the above conditions must be subject to the prior consent of users. 

## How to configure AFS Analytics to be in compliance

AFS Analytics only has first-party cookies, which means cookies that are posted from your site's domain. The content of first-party cookies can only be transmitted from your site and are not accessible outside your site. 

There are three ways to bring your site into compliance: 


### Solution #1: Ask AFS Analytics not to store cookies.

This is the most radical solution. AFS will not deposit cookies on Internet users' terminals. Only session cookies allowed by law will be used. The disadvantage of this solution is the impossibility of knowing whether the visitor is new or returning, or access the list of his previous visits. 

#### How to configure analytics.js to stop depositing cookies 

##### a. Enable the consent rule
The consent rule is activated with the ==nocookie== parameter.

##### b. Define the region to which the consent rule applies.
|Region | Code
|---|---
|Europe | eu
| USA | us
| All | all 

In the following example the rule applies only to EU citizens. 

```js
/* solution #1 code */

aa("set","cookieconsent_mode", "nocookie")
aa("set","cookieconsent_audience", "eu") ;
```

#### How does it work? 

AFS detects the user's country,
- If it is European, cookies are not stored
- Otherwise cookies are saved normally.

!!! note 
    The user location service provided by AFS Analytics is guaranteed only for premium accounts. For free accounts, you must inform AFS Analytics of the user's location. 


### Solution #2 The exemption of request for consent to Internet users.

This solution allows you to be exempt from consent in accordance with the regulations. The duration of the cookie is 12 months from the first visit. 

##### a. Inform the user of the presence of audience measurement cookies

Mention inside your site legal notice that you are using AFS Analytics
as a solution of audience analysis. 

You can use the following message: 

```html
In order to better serve you and improve the user experience, 
we are analyzing the audience of our site with 
<a href = "https://www.afsanalytics.com/info/105/web-analytics-how-it-works.html">Web Analytics</a> solution:
<a href="https://www.afsanalytics.com/">AFS Analytics</a>. 
This service complies with the general data protection regulations, and your IP address is anonymised.
We are the sole owner of the data collected on our website. 
For collecting data, we are using 
<a href="https://www.afsanalytics.com/info/113/add-analytics-js-to-your-website.html">analytics.js</a>,
a library developed by AFS Analytics. This library uses first-party Cookies: 
cookies that are exclusively attached to our domain name and are not shared. 
The data collected makes it possible to provide statistical traffic data.
We are the sole owner of these cookies, and you can oppose their registration:
<a href='javascript: aa("set","cookiesconsent","optout");'>Click here to opt out of AFS Analytics cookies</a>
```

##### b. Include a withdrawal or Opt-Out option in the legal notice.
##### c. Enable the consent rule in analytics.js.
##### d. Define the location of the users concerned.
##### e. Anonymize Users IP address

To avoid going back to a physical person, analytics.js will anonymize the IP address, only the first two bytes of the IP address will be kept. 
In our example the law applies only to European Internet users. 

```js
/* solution #2 example code */

aa("set", "cookieconsent_mode", "exemption")
aa("set", "cookieconsent_audience", "eu") ;
```

The setting for the cookieconsent_anonymizeipvariable accepts the following parameters : 
| Value | Description
| --- | ---
|true| Only the last byte is deleted. IP 8.8.8.8 becomes 8.8.8.0
|false| The address becomes 8.8.8.8
|1| Last byte is deleted -> 8.8.8.0 (equivalent to true).
|2| The last two bytes are deleted -> 8.8.0.0
|3| The last three bytes are deleted -> 8.0.0.0

!!! note
    ==cookieconsent_anonymizeip== variable should not be confused with ==anonymizeip==. The first applies only to users defined by cookieconsent_audience. The second concerns all site visitors. 

### Solution #3:  The request for consent to Internet users.

#### I. You asked the user's consent on your website:

As previously stated, AFS Analytics via analytics.js only uses first-party cookies, that is, cookies that are attached to the domain name of your site. For this reason, you do not have to request specific consent for AFS Analytics. The consent previously obtained by the visitor is valid for the removal of cookies managed by AFS Analytics. In this case, you just need to update your legal notices or terms of use. 

```html
In order to better serve you and improve the user experience,
we are analyzing the audience of our site with 
<a href = "https://www.afsanalytics.com/info/105/web-analytics-how-it-works.html"> Web Analytics</a> solution: <a href="https://www.afsanalytics.com/"> AFS Analytics </a>.
This service, which complies with the general data protection regulations, 
may save personal data (as defined by the GDPR) as a subcontractor, 
including a unique number consisting of alphanumeric characters identifying you. 
This encrypted data is saved on secure servers located in France or in Canada.
Canada guarantees data protection under Articles 44 and 46 of the GDPR.
No banking information is transmitted to AFS Analytics.
We are the sole owner of the personally identifiable 
or not information data collected on our website.
AFS Analytics does not share, sell, or claim any rights to this data.
The storage duration is limited to 365 days by default. 
You may request the deletion or modification of this data by contacting 
our Data Manager or <a href="https://www.datasense-analytics.com/">DataSense</a>,
the company responsible for data for AFS Analytics.
For collecting data, we are using <a href="https://www.afsanalytics.com/info/113/add-analytics-js-to-your-website.html">analytics.js</a>, 
a library developed by AFS Analytics. 
This library uses cookie technology. The cookies are exclusively attached 
to our domain name, first-party Cookies and are not shared. 
The data collected makes it possible to provide statistical traffic data.
We are the sole owner of these cookies, 
and you can oppose their registration: <a href='javascript: aa("set","cookiesconsent","optout");'>Click here to opt out of AFS Analytics cookies</a>
```

#### II. You did not ask for the user's consent:

You must inform the user of the deposit of cookies and add a mention in your privacy page or legal notice. 

##### When is the consent of the user valid? 
To the extent that the consent must not be ambiguous, the consent banner must stay visible until the person has continued to navigate, that is, as long as they have not visited another page of the site or clicked on an element of the site (image, link, search button). 

##### The steps to follow: 
###### a. Display a banner informing about the use of cookies: 
```html
By continuing your visit to this site, you accept the use of Cookies to establish visit statistics. <a href = "mycookies.html"> Learn More</a>.
```

###### b. A "Learn More" link: 
Optionally, you can add a learn more link sending to a page detailing the role of registered cookies and an opt-out option (removal of cookies). 

###### c. Add AFS Analytics disclaimer to your privacy policy page: 

```html
In order to better serve you and improve the user experience, we are analyzing the audience of our site with <a href = "https://www.afsanalytics.com/info/105/web-analytics-how-it-works.html"> Web Analytics</a> solution: <a href="https://www.afsanalytics.com/"> AFS Analytics </a>. This service, which complies with the general data protection regulations, may save personal data (as defined by the GDPR) as a subcontractor, including a unique number consisting of alphanumeric characters identifying you. This encrypted data is saved on secure servers located in France or in Canada. Canada guarantees data protection under Articles 44 and 46 of the GDPR. No banking information is transmitted to AFS Analytics.  We are the sole owner of the personally identifiable or not information data collected on our website. AFS Analytics does not share, sell, or claim any rights to this data. The storage duration is limited to 365 days by default. You may request the deletion or modification of this data by contacting our Data Manager or <a href="https://www.datasense-analytics.com/">DataSense</a>, the company responsible for data for AFS Analytics. For collecting data, we are using <a href="https://www.afsanalytics.com/info/113/add-analytics-js-to-your-website.html">analytics.js</a>, a library developed by AFS Analytics. This library uses cookie technology. The cookies are exclusively attached to our domain name, first-party Cookies and are not shared . The data collected makes it possible to provide statistical traffic data. We are the sole owner of these cookies, and you can oppose their registration: <a href='javascript: aa("set","cookiesconsent","optout");'>Click here to opt out of AFS Analytics cookies</a>
```

###### d. How to configure analytics.js: 
Analytics.js can perform all the technical part for you: 

AFS Analytics does the following: 

AFS uses its location service to define the internet user as European.

Has the user given consent?
-> If yes, does the ==cookieconsent_status== exist? if Yes, read its content:
If ==deny== or ==optout==. No consent, no saved cookies. Only a session cookie is used. 
if ==allow==, cookies are stored normally. 

If no consent, a consent request banner will be automatically displayed by analytics.js (automated mode: consent_auto or your own callback routine will be called, mode: consent 
!!! note
    Consent messages displayed by analytics.js are in French or English depending on the origin of the user. 

#### Automated mode

If you want the AFS Banner to be automatically displayed, 
you have to set the consent mode to ==consent_auto==. 

```js
/* solution #3 with automated mode */

aa("set","cookieconsent_mode", "consent_auto")
aa("set","cookieconsent_audience","eu") ;
``` 
Optionally in this mode you can define your own message, the button caption and a callback function: 

|Argument| Description
|---|---
|cookieconsent_message| The message to display.
|cookieconsent_button| The button text.
|cookieconsent_callback| your own function, you can change the attributes of the box or text.

Example: 

```js
aa("set", "cookieconsent_mode", "consent_auto")
aa("set", "cookieconsent_audience", "eu") ;
aa("set", "cookieconsent_message", "By continuing your navigation, you accept the use of cookies to gather statistics and offer targeted advertisement") ;
aa("set", "cookieconsent_button", "Accept") ;
```

Example with callback function
( Use the callback function to change box attributes )

```js
aa("set", "cookieconsent_mode", "consent_auto")
aa("set", "cookieconsent_audience", "eu") ;
aa("set", "cookieconsent_message", "By continuing your navigation, you accept the use of cookies to gather statistics and offer targeted advertisement") ;
aa("set", "cookieconsent_button", "Accept") ;
aa("set", "cookieconsent_callback", "myfunction") ;
```

Default mode ( Banner is displayed by your own routine ) 

```js
/* solution #3 with default mode */

aa("set", "cookieconsent_mode", "consent")
aa("set", "cookieconsent_audience", "eu") ;
aa("set", "cookieconsent_callback", "askconsent") ;
```

!!! note
    If you use AFS Analytics localization service, a cookie, aa_country, containing the user's country will be created 


#### Function used by analytic.js to display the banner 

```js
function consentbox()
 {
   var m=this.cookieconsent_message;
   var b=this.cookieconsent_button;
    var l=0; 
     
  if (m==-1)
   {
   
   var l0 = navigator.language || navigator.userLanguage; 
   var l1 =document.getElementsByTagName('html')[0].getAttribute('lang');
   var l2=document.getElementsByTagName('html')[0].getAttribute('xml:lang');
   if (l0=="fr" || l1=="fr" || l2=="fr") l=1;
   m="This site uses cookies. By continuing to browse the site you are agreeing to our use of cookies.";
   b="Accept";
    if (l==1)
    {
    var m="En poursuivant votre navigation, vous acceptez l’utilisation de Cookies pour réaliser des statistiques et vous proposer des publicités.";
    b="J'accepte";
    }
   } 
   
   var div=document.createElement('div');
    div.id = 'consent_box';
    document.body.appendChild(div);
    div = document.getElementById("consent_box");
    div.style.width="100%";
    div.style.margin="0";
    div.style.background="rgba(0, 0, 0, 0.80)";
    div.style.padding="5px";
    div.style.color="#FFF";
    div.style.position="fixed";
    div.style.display="none";
    div.style.bottom="0";
    div.style.right="0";
    div.style.left="0";
    div.style.zIndex="9999";
    div.style.fontSize="13px";
    div.style.fontFamily="sans-serif"; 
    var text='<div class="consent_design">';
    text+='<div id="consent_text">'+m+'</div>';
    if (b!=-1) text +='<div id="consent_button"  onclick="document.getElementById('consent_box').style.display='none';aa('set','cookieconsent_status','allow');">'+b+'</div>';
    text+='</div>';
    div = document.getElementById("consent_box");
    div.innerHTML=text;
    var div1=document.getElementById("consent_text");
    div1.style.minheight="20px";
    div1.style.padding="10px";
    div1.style.width="70%";
    div1.style.display="inline-block";
    div1.style.cssFloat="left";
    
    if (b!=-1) 
    {       
    div1=document.getElementById("consent_button");
    div1.style.fontFamily="sans-serif";
    div1.style.fontSize="13px";
    div1.style.margin="10px";
    div1.style.marginRight="20px";
    div1.style.display="inline-block";
    div1.style.cssFloat="right";   
    div1.style.border="2px solid rgba(255,255,255,1)";
    div1.style.borderRadius="2px";
    div1.style.padding="5px 10px";
    div1.style.fontWeight="400";
    div1.style.opacity=".90";
    div1.style.cursor="pointer";
    }
         
      div.style.display ="block";
   };
```

### Analytics.js Additional options 

#### Changing the name of the consent cookie
```js
aa("set", "cookiesconsent_name", "nameofcookieconsent") ; 
```

#### Localization service 
On each user connection, analytics.js uses its location service to detect the origin of 
the visitor and deposit the cookie aa_country containing the code of his country. 
This cookie is exempt from the visitor’s consent request.
However, the availability of this service is provided exclusively to our premium plan subscribers. 
For free accounts, we advise you to disable this service, and to inform AFS about the visitor's country. 
```js
aa(set, "localisation", "disable") ;
aa(set, "country", "FR") ;
```

## Useful information

- [Cookie Consent Exemption](http://ec.europa.eu/justice/data-protection/article-29/documentation/opinion-recommendation/files/2012/wp194_en.pdf)
- [AFS Analytics GDPR Compliance and Privacy](/)

