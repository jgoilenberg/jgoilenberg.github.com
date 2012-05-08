---
layout: 1columns
title: List items
categories: guides
tag: List
---

# List your Item

You already know what items and attributes are. If you don’t know we recommend that you read the Listings Introduction tutorial.

So, let’s see how to list items in MELI. Don’t worry about the different attribute codes, we are going to explain each one latter.

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
"description":"This is the first Harry Potter book that was printed outside the UK, <strong> I bought it in San Francisco at the Harry Potters week in 2009 </strong> Do not miss the opportunity, it is in perfect conditions and with a unique design cover",
"pictures":[
{"source":"http://upload.wikimedia.org/wikipedia/en/a/a7/Original_Paperback_Cover.jpg"},
{"source":"http://upload.wikimedia.org/wikipedia/en/2/2c/Harry_Potter_and_the_Philosopher%27s_Stone.jpg"}
]
}'

https://api.mercadolibre.com/items?access_token=$ACCESS_TOKEN  
</pre>

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

