---
layout: 2columns
title: Search for product ads
categories: guides
tags: Advertising
---

# Search a Product Ad
There are two different ways to search Product Ads. 

## By ID
One ways is searching the product Ad by it's ID. This means that you will get only one Product Ad.
In order to use this service you have to do as follow:

<pre class="terminal">
curl -i -H "X-Caller-Scopes: mclics_admin"
https://api.mercadolibre.com/mclics/productAd/11130279?access_token=$ACCESS_TOKEN  
</pre>

You will receive the following JSON response:

{% highlight javascript %}
{
	"adDailyBudget":"1",
	"adID":"11130279",
	"campaignID":"39003",
	"categID":"1652",
	"originalCategID":"1652",
	"custID":"66258610",
	"customAdBox":"",
	"invalidLink":"false",
	"maxCPC":"0.15",
	"name":"Default",
	"refFrom":"Reference owner",
	"refID":"Reference ID",
	"siteID":"MLA",
	"status":"A",
	"title":"Title Test",
	"type":"P",
	"URLDestiny":"http://www.mercadolibre.com.ar",
	"URLVisible":"www.mercadolibre.com.ar,
	"image":"exampleImage.jpg",
	"price":"15"
}
{% endhighlight %}

## By Reference
The other way of searching Product Ads is by Reference. With this service you can get one or more Product Ad. To do so you have to do as follow:

<pre class="terminal">
curl -i -H "X-Caller-Scopes: mclics_admin"
https://api.mercadolibre.com/mclics/productAd/search?custId=66258610&refFrom=Prueba&refId=prueba&access_token=$ACCESS_TOKEN  
</pre>

You will receive the following JSON response:

{% highlight javascript %}

NOT YET

{% endhighlight %}
