---
layout: 2columns
title: Javascript SDK
categories: guides
tags: SDKs
---


#Javascript SDK

The JavaScript SDK enables you to access the API from a Web Browser.
It  hides all the complexity of OAuth 2.0 and lets you focus on writing application code.

Just include the following source script in your application
	
	<script src="http://static.mlstatic.com/org-img/sdk/mercadolibre-1.0.1.js"></script>

For https use: 

    <script src="https://a248.e.akamai.net/secure.mlstatic.com/org-img/sdk/mercadolibre-1.0.1.js"></script>
	
Initialize the API with your client_id as follows:

{% highlight javascript %}
MELI.init({client_id: 6586});
{% endhighlight %}
	

That's it. Afterwards, this line of code will show the First Name of your registration in MELI:

{% highlight javascript %}
MELI.get(
  "/users/me",{},
    function(data) { alert("Hello "+data[2].first_name) }
);
{% endhighlight %}

Under the hood, the JSSDK checks that:
- You are actually you
- The app “melidev” (client_id #6586 in this example) is the actual caller
- You authorized the app “melidev” to access your data
    
If you want to contribute or you find something that needs to be fixed, just fork our SDK in [GitHub](https://github.com/mercadolibre/mercadolibre.js) and pull requests as needed or get in touch
through our [contact](/discuss) page
