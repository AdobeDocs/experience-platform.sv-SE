---
title: Adobe Experience Platform Release Notes
description: The latest release notes for Adobe Experience Platform.
source-git-commit: 9117fffc58786f05e8741d9695ddb551344b6cc7
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 2%

---

# Adobe Experience Platform release notes

****

New features in Adobe Experience Platform:

- [Audit logs](#audit-logs)

Updates to existing features in Adobe Experience Platform:

- [Larm](#alerts)
- [Experience Data Model (XDM)](#xdm)
- [Källor](#sources)

## Audit Logs {#audit-logs}

Experience Platform allows you to audit user activity for various services and capabilities. The audit logs provide information about who did what and when.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Audit logs for Dataset, Schema, Class, Field group, Data type, Sandbox, Destination, Segment, Merge policy, Computed attribute, Product profile and Account (Adobe) | These are the resources which are recorded by audit logs. If the feature is enabled, the audit logs will be automatically collected as activity occurs. You do not need to manually enable log collection. |
| Export audit logs | `CSV``JSON` The generated files are saved directly to your machine. |

{style=&quot;table-layout:auto&quot;}

[](../../landing/governance-privacy-security/audit-logs/overview.md)

## Larm {#alerts}

Experience Platform allows you to subscribe to event-based alerts for various Platform activities. [!UICONTROL Alerts]

****

| Funktion | Beskrivning |
| --- | --- |
| New alert rules | Two new alert rules are now available for sources related to data ingestion. [](../../observability/alerts/rules.md) |

{style=&quot;table-layout:auto&quot;}

[](../../observability/alerts/overview.md)

## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

****

| Funktion | Beskrivning |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br><br><br>[](../../xdm/ui/resources/schemas.md) |

{style=&quot;table-layout:auto&quot;}

[](../../xdm/home.md)

## Källor {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using Platform services. You can ingest data from a variety of sources such as Adobe applications, cloud-based storage, third-party software, and your CRM system.

Experience Platform provides a RESTful API and an interactive UI that lets you set up source connections for various data providers with ease. These source connections allow you to authenticate and connect to external storage systems and CRM services, set times for ingestion runs, and manage data ingestion throughput.

****

| Funktion | Beskrivning |
| --- | --- |
| New sources now available for B2B usage | You can now use all the available sources on Platform for B2B use cases. [](../../sources/home.md) |
| [!DNL Oracle Eloqua] | [!DNL Oracle Eloqua][!DNL Oracle Eloqua] [ [!DNL Oracle Eloqua] ](../../sources/connectors/oracle-eloqua.md) |
| [!DNL Data Landing Zone] | [!DNL Data Landing Zone][!DNL Flow Service] [ [!DNL Data Landing Zone] ](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) |

{style=&quot;table-layout:auto&quot;}

[](../../sources/home.md)
