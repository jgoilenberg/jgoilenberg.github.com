---
layout: 2columns
title: Real estate listing
categories: guides
tags: Selling
---

use_numbered_headers: true

#Real estate listing

The purpose of this tutorial is to provide a full guide on how to list real estate items using the MELI APIs platform. 

* * *

Table of contents: 

* This list will contain the toc (it doesn't matter what you write here)
{:toc}

* * *


About MercadoLibre's APIs. REST & JSON 		{#about}
--------------------------------------
We have developed our APIs based on a <a href="http://en.wikipedia.org/wiki/Representational_state_transfer" target="_blank"> REST architecture</a> via HTTP requests in a <a href="http://en.wikipedia.org/wiki/Json" target="_blank">JSON format</a>.

Available REST operations for our APIs are: GET, POST, PUT & DELETE.

Any REST Client can be used to send a request to a MercadoLibre API.

Requests must be sent to a specific URL and contain certain headers (depending on the API). A message in a JSON format must be sent in the request body (except on GET requests).

**If you were to receive an error status code on a response when communicating with our APIs, in most cases you will be able to determine the cause of the error by looking at the response body. In addition to the response status code, the response body will also contain detailed information regarding the error and will most likely help you understand how to solve different issues.**


Sign up 	{#signup}
-------
The first step to list a real estate property, you must sign up to obtain a MercadoLibre user in the country you will be operating in. To accomplish this go to the following URL:

<a href="http://www.mercadolibre.com" target="_blank">http://www.mercadolibre.com</a>

Once there, click on the country you want to operate in and then click on the "Reg&iacute;strate" button, as shown on figure 1.

![Register](/images/new-realestate-1.png){:style="width:700px;"}
*<center>figure 1</center>*

Complete the on screen fields and you will receive a confirmation email to activate your account.


Complete the required additional information 	{#additionalinfo}
--------------------------------------------

Make your user available for listing using MercadoLibre's APIs by completing some additional information (documentation, location, etc.). To accomplish this go to the following URL:

<a href="http://www.mercadolibre.com" target="_blank">http://www.mercadolibre.com</a>

Once there, click on the country you have signed up in and click on the "Vender" button, as shown on figure 2.

![Sell](/images/new-realestate-2.png){:style="width:700px;"}
*<center>figure 2</center>*

A modal window will be displayed in which you will be required to complete some additional information, similar to what is shown in figure 3.

![Additional Info](/images/new-realestate-3.png){:style="width:700px;"}
*<center>figure 3</center>*

After completing this information, choose any listing category and click on the "Continuar" button. Nothing further is required for this step. If you successfully reach the next listing step you are good to go.

Congratulations! Your user is now allowed to list in MercadoLibre.


Identify as a Real Estate Agency 	{#identifyasagency}
------------------------------------------------

If you are a real estate agency, you can identify your user as such to gain access to our promotional real estate packs. To accomplish this access the Help section, as shown on figure 4.

![Help](/images/new-realestate-4.png){:style="width:700px;"}
*<center>figure 4</center>*

Once there, click on the "Tus datos y registraci&oacute;n" tab and then on the "Registrarme como inmobiliaria" link, as shown on figure 5.

![Personal info](/images/new-realestate-5.png){:style="width:700px;"}
*<center>figure 5</center>*

You will the be redirected to a form which must be filled with the proper information and you will also be able to choose your desired promotional package. After completing the form, one of our agents will get in touch with you.

Keep in mind that having a promotional pack <u>is not mandatory</u> for publishing using the APIs.

If you have indeed acquired a promotional pack for your agency, you can access it's information by sending a GET request to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/users/me/promotion_packs?access_token=YOUR_ACCESS_TOKEN
</pre>

*YOUR_ACCESS_TOKEN* is the key that will allow you to authenticate when using MercadoLibre's APIs. You will learn how to obtain the access token on the [Authenticate section](#authenticate).

If you wish to see detailed information regarding your promotional pack, you can do so by sending a GET request to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/users/me/promotion_pack_combos/YOUR_PACKAGE_ID?access_token=YOUR_ACCESS_TOKEN
</pre>

*YOUR_PACKAGE_ID* is the id of the package obtained in the previous step.
*YOUR_ACCESS_TOKEN* is the key that will allow you to authenticate when using MercadoLibre's APIs. Once agagin, you will learn how to obtain the access token on the [Authenticate section](#authenticate).


Create your MercadoLibre APP 	{#createapp}
----------------------------
In order to list using MercadoLibre's APIs, you must first create an APP within MercadoLibre. To accomplish this go to the following URL:

<a href="http://applications.mercadolibre.com.ar" target="_blank">http://applications.mercadolibre.com.ar</a>
(if you are accesing with a user belonging to another country other than Argentina, please change the ".com.ar" to your corresponding country extension).

Log in with your username and password and click on the "Create new application", as shown on figure 6.

![Create new app](/images/new-realestate-6.png){:style="width:700px;"}
*<center>figure 6</center>*

If your APP will list properties **only on behalf your registered user**, then complete the fields in the form, checking both "read" and "write" scopes and click on the "Create application" button (you can complete the "Callback URL" with any data, it won't be used). However, **if you want your APP to list properties on behalf other users**, then at this step you must complete the fields in the form, checking the "read", "write" and "offline_access" scopes, and in the Callback URL will have to be completed with a URL to which users will be redirected right after granting permissions to your APP, explained further ahead in the [Authenticate section](#authenticate).

If your app has been successfully created, you should be now seeing all of the app's details on screen, as shown on figure 7.

![Apps details](/images/new-realestate-7.png){:style="width:700px;"}
*<center>figure 7</center>*

The most important fields you will be using along this listing steps are the *Client ID* (shown on screen as "ID") and your app's *Secret Key*. Keep both at hand since you will be needing them later on for authentication. Make sure you keep this information protected.


Authenticate	{#authenticate}
------------
MercadoLibre's APIs work with the <a href="http://en.wikipedia.org/wiki/Oauth" target="_blank">OAuth authentication protocol</a>.

There are certain actions that require you to identify as a MercadoLibre user (ie: listing a real estate property). To successfully accomplish this actions, you must get an access token that will allow you to identify your user when interacting with the APIs, for a determined amount of time (after which you will have to get a new access token).

### Getting an access token for your registered user ### {#accesstokenregistereduser}

If your APP will list properties **only on behalf your registered user**, then follow the following steps to get an access token. However, **if you want your APP to list properties on behalf other users**, then follow the steps in the [Getting an access token for other users section](#accesstokenotherusers).

To get an access token you must send a POST request to the following URL:

<pre class="terminal">
https://api.mercadolibre.com/oauth/token?grant_type=client_credentials&client_id=YOUR_CLIENT_ID&client_secret=YOUR_SECRET_KEY
</pre>

*YOUR_CLIENT_ID* and *YOUR_SECRET_KEY* can be obtained from the MercadoLibre APP you've created.

In the request headers include:

<pre class="terminal">
accepts: application/json
content-type: application/x-www-form-urlencoded
</pre>

You will receive a response body in a JSON format with the following layout:
{% highlight javascript %}
{ 
	"access_token":"YOUR_NEW_ACCESS_TOKEN",
	"token_type":"bearer",
	"expires_in":10800,
	"scope":"read write",
	"refresh_token":1
}
{% endhighlight %}


*YOUR_NEW_ACCESS_TOKEN* is now the access token required to interact with the APIs to list a real estate property. Keep in mind that this token will expire after the "expires_in" amount of seconds. Once expired your access token will no longer be valid and you will have to send a new request to the OAuth API to get a new access token.


### Getting an access token for other users ### {#accesstokenotherusers}

If your APP will list properties **on behalf other users**, then follow the following steps to get an access token. However, **if you want your APP to list properties only on behalf your registered user**, then follow the steps in the previous [Getting an access token for your registered user section](#accesstokenregistereduser).

Users on whose behalf you wish to list properties will have to grant permissions to allow your APP do so. This permission granting will only be needed once per user. To accomplish this, the user who wants to grant this permission must access the following URL:

<pre class="terminal">
 https://auth.mercadolibre.com.ar/authorization?response_type=code&client_id=YOUR_CLIENT_ID
</pre>

*YOUR_CLIENT_ID* can be obtained from the MercadoLibre APP you've created.

Note: if you are accesing with a user belonging to another country other than Argentina, please change the ".com.ar" to your corresponding country extension.

Once there, the user will have to login and grant permissions to your APP, as shown on figure 8.

![Grant](/images/new-realestate-8.png){:style="width:700px;"}
*<center>figure 8</center>*

Once the user grants permissions to your APP, it will be automatically redirected to the URL previously set up in the "Callback URL" when creating your APP (you can edit your APPs settings at any time in the same admin used for creating it), and this redirecting will also add a *CODE* to the URL. For instance, if your "Callback URL" was https://www.mydomain.com/mercadolibre.php, then the user will be redirected to:

<pre class="terminal">
 https://www.mydomain.com/mercadolibre.php?code=YOUR_SECRET_CODE
</pre>

*YOUR_SECRET_CODE* will be generated by MercadoLibre for security reasons.

When receiving a request to your "Callback URL", it must then send a POST request to our OAuth API to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/oauth/token?grant_type=authorization_code&client_id=YOUR_CLIENT_ID&client_secret=YOUR_SECRET_KEY&code=YOUR_SECRET_CODE&redirect_uri=CALLBACK_URL
</pre>

*YOUR_CLIENT_ID* and *YOUR_SECRET_KEY* can be obtained from the MercadoLibre APP you've created. *YOUR_SECRET_CODE* can be obtained from the params received and for the *CALLBACK_URL* you must send the exact same "Callback URL" set up for your APP.

In the request headers include:

<pre class="terminal">
accepts: application/json
content-type: application/x-www-form-urlencoded
</pre>

You will receive a response body in a JSON format with the following layout:
{% highlight javascript %}
{ 
	"access_token" : "YOUR_NEW_ACCESS_TOKEN",
	"token_type" : "bearer",
	"expires_in" : 10800,
	"refresh_token" : "YOUR_REFRESH_TOKEN",
	"scope" : "write read offline_access"
}
{% endhighlight %}

*YOUR_NEW_ACCESS_TOKEN* is now the access token required to interact with the APIs to list a real estate property on behalf the user who just granted permissions to your APP. Keep in mind that this token will expire after the "expires_in" amount of seconds. Once expired your access token will no longer be valid and you will have to get a new access token. To obtain from the second access token on, you will need *YOUR_REFRESH_TOKEN* and will have to send a POST request to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/oauth/token?grant_type=refresh_token&client_id=YOUR_CLIENT_ID&client_secret=YOUR_SECRET_KEY&refresh_token=YOUR_REFRESH_TOKEN
</pre>

This POST will then return a new valid access token and a new refresh token, which you will have to use for getting your next valid access token by sending a POST request to the last mentioned URL.

Finally, you will most likely will want to know to which MercadoLibre's user this access token belongs to (to store the user ID, access token and refresh token in your DB maybe). To accomplish this you must send a GET request to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/users/me?access_token=YOUR_NEW_ACCESS_TOKEN
</pre>

You will receive a response body in a JSON format from which you will be able to get all of the user's information.


List your real estate property 	{#publish}
---------------------------------

* Listing a real estate property requires the following steps:

- 1\. Pictures upload (optional)
- 2\. Category selection
- 3\. Attributes selection
- 4\. Location selection
- 5\. Putting together the publication JSON
- 6\. Sending the JSON to the Items API
	
	
### Pictures upload ###	{#picupload}

Pictures are optional when listing, but they make a big difference in the publication quality and results (visits and contacts), specially when talking about real estate properties. *<u>If you already have your pictures uploadad to an accesible web URL, you can then skip this picture uploading step</u> and send them directly as explained in the [Putting toghether the publishing JSON section](#puttingtoghetherJSON). However, if your pictures are stored locally, you will then have to upload them to our Pictures API, by sending a POST request to the following URL:
<pre class="terminal">
 https://api.mercadolibre.com/pictures?access_token=YOUR_ACCESS_TOKEN
</pre>
Remember *YOUR_ACCESS_TOKEN* is the necessary key to interact with cerain APIs, obtained in the previous [Authenticate section](#authenticate).

The request body is in this case a binary (instead of plain text), and the procedure varies according to the programming language you are working with.

The request sent must be a *multipart-mime* type and the content-type must also be specified, according to the image format you are uploading, such as:
<pre class="terminal">
 jpg: 'image/jpeg'
 png: 'image/png'
 gif: 'image/gif'
 svg: 'image/svg'
</pre>
Should you need to run some tests with this API, you can use the cURL command, as follows:

curl -F file=@<*LOCAL_PICTURE*> https://api.mercadolibre.com/sites/SITE_ID/pictures?access_token=YOUR_ACCESS_TOKEN

*LOCAL_PICTURE* is the path and file name of the picture you wish to upload.
*SITE_ID* is the ID of your country. You will see how to obtain this value in the next step (7.2 Category selection).

If the picture was sucessfully uploaded you will receive a JSON response body, which contains an "id" element. Save the Picture ID value for every picture you upload, since you will be needing them later on, when putting together the JSON for publishing the property.

*There is currently a maximum amount of fifteen pictures per property.*


### Category selection ###	{#categselection}

In this step you will have to choose the category in which your property will be listed. First, determine the "SITE_ID" that corresponds to the country your user belongs to. To accomplish this go to the following URL:

<a href="https://api.mercadolibre.com/sites" target="_blank">https://api.mercadolibre.com/sites</a>

Once there you will be able to determine your SITE_ID, which is the "id" for your corresponding country.

Now that you have your SITE_ID, you can now access the following URL:

**https://api.mercadolibre.com/categories/SITE_ID1459**

If your user belongs, for example, to Argentina, then the URL would be: <a href="https://api.mercadolibre.com/categories/MLA1459" target="_blank">https://api.mercadolibre.com/categories/MLA1459</a>

Once there, browse within the "children categories" element, according to the publication category you are interested in (you can do this by clicking the "id") <u>until you reach a leaf category</u>. You will know when you have reached a leaf category when you reach a category that has an empty "children_categories" array.

Save this Category ID, since you will be needing it later on, when putting together the JSON for publishing the property.


### Attributes selection ###	{#attrsselection}

When listing a property, its attributes will vary according to the chosen category. Now that you have your Category ID, you can see it's attributes by accessing the following URL:

**https://api.mercadolibre.com/categories/SITE_IDCATEGORY_ID/attributes**

If your user belongs, for example, to Argentina, and the chosen category was 1467, then the URL would be: <a href="https://api.mercadolibre.com/categories/MLA1467/attributes" target="_blank">https://api.mercadolibre.com/categories/MLA1467/attributes</a>

Once there, you will get a JSON response with as many elements as the amount of attributes belonging to the chosen category. For each attribute you get an id, type, tags and possible values. Consider the following:

> An attribute with the "tags" element containing "fixed" means that this attribute is indeed fixed, and you don't need to add it when putting toghether the property JSON.
> Attribute type "list" means you will have a list of the possible values, for which you will have to send the desired value **id**.
> Attribute type "boolean" means you will have two possible values (one for true, one for false), for which you will have to send the desired value **id**.
> Attribute type "string" with "tags" not containing "fixed" means you will have to send the desired value as text.
> Attribute with "tags" containing "required" means the attribute <u>is mandatory</u> when publishing the property.

For each attribute you choose to publish, save its Attribute ID and its value id as well. You will be needing them later on, when putting together the JSON for publishing the property. Keep in mind that required attributes are mandatory and vary between categories. Not sending the correct attributes when listing is a very common mistake.


### Location selection ###	{#locationselection}

Before putting together all of the gathered information so far, you will have to determine the property location, which includes state, city and in most cases neighborhood as well. To accomplish this access the following URL:

<a href="https://api.mercadolibre.com/classified_locations/countries" target="_blank">https://api.mercadolibre.com/classified_locations/countries</a>

Once there click on the country id your user belongs to and you will be redirected to a new page where you will be able to browse through the states of the selected country. By clicking the State ID you will be able to browse it's cities and the same applies for the neighborhoods. <u>You only need to send the leaf location id when publishing a property.</u> This means that sending only the Neighborhood ID is enough for our API to complete with the corresponding State and City IDs. If the chosen city does not have any neighborhood, then you will only need to send the City ID. Sending either the Neighborhood ID or the City ID is mandatory. If you were to send only a State ID, our API will not allow you to list the property.


### Putting together the publication JSON ###	{#puttingtoghetherJSON}

The last step before successfully listing a real estate property is putting together all of the gathered information plus some extra data detailed below, to obtain the resulting JSON you will have to POST to our Items API.

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
      "source":"http://farm3.staticflickr.com/2417/2176897085_946b7b66b8_b.jpg"
    },
    {
      "source":"http://farm2.staticflickr.com/1056/628680053_3b7c315548_b.jpg"
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


Modify, pause or finalize your property publication {#modify}
---------------------------------------------------

You can use our Items API to visualize the details of a property, by accessing the following URL:

**https://api.mercadolibre.com/items/ITEM_ID**

Example: https://api.mercadolibre.com/items/MLA12345678

### Modify your property ### {#modifsub}

Using our Items API you will be able to modify the same elements that you are currently able to modify when browsing our site with a browser, such as pictures, title, available quantity, price, attributes, etc. For security reasons, description cannot be modified, but you will find instructions on how to add new information to your description further ahead.

To modify a property, send a PUT request to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/items/ITEM_ID?access_token=YOUR_ACCESS_TOKEN
</pre>

In the request headers include:
<pre class="terminal">
 content-type: application/json
 accepts: application/json
</pre>

You must send a JSON formatted body with the elements you wish to modify.

Example:
{% highlight javascript %}
{ 
  "title": "Your new title",
  "price": 1000
}
{% endhighlight %}

Note: the JSON sent must not contain the Item ID.

If your property was successfully modified, you will receive a "200 OK" response status. Keep in mind that it can take some time to see the property's new information refreshed.

### Add new information to your property's description ### {#addtext}

To add new information to your property's description, you must send a POST request to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/items/ITEM_ID/descriptions?access_token=YOUR_ACCESS_TOKEN
</pre>

In the request body you must send:

{% highlight javascript %}
{
  "text": "You additional description text."
}
{% endhighlight %}

If the description was successfully posted, you will receive a "201 Created" status code. Keep in mind that it might take some minutes for you new description to be shown.

### Finalize, pause or reactive your publication ### {#finalize}

To accomplish this, the process is very similar to "Modify your property publication". All that is needed is a PUT request to our Items API with a change in the status of the item, to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/items/ITEM_ID?access_token=YOUR_ACCESS_TOKEN
</pre>

Possible values are:

- closed: finalizes your publication. Once closed, it cannot be reactivated again, but it can be relisted.
- paused: pauses your publication. Once paused, it will not be visible by other MercadoLibre's users, but it will not be closed and it can be reactivated later on.
- active: reactivates a previously paused item.


JSON example:
{% highlight javascript %}
{
  "status":"paused"
}
{% endhighlight %}
Note: the value passed in the "status" key is case sensitive and thus must be sent in lowercase.

Relisting your properties {#relist}
-------------------------

Real estate listings have an expiration date on MercadoLibre. This expiration date is usually two months since the activation date. Once an item has reached its expiration date, it will be automatically finalized and will no longer be visible to other users. When this ocurrs, you may choose to relist your property so that it becomes active again. Relisting implies the creation of a NEW item with the exact same elements as its parent.

For your APP development, you might want to add a process that checks your listings' expiration dates so as to finalize and relist your listings before they reach their expiration date. *Only items with a "closed" status admit relisting.* You can send a PUT request with a "closed" status at any time your item is "active" or "paused".

To check the current status and expiration date of a listing, you must send a GET request to our items API to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/items/ITEM_ID
</pre>

Once you've received the response body, check the "stop_time" element to get the expiration date of the property. This information is also available in the response body you receive when successfully listing the property in the first place.

To relist a property you must send a POST request to the following URL:

<pre class="terminal">
 https://api.mercadolibre.com/items/ITEM_ID/relist?access_token=YOUR_ACCESS_TOKEN
</pre>

Example: https://api.mercadolibre.com/items/MLA12345678/relist?access_token=YOUR_ACCESS_TOKEN

In the request headers include:
<pre class="terminal">
 content-type: application/json
 accepts: application/json
</pre>
In the request body you must send "price", "quantity" and "listing_type_id" for your relisting. Remember that the possible values for "listing_type_id" are "gold_premium", "gold" or "silver" (lowercase).

JSON example:

{% highlight javascript %}
{
  "price": 20000,
  "quantity": 1
  "listing_type_id": "silver"
}
{% endhighlight %}

If your property has been successfully relisted, you will receive a "201 Created" response status. Keep in mind that it might take some minutes before you see the item listed in our site.

Note: as stated before, relisting an item generates a NEW item, which means that the Item ID MercadoLibre assigns to that item will be a new one. You will be able to obtain it from the response body when successfully relisting your properties.

**Congratulations! You have successfully finished covering all the required steps of the publication process of a real estate property using our APIs.**

Don't hesitate to contact us for further assistance, comments and feedback about this tutorial, etc. at <a href="mailto:developers_re@mercadolibre.com" target="_blank">developers_re@mercadolibre.com</a>. We will get back to you as soon as possible!