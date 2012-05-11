---
layout: 2columns
title: List items
categories: guides
tag: Listing
---

# List your Item


You already know what items and attributes are. If you don’t know we recommend that you read the Listings Introduction tutorial.


So, let’s see how to list items in MELI. Don’t worry about the different attribute codes, we are going to explain each one latter.



### Table of Contents
- [Requirements](#requirements)
- [Listing example](#list-example)
- [Special considerations for real estate, vehicles & services](#further-consideration)


## Previous requirements





## Listing example{#list-example}

We're ready to list our first item. You can use the code below to create your first item:

<pre class="terminal">

curl -X POST -H "Content-Type: application/json" -d
'{
"title":"Harry Potter and the Sorcerer stone - Unique Cover",
"category_id":"MLA1227",
"price":10,
"currency_id":"ARS",
"available_quantity":1,
"buying_mode":"buy_it_now",
"listing_type_id":"bronze",
"condition":"new",
"description":"This is the first Harry Potter book that was printed outside the UK, {{"<strong> I bought it in San Francisco at the Harry Potters week in 2009 </strong>" | xml_escape }} Do not miss the opportunity, it is in perfect conditions and with a unique design cover",
"pictures":[
{"source":"http://upload.wikimedia.org/wikipedia/en/a/a7/Original_Paperback_Cover.jpg"},
{"source":"http://upload.wikimedia.org/wikipedia/en/2/2c/Harry_Potter_and_the_Philosopher%27s_Stone.jpg"}
]
}'

https://api.mercadolibre.com/items?access_token=$ACCESS_TOKEN  
</pre>

As you may suppose, each type of item has it's own attributes and restrictions when listing them. Please refer to the [API Appendinx](/guide-appendix) for more information 
about how to obtain and use these attributes.

The Items API will automatically download the provided images to MELI Storage and creates a listing for your item. You will receive the following Json response:


{% highlight javascript %}
{
"id":"MLA421174922",
"site_id":"MLA",
"title":"Harry Potter And The Sorcerer Stone - Unique Cover",
"permalink":"http://articulo.mercadolibre.com.ar/MLA-421174922-harry-potter-and-the-sorcerer-stone-unique-cover-_JM",
.
.
}

{% endhighlight %}

**Congratulations!** You have just list your first item! You can access the Item’s VIP throw the permalink attribute.  

If you have some questions regarding how to get your access token to list items, please refer to the [getting started](/getting-started) tutorial.


## Special considerations for real estate, vehicles & services {#further-consideration}

In MELI you can list different type of items which can be grouped in the following categories:

*Products    
*Vehicles    
*Real estate    
*Services    


If you still have some questions, [Here](/real-estate-list-item) you can see an example on how to list real estate items in MELI.




