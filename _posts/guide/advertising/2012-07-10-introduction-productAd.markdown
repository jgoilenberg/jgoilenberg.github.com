---
layout: 2columns
title: Introduction to Product Ads
categories: guides
tags: Advertising
---

# Product Ads Introduction
As you know, MercadoClics is a platform in which users can create Ads. This tutorials are going to show you, developer, how mange your product Ads using the ProductAds API.
## What is a Product Ad?{#what-is-a-product-ad}
Product Ads are a new kind of banner with the characteristic of which is shown with an explicit price and image.

### Attributes
* **adID**: Id of the productAd
* **custID**: Id of the customer
* **name**: Name of the customer
* **maxCPC**: max value for the PPC (Pey per click)
* **adDailyBudget**: Daily budget of the productAd
* **status**: Ad status
* **title**: Ad’s title
* **URLVisible**: visible URL by the final user
* **URLDestiny**: Real destiny URL
* **campaignID**: Id of the campaign
* **siteID**: Id of the site
* **categID**: Id of the category for the productAd
* **refID**
* **refFrom**

## Reference
You will notice that there are two different refence attributes: **refID**, **refFrom**. With this attributes you will be able to find all the product Ads you have associate to your product. To know more about this feature you can read [Search a Product Ad](../searching-productAd).

## Other considerations{#other-considerations}
The ProductAds API tutorials require a basic understanding of the curl Linux command, you can get information of how to use it in our Basic Curl Tutorial.
In order to use this API, you will need an access_token, we recommends that you read the [Authorization Tutorial](../authentication-and-authorization).
