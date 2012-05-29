---
layout: 2columns
title: Authentication & Authorization
categories: tutorials popular
tags: home
---

#Authentication & Authorization

Authentication gives your app the ability to know the identity of a MELI user, and to read and write data via MELI's APIs. The platform uses [OAuth 2.0](http://tools.ietf.org/pdf/draft-ietf-oauth-v2-12.pdf) for authentication and authorization.  
A successful authentication flow results in your application obtaining a user access token which can be used to make requests to MELI's APIs. 

### Table of Contents
- [Access token validity](#token-validity)
- [User login](#user-login)
- [Server side flow](#server-side-flow)
- [Client side flow](#client-side-flow)
- [Token refresh](#token-refresh)


##Access Token Validity & Expiration {#token-validity}

When you obtain an access token, it will be valid immediately and usable in requests to the API for some time period. After that period has elapsed, the access token is considered to have expired and the user will need to be authenticated again in order for your app to obtain a fresh access token. The duration for which a given access token is valid depends on how it was generated.

There are also events which may cause an access token to become invalid before its expected expiry time. Such events include the user changing their password, an application refreshing it's App Secret. Dealing with varying access token expiry times, and handling the case when an access token becomes invalid before its expected expiry time is essential for building robust social experiences.


## User Login {#user-login}
The MELI API supports two different authentication flows: server-side and client-side. The server-side flow is used whenever you need to call the API from your webserver. If you want to interact with the API from a desktop or mobile application you should use the client-side flow.
Regardless of the flow you use, our implementation of the OAuth 2.0 protocol involves three different steps: user authentication, app authorization and app authentication. User authentication ensures that the user is who he says he is, app authorization ensures that the user knows exactly what data and capabilllities they are providing to your app and app authentication ensures that the user is giving his information to your app and your app only. Once these steps are completed your app is issued an access token which you can use to access the user's information and take action on his behalf.


## Server-side flow {#server-side-flow}
User authentication and app authorization are handled at the same time by redirecting the user to our OAuth Dialog. When invoking this dialog, you must pass your client id that is generated when you create your application in our [Applications Portal](http://applications.mercadolibre.com.ar/home) (the client_id parameter) and the URL that the user's browser will be redirected to once app authorization is completed (the redirect_uri parameter).

The URL should look like this:   

	https://auth.mercadolibre.com.ar/authorization?response_type=code&client_id=Client_id&redirect_uri=REDIRECT_URL

When the user succesfully logged in a cookie will be stored on the user's computer. If the OAuth dialog is requested for a second time the dialog will not be shown but instead the cookie will be validated. When the dialog is shown the user is prompted to enter his credentials:

![Login page](/images/login_auth.png)


Once the user is authenticated succesfully an authorization dialog will be shown in which the user has to confirm that he grants your application the requested data permission. When submitting this dialog the user authenticates your app.

If the user grants your application the requested data permission the OAuth Dialog will redirect the user's browser to the URL you specified in the redirect_url together with an authorization code. This redirect uses the HTTP 302 status code. The URL will look like this:

	http://YOUR_URL?code=SERVER_GENERATED_AUTHORIZATION_CODE
	
Using this code you can perform the next step: app authentication. After your application has been authenticated you will receive an access code which you can use when making calls to the API. In order to authenticate your app you have to submit your authorization code and app secret to the token endpoint at the address:

The app secret can be viewed when you log in to our [Applications Portal](http://applications.mercadolibre.com.ar/home), you should never share your application secret with anyone. To authenticate your app you must pass the right parameters and make a *POST* to the following URL:

	https://api.mercadolibre.com/oauth/token?grant_type=authorization_code&client_id=CLIENT_ID&client_secret=CLIENT_SECRET&code=SECRET_CODE&redirect_uri=$APP_CALLBACK_URL
	
If your app is succesfully authenticated and the authorization code from the user is valid, the authorization server will return the access token. An example JSON response is:

{% highlight javascript %}

{
   "access_token" : "APP_USR-6092-3246532-cb45c82853f6e620bb0deda096b128d3-8035443",
   "token_type" : "bearer",
   "expires_in" : 10800,
   "refresh_token" : "TG-1025633383c1a2f67323423423b05213abb",
   "scope" : "write read"
}
{% endhighlight %}

Besides the access token, the response also contains the time in seconds the access token expires (the expires_in parameter). You can use the refresh token (the refresh_token) to get a new access token. Please use the following url to request a new access token using the refresh token:

## Client-side Flow {#client-side-flow}
As with the server-flow, the client-side flow also uses the OAuth Dialog for user authentication and app authorization. The only difference is that you must remove the redirect_uri parameter. The URL should look like:

	https://auth.mercadolibre.com.ar/authorization?response_type=code&client_id=Client_id

## Token refresh {#token-refresh}
After the consumer has been authorized for access, they can use a refresh token to get a new access token (session ID.) This is only done after the consumer already has received an access token using either the Web server or user-agent flow. This becomes necessary when an access token is no longer valid and when you need to  apply for a new one.    
    
A consumer can use the refresh token to get a new session as needed.
The consumer should make POST request to the token endpoint, with the following parameters:    

- `grant_type` — Value must be refresh_token for this flow.
- `refresh_token` — Refresh token from the approval step.
- `client_id` — Consumer key from the remote access application definition.
- `client_secret` — Consumer secret from the remote access application definition.    

		https://api.mercadolibre.com/oauth/token?grant_type=refresh_token&client_id=CLIENT_ID&client_secret=CLIENT_SECRET&refresh_token=REFRESH_TOKEN
		

