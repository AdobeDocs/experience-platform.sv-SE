---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Sekretess i kunddataprofil i realtid
seo-title: Sekretess i kunddataprofil i realtid
description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
seo-description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Sekretess i CDP i realtid

[!DNL Real-time Customer Data Platform] (CDP i realtid) hjälper marknadsförare att samla data från olika affärssystem så att de bättre kan identifiera, förstå och engagera sina kunder. Adobe har konsumentdatasekretess som en grundläggande designprincip och tillhandahåller olika kontroller för att hjälpa marknadsförarna att hantera sina kunders datasekretess.

Huvuddelen av CDP-funktionerna i realtid drivs av Adobe Experience Platform. Det här dokumentet innehåller information om de olika tekniker för integritetsförbättring som stöds av CDP i realtid, med länkar till [!DNL Experience Platform] dokumentation för mer information.

## [!DNL Privacy Service]

Med Adobe Experience Platform [!DNL Privacy Service] kan ni effektivisera processen att se till att era dataåtgärder följer sekretessregler som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA). Eftersom CDP i realtid utnyttjar [!DNL Experience Platform] funktioner för datainsamling och datalagring bör förfrågningar om åtkomst och radering för GDPR och CCPA hanteras inom [!DNL Platform]. En mer detaljerad introduktion till tjänsten finns i översiktsdokumentet om [Privacy Servicen](../../privacy-service/home.md) .

Det finns två metoder för att skicka in enskilda förfrågningar från registrerade personer om GDPR och CCPA för att få tillgång till och ta bort kunddata:

* Använd för [!DNL Privacy Service UI](https://gdprui.cloud.adobe.io/) att skapa och övervaka åtkomst- och borttagningsbegäranden på en visuell arbetsyta. I självstudiekursen [för](../../privacy-service/ui/overview.md) Privacy Service finns stegvisa instruktioner.
* Använd för [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) att hantera åtkomst- och borttagningsbegäranden med RESTful API-anrop. I självstudiekursen [för](../../privacy-service/api/getting-started.md) Privacy Service-API finns stegvisa instruktioner.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Nästa steg

Det här dokumentet innehåller en kort introduktion till sekretessfunktionerna i CDP i realtid. Mer detaljerad information om de effektivaste strategierna och stegen för att skicka in begäran om åtkomst/borttagning finns i [Privacy Servicens dokumentation](../../privacy-service/home.md).