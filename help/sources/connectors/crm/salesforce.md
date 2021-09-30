---
keywords: Experience Platform;hem;populära ämnen;crm schema;crm;CRM;salesforce;Salesforce
solution: Experience Platform
title: Salesforce Source Connector - översikt
topic-legacy: overview
description: Lär dig hur du ansluter Salesforce till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 759f38bac9b59fe32594dff771617ba8eaabae41
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# [!DNL Salesforce] koppling

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett CRM-system från tredje part. Stöd för CRM-providers är [!DNL Salesforce].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

<!--
## Field mapping from [!DNL Salesforce] to XDM

To establish a source connection between [!DNL Salesforce] and Platform, the [!DNL Salesforce] source data fields must be mapped to their appropriate target XDM fields prior to being ingested into Platform.

See the following for detailed information on the field mapping rules between [!DNL Salesforce] datasets and Platform:

- [Contacts](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Accounts](../adobe-applications/mapping/salesforce.md#account)
- [Opportunities](../adobe-applications/mapping/salesforce.md#opportunity)
- [Opportunity contact roles](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campaigns](../adobe-applications/mapping/salesforce.md#campaign)
- [Campaign members](../adobe-applications/mapping/salesforce.md#campaign-member)

## Set up the [!DNL Salesforce] namespace and schema auto-generation utility

To use the [!DNL Salesforce] source as part of [!DNL B2B-CDP], you must first set up a [!DNL Postman] utility to auto-generate your [!DNL Salesforce] namespaces and schemas. The following documentation provides additonal information on setting up the [!DNL Postman] utility:

- You can download the namespace and schema auto-generation utility collection and environment from this [GitHub repository](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility).
- For information on using Platform APIs including details on how to gather values for required headers and read sample API calls, see the guide on [getting started with Platform APIs](../../../landing/api-guide.md).
- For information on how to generate your credentials for Platform APIs, see the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md).
- For information on how to set up [!DNL Postman] for Platform APIs, see the tutorial on [setting up developer console and [!DNL Postman]](../../../landing/postman.md).

With a Platform developer console and [!DNL Postman] set up, you can now start applying the appropriate environment values to your [!DNL Postman] environment.

The following table contains example values as well as additional information on populating your [!DNL Postman] environment:

| Variable | Description | Example |
| --- | --- | --- |
| `CLIENT_SECRET` | A unique identifier used to generate your `{ACCESS_TOKEN}`. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to retrieve your `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | The JSON Web Token (JWT) is an authentication credential used to generate your {ACCESS_TOKEN}. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to generate your `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | A unique identifier used to authenticate calls to Experience Platform APIs. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to retrieve your `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | The authorization token required to complete calls to Experience Platform APIs. See the tutorial on [authenticating and accessing Experience Platform APIs](../../../landing/api-authentication.md) for information on how to retrieve your `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | With regards to [!DNL Marketo], this value is fixed and is alway set to: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | The `global` container holds all standard Adobe and Experience Platform partner provided classes, schema field groups, data types, and schemas. With regards to [!DNL Marketo], this value is fixed and is always set to `global`. | `global` |
| `PRIVATE_KEY` | A credential used to authenticate your [!DNL Postman] instance to Experience Platform APIs. See the tutorial on setting up developer console and [setting up developer console and [!DNL Postman]](../../../landing/postman.md) for instructions on how to retrieve your {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | A credential used to integrate to Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | The Identity Management System (IMS) provides the framework for authentication to Adobe services. With regards to [!DNL Marketo], this value is fixed and is always set to: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | A corporate entity that can own or license products and services and allow access to its members. See the tutorial on [setting up developer console and [!DNL Postman]](../../../landing/postman.md) for instructions on how to retrieve your `{IMS_ORG}` information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | The name of the virtual sandbox partition that you are using. | `prod` |
| `TENANT_ID` | An ID used to ensure that the resources you create are namespaced properly and are contained within your IMS Organization. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | The URL endpoint that you are making API calls to. This value is fixed and is always set to: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | The unique ID for your [!DNL Marketo] account. See the tutorial on [authenticating your [!DNL Marketo] instance](../adobe-applications/marketo/marketo-auth.md) for information on how to retrieve your `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | The organization ID for your [!DNL Salesforce] account. See the following [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&type=1&mode=1) for more information on acquiring your [!DNL Salesforce] organization ID. | `00D4W000000FgYJUA0` |
`f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | A boolean value that indicates if you are subscribed to [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | A boolean value that indicates if you are subcscribed to [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Running the scripts

With your [!DNL Postman] collection and environment set up, you can now run the script through the [!DNL Postman] interface.

In the [!DNL Postman] interface, select the root folder of the auto-generator utility and then select **[!DNL Run]** from the top header.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

The [!DNL Runner] interface appears. From here, ensure that all the checkboxes are selected and then select **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

A successful request creates the B2B namespaces and schemas according to beta specifications.

-->

## Anslut [!DNL Salesforce] till plattformen med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce] till plattformen med API:er eller användargränssnittet:

- [Skapa en Salesforce-basanslutning med API:t för Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Utforska datastrukturen och innehållet i en CRM-källa med API:t för Flow Service](../../tutorials/api/explore/crm.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

## Anslut [!DNL Salesforce] till plattformen med användargränssnittet

- [Skapa en Salesforce-källanslutning i användargränssnittet](../../tutorials/ui/create/crm/salesforce.md)
- [Skapa ett dataflöde för en CRM-anslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
