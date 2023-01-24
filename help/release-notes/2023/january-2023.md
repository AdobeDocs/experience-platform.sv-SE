---
title: Adobe Experience Platform Release Notes januari 2023
description: Versionsinformation januari 2023 för Adobe Experience Platform.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 25 januari 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Källor](#sources)

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| Tillåt användaråtkomst till undermappar för molnlagringskällor | Nu kan du definiera åtkomst till en viss undermapp i molnlagringskällan när du skapar ett nytt konto. När de har skapats kan användarna bara komma åt data från den tillåtna undermappen. Den här funktionen är tillgänglig för följande molnlagringskällor: [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud-lagring](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)och [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Tillgänglighet för betaversion av [!DNL SugarCRM] | [!DNL SugarCRM] Nu finns källor i betaversionen. Använd [!DNL SugarCRM Accounts & Contacts] och [!DNL SugarCRM Events] källor som hämtar data från [!DNL SugarCRM] konto till Experience Platform. Mer information finns i [[!DNL SugarCRM] översikt](../../sources/connectors/crm/sugarcrm.md). |