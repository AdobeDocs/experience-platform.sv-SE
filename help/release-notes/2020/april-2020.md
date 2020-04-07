---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 8 april 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: b3ee2839412c9949d67c2ae976e3df32fea7731e

---


# Versionsinformation om Adobe Experience Platform

## Releasedatum: 8 april 2020

## Integritetstjänst

Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Integritetstjänsten för Adobe Experience Platform tillhandahåller ett RESTful API och användargränssnitt som hjälper er att hantera dessa dataförfrågningar från era kunder. Med Integritetstjänsten kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för PDPA | Begäran om skydd av personuppgifter kan nu skapas och spåras i Thailand enligt lagen om skydd av personuppgifter (PDPA). När du gör sekretessförfrågningar i API:t accepterar arrayen värdet &quot;pdpa_tha&quot;. `regulation` |
| Namnområdestyper i användargränssnittet | Du kan nu ange olika namnområdestyper i Request Builder i Sekretessgränssnittet. Mer information finns i [användarhandboken](../../privacy-service/ui/user-guide.md) . |
| Tidigare borttagning av slutpunkt | Den gamla API-slutpunkten (`data/privacy/gdpr`) har tagits bort. |

Kända fel

* Ingen

Mer information om sekretesstjänsten finns i översikten över [sekretesstjänsten](../../privacy-service/home.md).

## Källor

Adobe Experience Platform kan importera data från externa källor samtidigt som ni kan strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, programvara från tredje part och ditt CRM-system.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

### Nya funktioner

| Funktion | Beskrivning |
| ------- | ----------- |
| API- och gränssnittsstöd för databaser | Nya källanslutningar för Apache Spark (på HDInsights), Azure Synapse Analytics, Azure Table Storage, Hive (på HDInsights) och Phoenix. |
| API- och gränssnittsstöd för betalningsbaserade program | Nya källanslutningar för PayPal. |
| API- och gränssnittsstöd för protokollbaserade program | Nya källkopplingar för allmänna OData. |

### Kända fel

* Ingen

Mer information om källor finns i [Källöversikt](../../source-connectors/home.md).

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->