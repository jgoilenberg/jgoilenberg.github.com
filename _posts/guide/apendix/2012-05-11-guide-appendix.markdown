---
layout: 1columns
title: Appendix - related APIs
categories: guides
tags: Appendix
---

#Appendix – Related APIs

Some of the tutorials described in this site need several “id’s” from different MELI’s API’s.

For example, when you list an item, you have to specify the following attributes:

{% highlight javascript %}

{
"title": "Test Item - Do Not Bid",
"category_id": "MLA3530",
"price": 10,
"currency_id": "ARS",
"available_quantity": 1,
"listing_type_id": "bronze",
"condition":"new"
}

{% endhighlight %}

As you can see in the JSON above, you need to specify the **category_id**, the **currency_id** and the **listing_type_id**. This particular three fields are mandatory and only accepts pre-defined id’s. You can see the different id’s that these fields accept by looking at the Category, Currencies and Listing Type APIs.

##Category API

The Sites API shows the entirely MELI category structure for a particular country, in this case Argentina.

	https://api.mercadolibre.com/sites/MLA/  
As you can see, you get information related to Argentina MELI operation, one of the JSON attributes is “categories”, in which you have the first level of categories.

{% highlight javascript %}
"categories": - [
- {
"id": "MLA5725",
"name": "Accesorios para VehÃ­culos",
},
- {
"id": "MLA1071",
"name": "Animales y Mascotas",
},
- {
"id": "MLA1367",
"name": "AntigÃ¼edades",
},
- {
"id": "MLA1743",
"name": "Autos, Motos y Otros",
},
{% endhighlight %}


For second level categories, or information related to specific categories, you have to use the Categories API sending the category ID as a URL parameter. The next example shows the information related to the “Animales y Mascotas” Category:

	https://api.mercadolibre.com/categories/MLA1071

{% highlight javascript %}
{
"id": "MLA1071",
"name": "Animales y Mascotas",
"permalink": "http://home.mercadolibre.com.ar/animales-y-mascotas",
"total_items_in_this_category": "30434",
"path_from_root": - [
- {
"id": "MLA1071",
"name": "Animales y Mascotas",
},
],
"children_categories": - [
- {
"id": "MLA1100",
"name": "Aves",
"total_items_in_this_category": "1430",
},
- {
"id": "MLA1117",
"name": "Caballos",
"total_items_in_this_category": "1092",
},
.
.
{% endhighlight %}

As you can see, you get the “path_from_root” and "children_categories" attributes, use these attributes to browse the categories tree to find the specific category for your item.

##Currency API

You can get the default currency_id for each MELI operation, using the Sites API.

	https://api.mercadolibre.com/sites/MLA/
In this case, you have to take a look at the “default_currency_id” attribute from the Sites API. This field specifies one id's of the "currencies" array (where all the available currencies are displayed)


{% highlight javascript %}
{
"id": "MLA",
"name": "Argentina",
"country_id": "AR",
"sale_fees_mode": "not_free",
"mercadopago_version": "3",
"default_currency_id": "ARS",
"currencies": - [
- {
"id": "USD",
"symbol": "U$S",
},
- {
"id": "ARS",
"symbol": "$",
},
],
}

{% endhighlight %}  
  
	https://api.mercadolibre.com/currencies/ARS
{% highlight javascript %}
{
"id": "ARS",
"description": "Peso argentino",
"symbol": "$",
"decimal_places": "2",
}
{% endhighlight %}
##Listing Type API

As you have seen in the previous tutorials, each time you list an item you have to specify a listing type.

A listing type defines the exposure level your listing will have in MELI. Each listing type has different levels of exposure and different fees.

The examples in the previous tutorials have used the listing type “bronze”, but if you want to change the level of exposure of you item you can specify another listing type id.

To see the complete list of listing types by country you have to use the listing type API:

	https://api.mercadolibre.com/sites/MLA/listing_types/

{% highlight javascript %}
[
- {
"site_id": "MLA",
"id": "gold_premium",
"name": "Oro Premium",
},
- {
"site_id": "MLA",
"id": "gold",
"name": "Oro",
},
- {
"site_id": "MLA",
"id": "silver",
"name": "Plata",
},
- {
"site_id": "MLA",
"id": "bronze",
"name": "Bronce",
},
- {
"site_id": "MLA",
"id": "free",
"name": "Gratuita",
},
]
{% endhighlight %}

For more information related to each listing type, let’s access to the listing type API sending the listing type ID as a URL parameter, in this case, for “gold”

	https://api.mercadolibre.com/sites/MLA/listing_types/gold

{% highlight javascript %}	
{
"id": "gold",
"configuration": - {
"name": "Oro",
"listing_exposure": "high",
"requires_picture": true,
"max_stock_per_item": "999",
"duration_days": - {
"buy_it_now": "60",
"auction": "10"
},
.
.
.
}
{% endhighlight %}
