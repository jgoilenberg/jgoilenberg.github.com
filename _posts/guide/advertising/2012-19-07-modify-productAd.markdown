---
layout: 2columns
title: Modify a Product Ad 
categories: guides
tags: Advertising
---

# Modify a Product Ad
The way to modify your product ad is as follow.

<pre class="terminal">
curl -i -H "X-Caller-Scopes: mclics_admin"  -H "Content-Type: application/json" -X PUT -d "
{
	"adDailyBudget":"1",
	"adID":"11130279",
	"campaignID":"39003",
	"categID":"1652",
	"custID":"66258610",
	"invalidLink":"false",
	"maxCPC":"0.15",
	"name":"Default",
	"refFrom":"Reference owner",
	"refID":"Reference ID",
	"siteID":"MLA",
	"status":"A",
	"title":"Title Test",
	"type":"P",
	"URLDestiny":"http://www.google.com.ar",
	"URLVisible":"www.google.com.ar",
	"image":"exampleImage.jpg",
	"price":"15"
}" 
https://api.mercadolibre.com/mclics/productAd/11130279"
</pre>

You will receive the following JSON response:

{% highlight javascript %}

{
	"errorsMap":null,
	"productAdDto":
	{
		"adDailyBudget":"1",
		"adID":"11130279",
		"campaignID":"39003",
		"categID":"1652",
		"custID":"66258610",
		"invalidLink":"false",
		"maxCPC":"0.15",
		"name":"Default",
		"refFrom":"Reference owner",
		"refID":"Reference ID",
		"siteID":"MLA",
		"status":"A",
		"title":"Title Test",
		"type":"P",
		"URLDestiny":"http://www.google.com.ar",
		"URLVisible":"www.google.com.ar","image":
		"exampleImage.jpg",
		"price":"15"
	}
}
{% endhighlight %}

**Congratulations!** You have modify your product ad.