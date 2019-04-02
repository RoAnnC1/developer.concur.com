---
title: Base URIs
layout: reference
---

## What is the Base URI?

The Base URI (also known as the Instance URL) is the domain where the SAP Concur entity resides. The APIs will work with all entities, but to specify which you are trying to work with you must make a change to the end point declaration before you make your API call. There will be a different domain for each of the following locations: Production, Implementation (copy of the product environment not available for all clients), and EMEA (the European data center).

|Environment |URI |Description |
|-----|-----|------|
|Production|`https://www.concursolutions.com`|The production domain is the only domain that is shared with another site. The developer resources known as “Sandbox sites” also reside on this domain. These domains do not share resources, only the domain they reside at.|
|Implementation|`https://implementation.concursolutions.com`|The implementation domain is used for the implementation sites. An implementation site is a copy of SAP Concur made from a backup of your production site. This feature is only available for a limited amount of time, and is only available for the Premium version of SAP Concur. You do have the option to have a full-time implementation site established, see your Client Executive or Account manager for details.|
|EMEA|`https://eu1.concursolutions.com`|The eu1 domain is reserved strictly for clients on the EMEA platform. This platform allows SAP Concur to host sites on servers that are physically located closer to a client’s location than other SAP Concur approved data centers.|
|Implementation|`https://eu1imp.concursolutions.com`|The eu1imp domain is used for the implementation sites that reside on the EMEA platform. An implementation site is a copy of SAP Concur made from a backup of your production site. This feature is only available for a limited amount of time, and is only available for the Premium version of SAP Concur. You do have the option to have a full-time implementation site established, see your Client Executive or Account manager for details.|

## Authentication URIs

The full list of available token geolocations:

|Environment |URI |Description|
|-----|------|------|
|US Production|`https://us.api.concursolutions.com/oauth2/v0`|Default for all API calls.|
|WWW-US Production|`https://www-us.api.concursolutions.com/oauth2/v0`|Used by browsers during Authorization Code grant.|
|EU Production|`https://emea.api.concursolutions.com/oauth2/v0`|Default for all API calls.|
|WWW-EU Production|`https://www-emea.api.concursolutions.com/oauth2/v0`|Used by browsers during Authorization Code grant.|
|China Production|`https://cn.api.concurcdc.cn/oauth2/v0`|Default for all API calls.|
|WWW-CN Production|`https://www-cn.api.concurcdc.cn/oauth2/v0`|Used by browsers during Authorization Code grant.|
|US Implementation|`https://us-impl.api.concursolutions.com/oauth2/v0`|For customers who have Implementation servers in the US.|
|EU Implementation|`https://emea-impl.api.concursolutions.com/oauth2/v0`|For customers who have Implementation servers in the EU.|
