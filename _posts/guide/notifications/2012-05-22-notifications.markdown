---
layout: 2columns
title: What are the Notifications?
categories: guides
tag: Notifications
---

#Notifications

Listening to Notifications give you the ability to have a real-time feed of the changes that occur on the different resources of the MercadoLibre platform.
If you published an item and it has been paused because or someone made you a question, purchase your item or even paid for it and requested a shipping, you will receive a Notification.
Notifications are a very convenient way of stay up-to-date with everything that you care, in a very efficient way for your app, without having to query our APIs on a constant basis.


## Table of Contents 
- [How to Subscribe](#how-to-subscribe)
- [Available Topics](#topics)
- [Considerations](#considerations)
- [Structure of Notifications](#structure)
+ [Purchase](#purchase)
+ [Payment](#payment)
+ [Feedback](#feedback)
+ [Questions](#questions)


---
##How do I subscribe to the Notifications? {#how-to-subscribe}
In the Applications Page where you created your App, you can edit the details and specify which 'topics' you will listen to.
(see [Applications Page](http://applications.mercadolibre.com.ar/home)).
_If you haven't created your App yet go to [Creating your app section] (http://developers.mercadolibre.com/creating-your-own-application/)_

  - **Notifications callback URL** Configure the public URL of your domain where you want to receive notifications for the different topics. e.g.: “http://myshoes-app.com/callbacks”.

  - **Topics** Comma separated list of 'topics' you want to subscribe to.

###Available Topics: {#topics}
- **orders**  — To get notified of any 'news' on an order. e.g.: you received an order from a purchase, the buyer added shipping instructions or the buyer added a payment to an order.

- **items**   — To get notified of any changes on an item you have published. 
	e.g.: Due to infringement of one of MercadoLibre's rules your item was set to 'under_review' and paused. 
	The seller changed any of an item's attribute (price, title, description) and all the application's subscribed to that seller's feed get notified of the change.
	The 60 days period of a listing finished.

- **questions**   — To receive a notification for every question made to you or answered.

> NOTE: All the applications subscribed to the question feed will receive notifications for every answer the seller sends.


###Considerations receiving notifications: {#considerations}
* Messages will be sent out and retried during 12 hours. After that period, if not accepted by the app, they will be discarded.

* Your application must acknowledge the reception with an HTTP status code 200, otherwise the message will be considered not delivered and it will be retried.

* Your application must send a response within 20 seconds, otherwise it will timeout considered not delivered and retried.

##Structure of the notifications {#structure}

##Order

###Purchase {#purchase}
When somebody purchase one of your items on sale, there is a notification with the buyer's details, the amount purchased, the item and so on.

{% highlight javascript %}
{
  "id":
  "seller":{
     "id":
     "nickname":
     "first_name":
     "last_name":
     "email":
     "phone":{
        "area_code":
        "number":
        "extension":
     }
  },
  "buyer":{
     "id":
     "nickname":
     "first_name":
     "last_name":
     "email":
     "phone":{
        "area_code":
        "number":
        "extension":
     }
     "billing_info":{
        "doc_type":
        "doc_number":
     }
  },
  "order_items":[
     {
        "item":{
            "id":
            "title":
        }
        "quantity":
        "unit_price":
        "currency_id":
        "variation_id":
        "variation_attributes":
     }

{% endhighlight %}


###Payments {#payment}
When the buyer pays the order using MercadoPago, an additional notification is generated with the payment details, associated to the order.

{% highlight javascript %}
   {
   "site_id":"MLA",
   "date_created":"2012-05-22T00:03:02-04:00",
   "date_approved":"2012-05-22T00:03:02-04:00",
   "order_id":"192687833",
   "date_last_updated":"2012-05-22T00:12:19-04:00",
   "collector_id":9883470,
   "payer_id":102456103,
   "reason":"Casio Ef-527bk-1av Edifice Chronograph Mens Watch Ef527bk",
   "transaction_amount":840.0,
   "currency_id":"ARS",
   "total_paid_amount":840.0,
   "shipping_cost":0.0,
   "status":"approved",
   "status_detail":"accredited",
   "marketplace":"MELI",
   "operation_type":"regular_payment"
   }
{% endhighlight %}

###Feedback {#feedback}
When the buyer rates the seller after the transaction is concluded or the seller rates a buyer.

{% highlight javascript %}
  {
   "item":{
      "id":"MLB227638289",
      "seller_id":74441846
   },
   "from":74441846,
   "to":105185078,
   "date_created":"2012-05-20T22:35:42-04:00",
   "date_last_updated":"2012-05-22T00:12:04-04:00",
   "fulfilled":false,
   "reason":"THEY_DIDNT_ANSWER",
   "rating":"negative",
   "status":"active",
   "message":"O usuário deu o lance, mas não efetuou o pagamento. Assim não concretizando a compra,",
   "visibility_date":"2012-05-22T00:11:58-04:00",
   "reply":null,
   "reply_status":"",
   "reply_date":null
  }
{% endhighlight %}

## Questions {#questions}

{% highlight javascript %}
  {
   "id":12154656,
   "date_created":"2012-05-20T22:35:42-04:00",
   "item_id":"MLB425068299",
   "seller_id":123456,
   "status":"answered",
   "text":"OLÁ.. QUANTO FICA SEDEX PARA O CEP 83601-100? QUANTO TEMPO DE GARANTIA?OBRIGADO",
   "answer": {
      "date_created":"2012-05-21T22:35:42-04:00",
      "status":"active",
      "text":"Olá boa tarde, o valor do frete para todo o estado de PR é de R$ 35,00, via Sedex com seguro incluso, para cada unidade adquirida, este produto possui garantia de fabricação de um mês, o mesmo não é coberto em caso de mau uso como riscos, quedas, líquidos e etc. Nosso prazo de entrega é de dois dias úteis após a confirmação do seu pagamento. Aguardamos seu pedido. Obrigado."
   }
  }
{% endhighlight %}


