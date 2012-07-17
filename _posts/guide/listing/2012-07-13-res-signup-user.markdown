---
layout: 2columns
title: Real estate listing
categories: guides-res
tags: signup-user
---

#Real estate listing

How to sign up a MELI user {#signUp}
---------------------------

To accomplish this go to the following URL:

<a href="http://www.mercadolibre.com" target="_blank">http://www.mercadolibre.com</a>

Once there, click on the country you want to operate in and then click on the "Reg&iacute;strate" button, as shown on figure 1.

![Register](/images/new-realestate-1.png){:style="width:700px;"}
*<center>figure 1</center>*

Complete the on screen fields and you will receive a confirmation email to activate your account.


Complete the required additional information  {#additionalinfo}
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

**Congratulations! Your user is now allowed to list in MercadoLibre.**


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