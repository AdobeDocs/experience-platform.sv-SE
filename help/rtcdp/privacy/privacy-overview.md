---
keywords: datastyrning rtcdp;rtcdp datastyrning;kunddataprofildatastyrning i realtid;sekretess rtcdp;rtcdp sekretess
title: Sekretess i kunddataprofil i realtid
seo-title: Sekretess i kunddataprofil i realtid
description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
seo-description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Sekretess i [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) hjälper marknadsförare att samla data från olika affärssystem så att de bättre kan identifiera, förstå och engagera sina kunder. Adobe har konsumentdatasekretess som en grundläggande designprincip och tillhandahåller olika kontroller för att hjälpa marknadsförarna att hantera sina kunders datasekretess.

Huvuddelen av [!DNL Real-time CDP]-funktionerna drivs av Adobe Experience Platform. Det här dokumentet innehåller information om de olika tekniker för integritetsförbättring som stöds av [!DNL Real-time CDP], med länkar till [!DNL Experience Platform]-dokumentationen för mer information.

## Klara förfrågningar om kundåtkomst och -borttagning

Lagliga sekretessbestämmelser som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA) ger kunderna rätt att begära åtkomst till eller radering av de personuppgifter som ni samlar in från dem. Eftersom [!DNL Real-time CDP] utnyttjar [!DNL Experience Platform]-funktioner för datainsamling och lagring bör kundförfrågningar om att få tillgång till och ta bort sina personuppgifter hanteras inom [!DNL Platform]. Mer information finns i översikten på [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Avanmälningsfunktioner

[!DNL Real-time CDP] ger kunderna möjlighet att välja bort att deras personuppgifter ska ingå i användningsfall för segmentering. Kundernas avanmälningsinställningar hämtas och lagras av [!DNL Real-time Customer Profile] och kan tillämpas genom att utesluta användare som har avanmält sig från ett segment med hjälp av boolesk logik (&quot;AND NOT&quot;) i segmentpredikatet.

Mer information finns i dokumentet om [ifråga om avanmälan](../../segmentation/honoring-opt-outs.md) i dokumentationen för Adobe Experience Platform Segmentation Service.

## Stöd för IAB TCF 2.0

[!DNL Real-time CDP] bygger på Adobe Experience Platform, som är en del av den registrerade  [leverantörslistan ](https://iabeurope.eu/vendor-list-tcf-v2-0/) för  [!DNL Transparency & Consent Framework (TCF)], enligt  [!DNL Interactive Advertising Bureau (IAB)]riktlinjerna. I enlighet med kraven för TCF 2.0 kan du med Platform samla in detaljerade data om kundernas samtycke och integrera dem i era lagrade kundprofiler. Dessa data om samtycke kan sedan beaktas för att avgöra om vissa profiler ingår i exporterade målgruppssegment, beroende på hur de används.

Mer information finns i översikten om stöd för IAB TCF 2.0 i Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).[

## Nästa steg

Det här dokumentet innehåller en kort introduktion till sekretessfunktionerna i [!DNL Real-time CDP]. Mer information om de olika funktionerna finns i dokumentationen som är länkad till i den här handboken.