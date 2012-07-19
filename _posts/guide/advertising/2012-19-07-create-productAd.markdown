---
layout: 2columns
title: Create a Product Ad 
categories: guides
tags: Advertising
---

# Create a Product Ad
There are two different ways to create a Product Ad. 

## Sending the image encoded
One ways of creating a product Ad is to send the encoded bytes of an image with the "fileInput" attribute in the request.

<pre class="terminal">
curl -i -H "X-Caller-Scopes: mclics_admin"  -H "Content-Type: application/json" -X POST -d '
{
	"campaignID":"39003",
	"adDailyBudget":"1",
	"name":"Default",
	"siteID":"MLA",
	"custID":"66258610",
	"title":"prueba de productAd REF2",
	"URLDestiny":"http://www.google.com",
	"URLVisible":"http://www.google.com",
	"maxCPC":"0.15",
	"image":"prueba.jpg",
	"categID":"1652", "refFrom":"Prueba",
	"refID":"prueba",
	"fileInput":"/9j/4AAQSkZJRgABAQEASABIAAD/4QCARXhpZgAASUkqAAgAAAAEABoBBQABAAAAPgAAABsBBQABAAAARgAAACgBAwABAAAAAgAAAGmHBAABAAAATgAAAAAAAABIAAAAAQAAAEgAAAABAAAAAwAAkAcABAAAADAyMTAAoAcABAAAADAxMDABoAMAAQAAAP//AAAAAAAA/9sAQwACAgICAgICAgICAwICAgMEAwICAwQFBAQEBAQFBgUFBQUFBQYGBwcIBwcGCQkKCgkJDAwMDAwMDAwMDAwMDAwM/9sAQwEDAwMFBAUJBgYJDQsJCw0PDg4ODg8PDAwMDAwPDwwMDAwMDA8MDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwM/8AAEQgAFAAcAwERAAIRAQMRAf/EABkAAAMAAwAAAAAAAAAAAAAAAAMFBgAHCf/EACgQAAICAgIBAQgDAAAAAAAAAAECAwQFEQAGElEHExYhMUGV1CJCUv/EABoBAAIDAQEAAAAAAAAAAAAAAAIEAAUGAQP/xAArEQACAQIDBgYDAQAAAAAAAAABAgMEEQAhMQUSQVFhYhMVIkJxkxQy0lL/2gAMAwEAAhEDEQA/AOveM6UbiZDs1eBM7Zt5fLjJYPIzOElWHIWYkNWbe4XCIB4tuM6/odtzCU2xfEVqlQJCZJN5HJztIwG43tNgBY3Q9v7Y19RtXwytOx3AEj3WUDK6KTvL7hc6izDu0xQYKr7L+wUJchUo1IFpx+9yMFqRonrqN/yl3Jrw+R04JRh81Yjj9DFsiriMiKosLsCbFepztbkwJU6gkYSq5dp00gRmJubAgXDfGWvafUOIGE9fB9f7k1qv1PGVqGHqze4v9nk8mmZ/FX8Kdd2+6uCJZR46IKpIDviaUNLtIstIgWMGzSG99AbRqTyIO+4tndVcZ4ZerqKABqlyzkXCcOV3YdQfSufAlTli59nlJMbg7uMryzSVsZmMlVqmxK8sgjisuqgu5JPLrYFOIadolJISR1FySbBjxxWbZk8WZZCBdkQmwsLlRwxJYCWTsdK31OjK0VCDL5l+3X0JUrFJlLTJRjYfSSZTtyPmkfoXQ8q6BmrIzSobKJJfFYcjK9owf9OP2/ynVlOH6xRSuKlx6ikfhjqI1u56Lw5t0U42Vd6x17Itj2v4WnZOK8Rjw8KERKuvFFGteIIBC/TYB1sDmjm2bSzbm/Gp3P1uBl0+OmlwDqBiiir6iLe3HYb2uevX5665nnhTnqljE3F7ZiIGsTQxrF2HFRDbXaabIZF+80Gyyf6XyT7qVVr4Xp5Py4RcgWdR70HEd6arzF14izNHKsyfjSmwJujH2N17W0bkbNwNxdAt1sjicnepWI7NO5m8nNVsRnavG9l2VlPoQeBsKdJYXkT1K0khB5gscHtmJopUR8mEaAjkd0YMehdYWSzPFVt1nv2JbVta2RvV0eaYl5H8Ip0UFmOzoc9fIaQMzAMCxLGzuoudTZWAz+MAu16kgKSpsABdEJsNBcqTlgvwL170yf5fJfs855LTd/2Sf3gfOKjs+uP+cZ8C9e9Mn+XyX7PJ5LTd/wBkn94nnFR2fXH/ADhzg8Hi8BQXG4isadKOSSURCR5CXlYyOzNIzMSzMSSTx6joYaOPw4VstydScybk3JJzOE6qplq38SVrtYDgNNMhYY//2Q==",
	"price":"15"
}'
https://api.mercadolibre.com/mclics/productAd?access_token=$ACCESS_TOKEN  
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
		"refFrom":"Prueba",
		"refID":"prueba",
		"siteID":"MLA",
		"status":"A",
		"title":"Prueba De Productad Ref4",
		"type":"P",
		"URLDestiny":"http://www.google.com",
		"URLVisible":"www.google.com",
		"fileInput":"/9j/4AAQSkZJRgABAQEASABIAAD/4QCARXhpZgAASUkqAAgAAAAEABoBBQABAAAAPgAAABsBBQABAAAARgAAACgBAwABAAAAAgAAAGmHBAABAAAATgAAAAAAAABIAAAAAQAAAEgAAAABAAAAAwAAkAcABAAAADAyMTAAoAcABAAAADAxMDABoAMAAQAAAP//AAAAAAAA/9sAQwACAgICAgICAgICAwICAgMEAwICAwQFBAQEBAQFBgUFBQUFBQYGBwcIBwcGCQkKCgkJDAwMDAwMDAwMDAwMDAwM/9sAQwEDAwMFBAUJBgYJDQsJCw0PDg4ODg8PDAwMDAwPDwwMDAwMDA8MDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwM/8AAEQgAFAAcAwERAAIRAQMRAf/EABkAAAMAAwAAAAAAAAAAAAAAAAMFBgAHCf/EACgQAAICAgIBAQgDAAAAAAAAAAECAwQFEQAGElEHExYhMUGV1CJCUv/EABoBAAIDAQEAAAAAAAAAAAAAAAIEAAUGAQP/xAArEQACAQIDBgYDAQAAAAAAAAABAgMEEQAhMQUSQVFhYhMVIkJxkxQy0lL/2gAMAwEAAhEDEQA/AOveM6UbiZDs1eBM7Zt5fLjJYPIzOElWHIWYkNWbe4XCIB4tuM6/odtzCU2xfEVqlQJCZJN5HJztIwG43tNgBY3Q9v7Y19RtXwytOx3AEj3WUDK6KTvL7hc6izDu0xQYKr7L+wUJchUo1IFpx+9yMFqRonrqN/yl3Jrw+R04JRh81Yjj9DFsiriMiKosLsCbFepztbkwJU6gkYSq5dp00gRmJubAgXDfGWvafUOIGE9fB9f7k1qv1PGVqGHqze4v9nk8mmZ/FX8Kdd2+6uCJZR46IKpIDviaUNLtIstIgWMGzSG99AbRqTyIO+4tndVcZ4ZerqKABqlyzkXCcOV3YdQfSufAlTli59nlJMbg7uMryzSVsZmMlVqmxK8sgjisuqgu5JPLrYFOIadolJISR1FySbBjxxWbZk8WZZCBdkQmwsLlRwxJYCWTsdK31OjK0VCDL5l+3X0JUrFJlLTJRjYfSSZTtyPmkfoXQ8q6BmrIzSobKJJfFYcjK9owf9OP2/ynVlOH6xRSuKlx6ikfhjqI1u56Lw5t0U42Vd6x17Itj2v4WnZOK8Rjw8KERKuvFFGteIIBC/TYB1sDmjm2bSzbm/Gp3P1uBl0+OmlwDqBiiir6iLe3HYb2uevX5665nnhTnqljE3F7ZiIGsTQxrF2HFRDbXaabIZF+80Gyyf6XyT7qVVr4Xp5Py4RcgWdR70HEd6arzF14izNHKsyfjSmwJujH2N17W0bkbNwNxdAt1sjicnepWI7NO5m8nNVsRnavG9l2VlPoQeBsKdJYXkT1K0khB5gscHtmJopUR8mEaAjkd0YMehdYWSzPFVt1nv2JbVta2RvV0eaYl5H8Ip0UFmOzoc9fIaQMzAMCxLGzuoudTZWAz+MAu16kgKSpsABdEJsNBcqTlgvwL170yf5fJfs855LTd/2Sf3gfOKjs+uP+cZ8C9e9Mn+XyX7PJ5LTd/wBkn94nnFR2fXH/ADhzg8Hi8BQXG4isadKOSSURCR5CXlYyOzNIzMSzMSSTx6joYaOPw4VstydScybk3JJzOE6qplq38SVrtYDgNNMhYY//2Q==",
		"image":"prueba.jpg",
		"price":"15"
	}
}
{% endhighlight %}

## Sending the URL of the image
The other way of doing this is sending the image URL in you request. The API will download and store it in ower own image repository. In order to do this you need to pass de image URL with the "image_URL" attribute.

<pre class="terminal">
curl -i -H "X-Caller-Scopes: mclics_admin"  -H "Content-Type: application/json" -X POST -d '
{
	"campaignID":"39003",
	"adDailyBudget":"1",
	"name":"Default",
	"siteID":"MLA",
	"custID":"66258610",
	"title":"prueba de productAd REF2",
	"URLDestiny":"http://www.google.com",
	"URLVisible":"http://www.google.com",
	"maxCPC":"0.15",
	"image":"exampleImage.jpg",
	"categID":"1652", 
	"refFrom":"Reference owner",
	"refID":"Reference ID",
	"image_URL": "http://www.imagestores.com/exampleImage.jpg,
	"price":"15"
}'
https://api.mercadolibre.com/mclics/productAd?access_token=$ACCESS_TOKEN  
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
		"image_URL": "http://www.imagestores.com/exampleImage.jpg,
		"title":"Prueba De Productad Ref4",
		"type":"P",
		"URLDestiny":"http://www.google.com",
		"URLVisible":"www.google.com",
		"image":"prueba.jpg",
		"price":"15"
	}
}
{% endhighlight %}

**Congratulations!** you have performed your first product Ad using the MELI APIs.
