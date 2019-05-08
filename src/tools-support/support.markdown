---
title: Support Options
layout: reference

redirect_from:
  - /docs-and-resources/support/index.html
---

## [Service Status](https://open.concur.com)

## Support Scenarios

* **Partners** have two choices depending on the scenario.
  * Alliance Team assistance - Partners should first contact their Alliance Manager or the [Alliance Team](mailto:concur_AppCenterAlliance@sap.com) for assistance that is not related to production app technical issues.
  * [Technical Support ticketing](#log-a-support-case) - select this option to log a support case related to the operation of your certified, production application.
* **Company Administrators** access the [FAQ and other resources](https://www.concur.com/en-us/support) to get the help you need.
* **Individual Users** of SAP Concur products should request assistance from their company's internal help desk or their company's SAP Concur administrator.

## Maintenance Schedule

The SAP Concur platform undergoes routine maintenance each weekend, and releases updates monthly. During these periods, the service may be unavailable. Unplanned maintenance is performed rarely, and limited to high priority fixes. During downtime, any request to the SAP Concur Platform will receive an HTTP 503 error code. To check the current status see [Service Status](https://open.concur.com) where a message will be posted during planned maintenance.

#### Monthly Release Schedule

For details regarding planned releases, see the [SAP Concur Release Calendar](https://www.concurtraining.com/customers/tech_pubs/ReleaseCalendar/_ReleaseCalendar_client.htm).

## <a name="log-a-support-case"></a>How To Log a Support Case

In the App Center Partner Program, partners provide first-line support for their application.

* Please advise customers to contact you directly for support rather than SAP Concur, which may slow the support process down and reduce customer satisfaction.
* If you are an existing partner and would like support from SAP Concur, please follow the steps below to log a ticket.
  * If you do not have login credentials to the partner support portal, please email [App Center Alliance](mailto:concur_appcenteralliance@sap.com?Subject=Support%20Portal%20Credentials) to request them.

[Login and open a partner support case](https://sapconcur.my.salesforce.com/secur/login_portal.jsp?orgId=00D600000007Dq3&portalId=06060000000PrEi)

Partner cases must include the following:

* App Name: Partners may have more than one certified app.
* Customer Name: This is the name that SAP Concur will recognize.
* For Partner apps certified after September 2017, tickets must include:
  * The `CompanyUUID` -- available via the Company Info API.
  * The `concur-correlationId` from the API response.
* Reproduction steps:
  * Provide contextual information related to the issue so support engineers have an understanding of what the integration is attempting to accomplish.
* If applicable:
  * Employee Name
  * Expense Report Name, Travel Request Name, Payment Request Name, etc.
  * Transactional data such as expense type, date, amount, etc.
* API related information:
  * Refresh Token: Never supply this via email.
  * API Request Information
    * URI
    * Include Method - `GET`, `POST`, `PUT`, `POST`
    * `POST` payload.
  * API Response Information
    * All HTTP Headers
    * Response payload.
  * Additional log information relevant to the issue.
