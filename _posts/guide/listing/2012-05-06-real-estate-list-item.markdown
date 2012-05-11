---
layout: 2columns
title: Real estate listing
categories: guides
tag: Appendix
---


#Listing real estate property

The purpose of this tutorial is to provide a real example on how to list real estate items using the MELI API platform. 

### Table of Contents
- [Considerations](#considerations)
- [Listing example](#listing-example)
- [Define the property type and operation](#define-operation)
- [Select the property's location](#propety-location)


## Considerations{#considerations}

Please note that you must have a basic knowledge about how the MELI API's work and it's design structure. Refer to the [getting started](/getting-started) and
[guides](/guides) tutorials for more information.


## Listing example{#listing-example}

Call the API with the corresponding JSON format with and required attributes.

<pre class="terminal">
curl -i -X POST -H "Content-Type: application/json" -d
'{
   "title":"Item title",
   "category_id":"MLA52745",
   "price":500,
   "currency_id":"ARS",
   "available_quantity":1,
   "listing_type_id":"silver",
   "condition":"new",
   "pictures":[
      {
         "id":"MLA2096545948_102011"
      },
      {
         "source":"http://farm3.staticflickr.com/2417/2176897085_946b7b66b8_b.jpg"
      },
      {
         "source":"http://farm2.staticflickr.com/1056/628680053_3b7c315548_b.jpg"
      }
   ],
   "location":{
      "address_line":"Item street 1234",
      "neighborhood":{
         "id":"TUxBQlBBUzgyNjBa"
      }
   },
   "attributes":[
      {
         "id":"MLA50547-AMBQTY",
         "value_id":"MLA50547-AMBQTY-1"
      },
      {
         "id":"MLA50547-ANTIG",
         "value_id":"MLA50547-ANTIG-A_ESTRENAR"
      },
      {
         "id":"MLA50547-MTRS",
         "value_name":"500"
      },
      {
         "id":"MLA50547-SUPTOTMX",
         "value_name":"2000"
      },
      {
         "id":"MLA50547-BATHQTY",
         "value_id":"MLA50547-BATHQTY-1"
      },
      {
         "id":"MLA50547-DORMQTYB",
         "value_id":"MLA50547-DORMQTYB-3"
      },
      {
         "id":"MLA50547-EDIFIC",
         "value_id":"MLA50547-EDIFIC-CHALET"
      }
   ],
   "description":"<b>Alquiler temporario de quinta</b>"
}'

https://api.mercadolibre.com/items/?access_token=$ACCESS_TOKEN
</pre>
    
**Congratulations!** you have listed your first real estate item using the MELI API platform.

## Define the property type and operation{#define-operation}

Before listing our item, we need to get the minimum necessary information required to submit our request. If you try to list an item without the required fields
you'll get an error from the API with the corresponding missing attributes.

To check which attributes are required for our item we can browse the following url:

	https://api.mercadolibre.com/categories/MLA1473/attributes
	

**Note:** If you don't know the id of the category you want to list in, you can get a list of categories at https://api.mercadolibre.com/sites/YOURSITE/categories/ where *`YOURSITE`* represents
the site id of your country (ie. MLA,MLB,MLC, etc)

From the url above we see that the following attributes are required to list our item in that category:

{% highlight javascript %}
{
"id": "MLA1472-ANTIG",      
"id": "MLA1472-DISPOSIC",    
"id": "MLA1472-AMBQTY",    
"id": "MLA1472-BATHQTY",    
"id": "MLA1472-DORMQTY",    
"id": "MLA1472-MTRS",	    
"id": "MLA1472-MTRSTOTAL"    
"id": "MLA1472-EDIFIC"
}
{% endhighlight %}

Keep in mind that you must also check which data types are allowed per attribute as well as it's possible values 

## Property's location{#propety-location}

Another required field for real estate items is the location information of the item. You can get a list of possible locations by browsing the following url:

	https://api.mercadolibre.com/classified_locations/countries/
	
Select the country you want to list your item in and retrieve all the location ids (country/state/city/neighborhoods) necessary to submit your request.    




