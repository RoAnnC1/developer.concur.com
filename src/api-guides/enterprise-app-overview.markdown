---
title: Enterprise App Overview
layout: reference
---

## SAP Concur Registers an App for Your Sandbox

This  will be your Development App. During the Development phase, you will be provided with:

* Development App: includes the `client_id` and `client_secret` (only applicable to select sandboxes) AND (after certification).
* Production App: includes a different `client_id` and `client_secret`. This app is available to be enabled by participating Production clients.

> **NOTE:** If the Partner plans to conduct business in China, this will require a dedicated App ID & Secret for the China App Center & Data Center. Companies connecting from within the China App Center will connect to this app.

Ensure these app credentials are stored securely and completely separate from each other to avoid mixing the IDs and Secrets. You will continue to use the Development app with your Sandbox(es) for ongoing troubleshooting related to Support ticket resolution. This Development app can also be used for future development as APIs are updated and/or released.

## Partner Develops to the SAP Concur App Center Flow using OAuth2

On the SAP Concur App Center page, only Company Admins can connect to your listing. The button is grayed out, otherwise.

![Screenshot showing Connect and Accept Terms](/src/api-guides/images/entoverview1.png)

When the Admin is redirected to the Partner's page to Sign In/Sign Up, the redirect URI will contain an ID and request token.

![Screenshot showing Sign In or Sign Up, and Account Creation](/src/api-guides/images/entoverview2.png)

Partner makes API call to exchange the ID and request token to obtain a Company Access Token.

![Screenshot showing Confirmation](/src/api-guides/images/entoverview3.png)

The App Listing confirms to the user that the accounts are linked

![Company-level authentican process](/src/api-guides/images/entoverview-company-level-auth.png)

### SAP Concur App Center Flow Technical Overview

Partner is required to create a landing web page (aka re-direct). Read the [App Center User Experience Guidelines](https://developer.concur.com/manage-apps/go-market-docs/app-center-ux-guidelines-enterprise.html). This page must be hosted at the URI specified by the Partner. SAP Concur will then reference this URI in the App Center listing. This listing is setup by SAP Concur.

### Token API request and response

REQUEST

```
POST https://us.api.concursolutions.com/oauth2/v0/token
```
Header

```
Content-Type:application/x-www-form-urlencoded
```

Body

```
client_id= \<New App client_id\> (DEV)

client_secret= \<New App client_secret\> (DEV)

grant_type= password

username= \<ID\>

password= \<request token\>
```

RESPONSE

```
{

"expires_in": 1523982425,

"scope": "scopes defined for application",

"token_type": "Bearer",

"access_token": "access_token",

"refresh_token": "refresh_token"

"geolocation": "https://us.api.concursolutions.com"

}
```

### SAP Concur App Center Flow - Technical Overview - API Request & Response

Data Center awareness must be part of your App. SAP Concur has several DCs and your App must be able to switch API endpoints based on the stored geolocation in your db.

* US: <https://us.api.concursolutions.com>
* EMEA: <https://emea.api.concursolutions.com>
* China: <https://cn.api.concurcdc.cn>

China requires a separate App ID and Secret

See more at:
<https://developer.concur.com/api-reference/authentication/apidoc.html#base_uri>

Log the SAP Concur Correlation ID of each API transaction that generates an error. This will enable you to include this ID value when submitting a Support ticket. Our Support team will then find that corresponding value in our logs. This process will expedite Support ticket resolution.

## Partner Includes the Company Info API in their app

Benefits of the SAP Concur Company Info API:

* Allows Partners to streamline the customer on-boarding (the API informs the Partner which client/company just connected).
* This API also includes the client UUID code which should be logged by the Partner and then leveraged for Support tickets.
* This API also includes the SAP Concur Edition type a customer purchased. There are differences in SAP Concur Edition types (Standard vs. Professional Edition) and therefore, some APIs are different. This is why we provide 2 sandboxes, one for each Edition. Differences, if applicable, will be discussed by your Partner Enablement Project Manager. If your app must account for these differences, logging this value will enable you to systematically adjust your app accordingly.

Endpoint to use - GET <https://us.api.concursolutions.com/profile/v1/me>
Authorization: Bearer {Company Access Token}

Response includes a couple of valuable data points:

-   UUID
-   Edition Type:
    -   Professional Edition = "marketingName": "CTE"
    -   Standard Edition = "marketingName": "Standard Edition"

The Partner app must record the SAP Concur Correlation ID of each API transaction that generates an error with this code in your logs. This will allow you to record the Correlation ID in your Support tickets. This ID will be matched in our logs for faster Support ticket resolution.

<https://developer.concur.com/api-reference/profile-beta/company.html>

## Partner: Test app end-to-end, including logging

Testing must include:

* App Center connection.
* Company API request & response.
* Test specific APIs for your application in as many use case scenarios as possible using both sandboxes.
* Test API calls using tokens from different GEO Locations.
  * Partner Enablement will provide access to sites that are hosted in different Data Centers. This is where your systematic switch to different API end points based on the token's GEO location is imperative.
  * If you have plans to conduct business in China, a separate App ID and Secret will be supplied to you solely for the Chinese App Center & Data Center.
* Test Logging (required to pass Certification)
  * Correlation ID: Some legacy APIs may not provide a Correlation ID. For any API that does, log it. Include this whenever submitting a Support ticket example of the correlation ID:

![Example of correlation ID](/src/api-guides/images/entoverview-correlationid-sample.PNG)

## SAP Concur & Partner: Post DEV Testing, Certification & Support

### SAP Concur & Partner: Post DEV Testing

* SAP Concur and Partner meet for Development Sandbox Walkthrough.
* If everything is working as expected, SAP Concur registers a Production App and provides Partner with the Production `client_id` and `client_secret`.
  * Reminders: This is different than your Development App's `client_id` and `client_secret`. Retain both securely and completely separate as noted earlier.
* SAP Concur creates Production App Listing.
* Partner prepares for Production Walkthrough.

### SAP Concur & Partner: Certification Steps

Successful completion of:
* Development Walkthrough and Production Walkthrough (will be recorded).
* Support requirements for Partner's app to pass certification:
  * GEO Location - support all Data Center API end points based on the token's GEO location.
  * Logging of UUID Code from the Company Info API.
  * Logging of Correlation ID for each API transaction that generates an error.

### Partner Support Requirements

When the Partner adheres to the following, our mutual customers win. App Center Partners should never instruct a customer to log a ticket directly into SAP Concur Customer Support. If the issue is related to the integration between SAP Concur and the Partner, the Partner must log the case. Please see the information at [How To Log a Support Case](https://developer.concur.com/tools-support/requesting-partner-support.html).

## Core Product Training

To ensure your integration has the highest added value for our mutual customers learn about our core products via the training link below. Raise your readiness with product knowledge!

<http://www.concurtraining.com/pr/>

## Production

After certification the client Admin connects to the app from the App Center. The Partner uses the new Auth service to gain Access Token and call Company API to store all the relevant data. Client and Partner begin to use Partner App.
