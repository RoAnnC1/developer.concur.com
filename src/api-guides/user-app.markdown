---
title: E-Receipts App Overview
layout: reference
---

## SAP Concur Sets Up Sandboxes, Registers a Development App, & an App Center Listing

This App will be your development App. During the Development phase, you will be provided with:
* Development App: includes the `client_id` and `client_secret` (only applicable to select sandboxes) AND (after certification)
* Production App: includes a different `client_id` and `client_secret`. This app is available to be enabled by participating Production clients.

> **NOTE:** If the Partner plans to conduct business in China, this will require a dedicated App ID & Secret for the China App Center & Data Center. Companies connecting from within the China App Center will connect to this app.

Ensure these app credentials are stored securely and completely separate from each other to avoid mixing the IDs and Secrets. You will continue to use the development app with your Sandboxes for ongoing troubleshooting related to Support ticket resolution. This development app can also be used for future development as APIs are updated and/or released.

![Process flow](/src/api-guides/images/user-flow.png)

## Partner Develops App Center and Partner-side Connection Flows Using OAuth2

### Partner: Develops Connection Flows

The Partner may be required to develop more than one of the following connections flows. Your Certification PM will advise if you should develop more
than one of these:

SAP Concur App Center Flow - Connecting from SAP Concur Web / Mobile App

* Password Grant

Web Flow - Connecting from Partner Web / Mobile App

* Authorization Grant
* One-Time Password Grant

Please refer to the [Receipts Recipe](https://developer.concur.com/api-guides/e-receipts.html) document for more details.

### Password Grant Flow

![Password grant flow](/src/api-guides/images/password-grant.png)

1. Clicks on 'Connect' on the App Center Page
2. Verifies User
3. Lands on Partner's page to Sign In/Sign Up
4. Uses the POST /token API endpoint with:
  * DEV `client_id` and `client_secret`
  * Password grant type

Partner uses the ID and Request token from the redirect URI as username and password, respectively for the API call.
5. Exchanges Request token for User Access token
6. Partner stores:
  * Access Token
  * Refresh token
  * Expiration date of refresh token
  * ID Token
  * Geolocation
7. After signing in, Partner page also shows that user is Connected.

Decode the `id_token` to obtain the sub value and store this value as the user id (see https://jwt.io ). The user id will be used to post receipts to the user’s SAP Concur account.

### SAP Concur App Center Flow - Technical Overview

Partner is required to create a landing web page (aka re-direct) for this flow. This page must be hosted at the URI specified by the Partner in their App Center listing in SAP Concur T&E. Read the [App Center User Experience Guidelines](https://developer.concur.com/manage-apps/go-market-docs/app-center-ux-guidelines-enterprise.html).

### Token API Request and Response

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

"expires_in": 3600,

"scope": "scopes defined for application",

"token_type": "Bearer",

"access_token": "access_token",

"refresh_token": "refresh_token"

"id_token": "eyJ0eXAiOiJ......",

"geolocation": "https://us.api.concursolutions.com"

}
```

### SAP Concur App Center Flow (Password Grant) - Technical Overview - API Request & Response

Data Center awareness must be part of your App. SAP Concur has multiple DCs and your App must be able to switch API endpoints based on the Token's stored geolocation in your db.

* US https://us.api.concursolutions.com
* EMEA https://emea.api.concursolutions.com
* China https://cn.api.concurcdc.cn

China requires a separate App ID and Secret

See more at: https://developer.concur.com/api-reference/authentication/apidoc.html#base_uri

Log the SAP Concur Correlation ID of each API transaction that generates an error for faster Support ticket troubleshooting. Include this ID in any Support ticket that you need to submit.

## Authorization Grant Flow

User-Level Authentication Technical Overview:

![Authorization grant flow](/src/api-guides/images/authorization-grant.png)

1. Clicks **Connect** on the Partner's Page.
2. Partner calls Auth Service.
3. Verifies Partner app scopes & app data and sends Auth page to User.
4. User has 2 options:
  * Enter SAP Concur Login ID and Password. Confirms app access.
  * Enter SAP Concur primary email address. Receives email, clicks provided **Sign in with Concur**.
5. Authenticates User & sends re-direct page with code to Partner.
6. Sends a POST call to the Auth Service with Authorization Code taken from re-direct.
7. Validates Authorization Code. Generates Token data.
8. Partner app stores token data:
  * Refresh token
  * Expiration date of refresh token
  * Sub (UUID)
  * Geolocation
  *  Access token (valid only for 1 hour)
9. Partner site shows user is connected to SAP Concur.
10. SAP Concur App Center shows user is connected to Partner.

Decode the `id_token` to obtain the sub value and store this value as the user id (see https://jwt.io). The user id will be used to post receipts to the user’s SAP Concur account.

[Authorization Grant]( https://developer.concur.com/api-reference/authentication/apidoc.html#auth_grant)

### SAP Concur Auth Grant - Technical Overview API Request & Response

#### Two API Requests & Responses

REQUEST \#1:

```
GET /oauth2/v0/authorize?client_id={your-app-clientId}&redirect_uri={your-app-redirect-uri}&response_type=code HTTP/1.1
Host: us.api.concursolutions.com
Cache-Control: no-cache
```

RESPONSE:

```
200 OK
```

REQUEST \#2:

```
POST /oauth2/v0/token HTTP/1.1
Host: us.api.concursolutions.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded
client_id={your-app-client_id}
&client_secret={your-app-client_secret}
&redirect_uri={your-app-redirect-uri}
&code={code from redirect-uri}
&grant_type=authorization_code
```

RESPONSE:

```
{
"expires_in": 3600,
"scope": "receipts.write user.read openid",
"token_type": "Bearer",
"access_token": "eyJ0eXAi.......",
"refresh_token": "c556b1a6-5a07-41c6-9005-ef900da66339",
"refresh_expires_in": 1506446740,
"id_token": "eyJ0eXAiOiJ......",
"geolocation": "https://us.api.concursolutions.com"
}
```

Data Center awareness must be part of your App. SAP Concur has multiple DCs and your App must be able to switch API endpoints based on the Token's stored geolocation in your db.

* US https://us.api.concursolutions.com
* EMEA https://emea.api.concursolutions.com
* China https://cn.api.concurcdc.cn

China requires a separate App ID and Secret.

See more at: https://developer.concur.com/api-reference/authentication/apidoc.html#base_uri

Log the SAP Concur Correlation ID of each API transaction that generates an error for faster Support ticket troubleshooting. Include this ID in any Support ticket that you need to submit.

Please refer to the [Receipts Recipe](https://developer.concur.com/api-guides/e-receipts.html) for more API details

## User-Level Authentication Technical Overview:

### One Time Password Grant flow

![One time password grant flow](/src/api-guides/images/one-time-password-grant.png)

1. User enters their email address within the Partner’s website/mobile App.
2. Partner app makes a call to the SAP Concur Authorization service to trigger the OTP email using OTP grant.
3. Verifies Partner app scopes & app data and sends confirmation email to User.
4. User clicks on Link/Connect button within the email.
5. Partner's app re-direct URI captures confirmation code. Calls OAuth2 for token.
6. Validates Authorization Code. Generates Token data.
7. App Stores:
  * Refresh token
  * Expiration date of refresh token
  * Sub (UUID)
  * Geolocation
  * Access token (valid for only 1 hour)
8. Partner site shows user is connected to SAP Concur.
9. SAP Concur App Center shows user is connected to Partner.

Decode the id_token to obtain the sub value and store this value as the user id (see https://jwt.io). The user id will be used to post receipts to the user’s SAP Concur account.

[One-Time Password Grant](https://developer.concur.com/api-reference/authentication/apidoc.html#otp_grant)

### SAP Concur OTP Grant - Technical Overview API Request & Response

#### Two API Requests & Responses

REQUEST \#1:

```
POST oauth2/v0/otp
Host: us.api.concursolutions.com
Content-Type: application/x-www-form-urlencoded
Cache-Control: no-cache
```

RESPONSE:

```
HTTP/1.1 200 OK
Content-Type: application/json
Date: date-requested
Content-Length: 22
json
{"message":"otp sent"}
```

REQUEST \#2:

```
POST oauth2/v0/token
Host: us.api.concursolutions.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 437
```

RESPONSE:

```
{
"expires_in": 3600,
"scope": "receipts.write user.read openid",
"token_type": "Bearer",
"access_token": "eyJ0eXAi.......",
"refresh_token": "c556b1a6-5a07-41c6-9005-ef900da66339",
"refresh_expires_in": 1506446740,
"id_token": "eyJ0eXAiOiJ......",
"geolocation": "https://us.api.concursolutions.com"
}
```

Data Center awareness must be part of your App. SAP Concur has multiple DCs and your App must be able to switch API endpoints based on the Token's stored geolocation in your db.

* US https://us.api.concursolutions.com
* EMEA https://emea.api.concursolutions.com
* China https://cn.api.concurcdc.cn

China requires a separate App ID and Secret.

See more at: https://developer.concur.com/api-reference/authentication/apidoc.html#base_uri

Log the SAP Concur Correlation ID of each API transaction that generates an error for faster Support ticket troubleshooting. Include this ID in any Support ticket that you need to submit.

Please refer to the [Receipts Recipe](https://developer.concur.com/api-guides/e-receipts.html) document for more API details

## Partner: Test App End-to-End

Testing must include:

* App Center connection (Password Grant), Authorization Grant &/or OTP Grant.
* Test specific Receipt APIs for your application
* Test API calls using tokens from different GEO Locations.
  * Partner Enablement will provide access to sites that are hosted in different Data Centers. This is where your systematic switch to different API end points based on the token's GEO location is imperative.
  * If you have plans to conduct business in China, a separate App ID and Secret will be supplied to you solely for the Chinese App Center & Data Center.
* Test Logging (required to pass Certification)
  * Correlation ID: Include this whenever submitting a Support ticket example of the correlation ID:

![Sample correlation ID](/src/api-guides/images/correlationid-sample.png)

## SAP Concur & Partner: Post DEV Testing, Certification, & Support

### SAP Concur & Partner: Post DEV Testing

* SAP Concur and Partner meet for Development Sandbox Walkthrough.
* If everything is working as expected, SAP Concur registers Production App and provides Partner with the Production `client_id` and `client_secret`.

  * Reminders: This is different than your Development App's `client_id` and `client_secret`. Retain both securely and completely separate as noted earlier.
* SAP Concur creates Production App Listing.
 * Partner prepares for Production Walkthrough.

### SAP Concur & Partner: Certification Steps

Successful completion of:
* Development Walkthrough and Production Walkthrough (will be recorded)
* Support requirements for Partner's app to pass certification:
  * App Center connection (Password Grant) + Authorization Grant/OTP Grant
  * GEO Location - support all Data Center API end points based on the token's GEO location.
  * Logging of Correlation ID for each API transaction that generates an error. Here's an example:

![Sample correlation ID](/src/api-guides/images/entoverview-correlationid-sample.png)

## Partner: Support Requirements

When the Partner adheres to the following, our mutual customers win. App Center Partners should never instruct a customer to log a ticket directly into SAP Concur Customer Support. If the issue is related to the integration between SAP Concur and the Partner, the Partner must log the case. Please see the information at [How To Log a Support Case](https://developer.concur.com/tools-support/requesting-partner-support.html).

## Core Product Training

To ensure your integration has the highest added value for our mutual customers learn about our core products via the training link below. Raise your readiness with product knowledge!

http://www.concurtraining.com/pr/

## Production

After certification the client Admin connects to the app from the App Center. The Partner uses the new Auth service to gain Access Token and call Company API to store all the relevant data. Client and Partner begin to use Partner App.
