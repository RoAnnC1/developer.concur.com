---
title: Base URIs
layout: reference
---

## What is the Base URI?

The Base URI (also known as the Instance URL) is the domain where the SAP Concur entity resides. The APIs will work with all entities, but to specify which you are trying to work with you must make a change to the end point declaration before you make your API call. There will be a different domain for each of the following locations: Production, Implementation (copy of the product environment not available for all clients), EMEA (the European data center), and the China data center.

### Production

This platform allows SAP Concur to host entities that are physically closer to a client’s location than other SAP Concur approved data centers.

|Environment|URI|Description|
|---|---|---|
|North America|https://us.api.concursolutions.com|Default for all API calls for client entities in North America.|
|EMEA|https://emea.api.concursolutions.com|Default for all API calls for client entities in throughout Europe.|
|China|https://cn.api.concurcdc.cn|Default for all API calls for client entities in China.|

### Implementation

The implementation base domains are used for implementation sites. An implementation site is a copy of an SAP Concur entity made from a backup of a client’s production site. This feature is only available for the Professional and Premium editions of SAP Concur. Clients have the option to have a permanent implementation site established, contact your Client Executive or Account Manager for details.

|Environment|URI|Description|
|---|---|---|
|North America|https://us-impl.api.concursolutions.com|This domain is used for API calls to client implementation sites that reside on the North America platform.|
|EMEA|https://emea-impl.api.concursolutions.com|This domain is used for API calls to client implementation sites that reside on the EMEA platform.|
|China|https://implementation.concurcdc.cn|This domain is used for API calls to client implementation sites that reside on the China platform.|

### Pre-2017 Authentication (deprecated)

The following base URIs can be used for client that are authenticating against our previous [Authentication method](/authentication/authorization-pre-2017.html).

To migrate to the current authentication method, review these resources:

* https://developer.concur.com/api-reference/authentication/migrationguide.html
* https://developer.concur.com/api-reference/authentication/oauth2-migration-best-practices.html

These URIs support the current authentication and the previous authentication simultaneously.

|Environment|URI|Description|
|---|---|---|
|North America Production|https://www.concursolutions.com|This domain is used for API calls to client production sites that reside on the North America platform.|
|EMEA Production|https://eu1.concursolutions.com|This domain is used for API calls to client production sites that reside on the EMEA platform.|
|North America Implementation|https://implementation.concursolutions.com|This domain is used for API calls to client implementation sites that reside on the North America platform.|
|EMEA Production|https://eu1imp.concursolutions.com|This domain is used for API calls to client implementation sites that reside on the EMEA platform.|

## Authentication Geolocation URIs

Applying the above base URI locations, below are the endpoints a developer would use to access our [authentication API](/authentication/apidoc.html)

|Environment|URI|Description|
|---|---|---|
|North America Production|https://us.api.concursolutions.com/oauth2/v0|Default for all API calls for client entities in the North America.|
|EU Production|https://emea.api.concursolutions.com/oauth2/v0|Default for all API calls for client entities in Europe.|
|China Production|https://cn.api.concurcdc.cn/oauth2/v0|Default for all API calls for all client entities in China.|
|WWW-US Production|https://www-us.api.concursolutions.com/oauth2/v0|Used by browsers during Authorization Code grant.|
|WWW-EU Production|https://www-emea.api.concursolutions.com/oauth2/v0|Used by browsers during Authorization Code grant.|
|WWW-CN Production|https://www-cn.api.concurcdc.cn/oauth2/v0|Used by browsers during Authorization Code grant.|
|North America Implementation|https://us-impl.api.concursolutions.com/oauth2/v0|For customers who have Implementation entities in North America.|
|EU Implementation|https://emea-impl.api.concursolutions.com/oauth2/v0|For customers who have Implementation entities in EMEA.|
|China Implementation|https://implementation.concurcdc.cn|For customers who have Implementation entities in China.|
