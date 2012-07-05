---
layout: 2columns
title: Real estate listing
categories: guides
tags: Selling
---

#Real estate listing

Preconditions 	{#preconditions}
---------------------------------

To list a real estate property using MELI's APIs, the following preconditions are necessary:

[Having a MELI registered user](http://www.somelink.com)

[Having a MELI APP created](http://www.somelink.com)

[Getting an access token (authentication)](http://www.somelink.com)


List your real estate property 	{#publish}
---------------------------------

We have developed our APIs based on a <a href="http://en.wikipedia.org/wiki/Representational_state_transfer" target="_blank"> REST architecture</a> via HTTP requests in a <a href="http://en.wikipedia.org/wiki/Json" target="_blank">JSON format</a>.

Available REST operations for our APIs are: GET, POST, PUT & DELETE.

You can list a real estate property by sending a POST request to our Items API with the following JSON:

{% highlight javascript %}

{ 
  "site_id": "SOME_SITE_ID",
  "title": "Property title",
  "category_id": "SOME_MELI_CATEGORY_ID",
  "price": 500,
  "currency_id": "ARS",
  "available_quantity": 1,
  "buying_mode": "classified",
  "listing_type_id": "SOME_MELI_LISTING_TYPE",
  "condition": "not_specified",
  "pictures": [
    {
      "id": "SOME_MELI_PICTURE_ID"
    },
    {
      "source":"SOME_PICTURE_URL"
    }
  ],
  "seller_contact": {
    "contact": "Contact name",
    "other_info": "Additional contact info",
    "area_code": "011",
    "phone": "4444-5555",
    "area_code2": "",
    "phone2": "",
    "email": "contact-email@somedomain.com",
    "webmail": ""
  },
  "location": {
    "address_line": "My property address 1234",
    "zip_code": "1111", <-- Mostly used Mexico and Brazil.
    "neighborhood": {
      "id": "SOME_MELI_NEIGHBORHOOD_ID"
    },
    "latitude": -34.48755,
    "longitude": -58.56987,
  },  
  "attributes": [
    {
      "id": "SOME_MELI_ATTR_ID",
      "value_id": "SOME_MELI_ATTR_VALUE"
    },
    {
      "id": "OTHER_MELI_ATTR_ID",
      "value_id": "OTHER_MELI_ATTR_VALUE"
    }
  ],
  "description" : "<b>This is the real estate property descritpion.</b>"
}
{% endhighlight %}

To complete the JSON with the necessary info, follow this steps:

- 1\. Pictures upload (optional)
- 2\. Category selection
- 3\. Attributes selection
- 4\. Location selection
	
	
### Putting together the publication JSON ###	{#puttingtoghetherJSON}

Once all the info is gathered, you will have to POST the JSON to our Items API.

A real estate property JSON is composed by the following information (an example is provided below the table):

<!-- ### JsonFieldsTable {#JsonFieldsTable} -->

Field				  |	Description
----------------------|----------------------------------------------------------------------------------------------------------
site_id\*			  |	ID of the site your user belongs to. Obtained in the [Category selection section](#categselection).
title\*				  |	Title of your listing.
category_id\*		  |	ID of the chosen category for your listing. Obtained in the [Category selection section](#categselection).
price\*				  |	Price of the property. Always send a real price, otherwise your listing will be removed.
currency_id\*		  |	Currency of the price. Allowed currencies vary according to your user's country. You can obtain all available currency options at https://api.mercadolibre.com/sites. Click on your Site ID and you will be now able to get the currencies element with all the available currencies and their IDs.
available_quantity\*  |	Available quantity of the property (generally 1)
buying_mode\*		  |	For real estate properties, always send a "classified" value.
listing_type_id\*	  |	Indicates the listing type for the listing. Possible values are "silver", "gold" or "gold_premium". If you have a promotional pack, keep in mind that you must have available items for the desired listing type.
condition\*			  |	Possible values: "new", "used" or "not_specified".
pictures\*			  |	You can provide either the Picture IDs of your uploaded pictures (if you have uploaded any) as well as the URLs	of the pictures you wish to upload (if you have them on an accesible web URL). - Check out the example. Both options are shown. -
location\*			  |	Location of the property, with the information gathered in the [Location selection section](#locationselection). If you have geolocation information (lat & long) you can add them here too. This will enable a map with the location, which will give your listings a higher quality.
seller_contact\*	  |	Seller's contact information. The email sent for this field will be the email used for sending the contact forms sent by users. If this email is not sent in the "seller_contact" field, the email used will be the publishing user's registered email address.
attributes\*		  |	Attributes of the property obtained the [Attributes selection section](#attrsselection).
description			  |	(optional) You can include a description with additional information of your property. HTML format supported. Just make sure the description sent does not violate our terms & conditions. Max width for an HTML description is 918px.

\*mandatory fields

JSON example:

{% highlight javascript %}

{ 
  "site_id": "MLA",
  "title": "Property title",
  "category_id": "MLA52745",
  "price": 500,
  "currency_id": "ARS",
  "available_quantity": 1,
  "buying_mode": "classified",
  "listing_type_id": "silver",
  "condition": "not_specified",
  "pictures": [
    {
      "id": "MLA2096545948_102011"
    },
    {
      "source":"http://media.point2.com/p2a/htmltext/f2a4/590f/3627/f49be256595a86c91457/original.jpg"
    }
  ],
  "seller_contact": {
    "contact": "Contact name",
    "other_info": "Additional contact info",
    "area_code": "011",
    "phone": "4444-5555",
    "area_code2": "",
    "phone2": "",
    "email": "contact-email@somedomain.com",
    "webmail": ""
  },
  "location": {
    "address_line": "My property address 1234",
    "zip_code": "1111",
    "neighborhood": {
      "id": "TUxBQlBBUzgyNjBa"
    },
    "latitude": -34.48755,
    "longitude": -58.56987,
  },  
  "attributes": [
    {
      "id": "MLA50547-AMBQTY",
      "value_id": "MLA50547-AMBQTY-1"
    },
    {
      "id": "MLA50547-ANTIG",
      "value_id": "MLA50547-ANTIG-A_ESTRENAR"
    },
    {
      "id": "MLA50547-MTRS",
      "value_name": "500"
    },
    {
      "id": "MLA50547-SUPTOTMX",
      "value_name": "2000"
    },
    {
      "id": "MLA50547-BATHQTY",
      "value_id": "MLA50547-BATHQTY-1"
    },
    {
      "id": "MLA50547-DORMQTYB",
      "value_id": "MLA50547-DORMQTYB-3"
    },
    {
      "id": "MLA50547-EDIFIC",
      "value_id": "MLA50547-EDIFIC-CHALET"
    }
  ],
  "description" : "<b>This is the real estate property descritpion.</b>"
}
{% endhighlight %}

### Sending the JSON to the API ### {#sendjson}

Once you have the JSON, you can validate your listing by sending it in a POST request body to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/items/validate?access_token=YOUR_ACCESS_TOKEN
</pre>

In the request headers include:
<pre class="terminal">
 content-type: application/json
 accepts: application/json
</pre>
If the response status code is "200 OK" or "204 No content", then the JSON was successfully validated and your property is ready to be listed.

Note: this validation process is not mandatory, but will most likely become handy when testing your APP. Keep in mind that there is no sandbox nor pre-production environment, so every property listed during your testing phase will be visible in our platform by all of our users. It is highly reccomended that you [finalize listed items](#finalize) posted while testing.

To list an item, POST the property JSON to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/items?access_token=YOUR_ACCESS_TOKEN
</pre>

If the property was successfully listed, you will receive a "201 Created" response status and all of the created item information in the response body (JSON formatted). <u>It is highly recommended that you track the <b>Item ID</b> received</u> (ie: MLA12345678), since you will be needing it later on when modifying or finalizing it.

Note: after successfully listing an item, its status will be "not yet active" until it passes our security filters and automatically gets activated. This process should take no longer than an hour.

**Congratulations! You have successfully finished the publication process of a real estate property using our APIs.**

If you were to receive an error status code on a response when communicating with our APIs, in most cases you will be able to determine the cause of the error by looking at the response body. In addition to the response status code, the response body will also contain detailed information regarding the error and will most likely help you understand how to solve different issues.

You can now follow the instructions to:

Modify, pause or finalize your property publication
Relist your properties

Don't hesitate to contact us for further assistance, comments and feedback about this tutorial, etc. at <a href="mailto:developers_re@mercadolibre.com" target="_blank">developers_re@mercadolibre.com</a>. We will get back to you as soon as possible!