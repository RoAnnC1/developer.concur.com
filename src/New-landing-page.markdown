---
title: What is SAP Concur
layout: reference
---

SAP Concur is an integrated travel and expense management solution. Through our platform you can access APIs for expense, travel, invoice, request, and other SAP Concur services to build apps. For information on each main category, explore our product offerings:

* [Expense](https://www.concur.com/en-us/expense-management)
* [Travel](https://www.concur.com/en-us/travel-booking)
* [Invoice](https://www.concur.com/en-us/invoice-management)
* [Request](https://www.concur.com/en-us/expense-approval-system)

To get started using the SAP Concur APIs you first need to have a contract. What do you want to build?

* Develop an application for the SAP Concur App Center. This requires a signed Partner Agreement, [contact us](mailto:concur_bizdev@sap.com).
* Develop an application as an SAP Concur client (or for a client). The client must purchase the Client Web Services SKU and their administrative support contact would open a case through our [support portal](https://www.concur.com/en-us/support).
* Develop an application as a TMC/reseller, [contact us](mailto:supplierservices@sap.com).

## What Can I Do with the SAP Concur APIs?

SAP Concur APIs allow clients or partners to access data and functions within the SAP Concur product ecosystem. Through the use of these exposed endpoints and functions you can solve a vast array of different business issues and reporting needs such as:

* Pull data from SAP Concur for in-depth reporting services.
* Reconcile or validate your data by comparing SAP Concur data to what you have.
* Post new data into SAP Concur allowing for programmatic creation of information.
* Update existing information in SAP Concur to match your system data.

## How Do I Get Started?

Once you have an agreement in place SAP Concur will set up a meeting with our technical resource team. They’ll go through your requirements with you to develop a plan for creating your app or application connector.

After that meeting you’ll receive the credentials necessary to make your first API call, including a `client_id` and `client_secret` that you’ll use to obtain an `access_token`. They’ll also set up sandboxes and/or implementation entities, as needed, for your project and help you work through the development and certification process.

The following terms are used when describing the dev environment that works with the APIs.

**Application or App**: Used by a client or partner to interact with the SAP Concur APIs and make test API calls. This is not included with a Sandbox. An app will have *scopes* assigned to it that dictate the endpoints the app has access to. An app will also have *grants* that dictate the authentication method used by the app.

**Application Connector**: The piece of software that communicates with the SAP Concur APIs and your application. This software can be a simple scheduled task, a user executed application, or even a separate module hosted on a public Web Server. For more information see, [Callouts and Application Connectors](https://developer.concur.com/api-reference/callouts/callouts-application-connectors.html).

**Grants**: Which authentication method the app is allowed to use.

**Sandbox**: An instance of the SAP Concur production environment that a client or partner can use to gain familiarity with SAP Concur products and create sample trips, expense reports, etc. Typically these are used for partner apps, but in some cases web services clients will be provided with an implementation test site.

**Scopes**: Which endpoints the app (not Sandbox) has access to.

## Best Practices to Keep in Mind

We all know you shouldn’t write your password on a sticky note and keep it under your keyboard. That said, sometimes convenience overrides common sense. Some things to keep in mind as you create your app:

* Ensure your app credentials are stored securely and completely separate from each other to avoid mixing the IDs and secrets.
* Examples that are provided in the online documentation are for illustration only. Don’t copy and paste them into your app without verifying their security and stability.
* Real financial data shouldn’t be used while developing and testing your app.

## How Do I Authenticate?

SAP Concur uses OAuth 2.0 an authorization protocol designed to enable third-party applications to obtain limited access to an HTTP service, either on behalf of a resource owner by orchestrating an approval interaction between the resource owner and the HTTP service, or by allowing a third-party application to obtain access on its own behalf.

The APIs implement OAuth 2.0 because it provides a simple mechanism for end-users to grant a partner application access to their data (protected resources) without sharing their passwords. It also enables the user to grant limited access to their data in terms of scope, duration, and so on. For example, a user (resource owner) can grant a travel app (client) access to her protected travel data stored at SAP Concur (resource server), without sharing her username and password with the travel app. Instead, she authenticates directly with SAP Concur (authorization server), which issues the travel app delegation-specific credentials (access token).

To learn how to obtain the credentials you’ll need for authentication, read [Getting Started](https://developer.concur.com/api-reference/authentication/getting-started.html). For information on the various types of grants available and when to use them, read [Authentication](https://developer.concur.com/api-reference/authentication/apidoc.html).
