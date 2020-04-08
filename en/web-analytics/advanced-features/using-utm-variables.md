hero: Tracking Marketing Campaigns - Using UTM variables
title: Tracking Marketing Campaigns - Using UTM variables
description: learn about using UTM variables to track marketing campaings.


# Using UTM variables

AFS Analytics tracks UTM settings to analyze the performance of your marketing campaigns. 
This guide will teach you how to set the UTM parameters in links as well as how to use them 
to measure the effectiveness of your campaigns. 

## UTM parameters definition

UTM parameters are used to identify incoming traffic to a website from a specific source. 

These parameters are variables added to a link to identify its origin. 
They are usually included in the query string of the URL or, after its # anchor. 
The *UTM* acronym means *URCHIN Tracking module*, as this system was first introduced by the "Urchin Software Corporation" company. 


## Purpose of UTM variables

These variables are used to measure the impact and performance of an advert campaign, 
a newsletter, an email, or just a link on a referring website. 

Example of a link used to measure the performance of an Google Adword campaign :
```html
https://www.afsanalytics.com?utm_source=google&utm_medium=cpc&utm_campaign=AFS%20Analytics%20January%202017&utm_term=Web%20Analytics&utm_content=text01&utm_calc=cpc&utm_cost=0.20
```

!!! tip 
    You will notice in the link above several parameters starting with the word utm_ these are the utm parameters. 


!!! note 
    AFS Analytics added two parameters to this standard. The utm_calc and utm_cost variables. These are optional parameters used to calculate the total cost of a marketing campaign. 

# UTM Link Builder
AFS Analytics provides a free creative tool making easy to add UTM parameters to a link. You can find it here: [UTM Campaign URL Builder](https://www.afsanalytics.com/utm-campaign-url-builder.php)

# UTM variables

#### *utm_source

The utm_source variable indicates where the traffic comes from. That is to say, the referrer. 
In our example the referrer is "google". 

#### *utm_medium

Indicates the means used to obtain the traffic. That is, the marketing medium used.
In our example we specify that it is a click (cpc). Other possible values could be: banner, email, newsletters, social network, etc. 

#### *utm_campaign

The name given to the ad campaign. 

#### utm_content (optional)
    
The campaign container. It can be a picture, a banner size and  basically whatever you want. 

#### utm_term (optional)

Contains the paid keywords used for a search engine campaign. In our example: "web analytics" 

#### utm_calc (optional)

Cost calculation method for the related campaign. 

Accepted values are:

|Name|Description
|---|---
|cpc| Cost per click
|cpm| The cost for a thousand impressions
|cps| Cost per sale. This is a fixed commission per sale
|cpspercent| Cost per sale. But this is a percentage on the sale
|total| This is the total cost of the campaign


!!! important 
    The *cpm* option in utm_calc is currently unsupported, as there is no way for AFS Analytics to know the number of advertising impressions. Instead, use the total option, specifying the total cost of the ad campaign with utm_cost. 

#### utm_cost (optional)

This parameter must be set if utm_calc is present. This is the value linked to the variable. 

| utm_calc value | utm_cost meaning |
| --- | ---
|cpc|  unit cost of the click
|cpm| cost per thousand impression
|cps|  a unit cost per sale
|cpspercent| percentage on the sale
