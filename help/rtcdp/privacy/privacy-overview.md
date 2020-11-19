---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Sekretess i kunddataprofil i realtid
seo-title: Sekretess i kunddataprofil i realtid
description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
seo-description: Med kunddataprofilen i realtid kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
translation-type: tm+mt
source-git-commit: bdd80b15258bf4e3c0dee1e260fd3469c76d5885
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Integritet i [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) hjälper marknadsförare att samla data från olika affärssystem så att de bättre kan identifiera, förstå och engagera sina kunder. Adobe har konsumentdatasekretess som en grundläggande designprincip och tillhandahåller olika kontroller för att hjälpa marknadsförarna att hantera sina kunders datasekretess.

Huvuddelen av [!DNL Real-time CDP] möjligheterna drivs av Adobe Experience Platform. Det här dokumentet innehåller information om de olika tekniker för integritetsförbättring som stöds av [!DNL Real-time CDP]samt länkar till [!DNL Experience Platform] dokumentation för mer information.

## Klara förfrågningar om kundåtkomst och -borttagning

Lagliga sekretessbestämmelser som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA) ger kunderna rätt att begära åtkomst till eller radering av de personuppgifter som ni samlar in från dem. Eftersom [!DNL Real-time CDP] använder [!DNL Experience Platform] funktioner för datainsamling och lagring bör kundförfrågningar om att få tillgång till och ta bort sina personuppgifter hanteras i [!DNL Platform]. Mer information finns i översikten om [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) .

## Avanmälningsfunktioner

[!DNL Real-time CDP] ger kunderna möjlighet att välja bort att deras personuppgifter ska ingå i användningsfall för segmentering. Kundernas avanmälningsinställningar hämtas och lagras av [!DNL Real-time Customer Profile], och kan tillämpas genom att utesluta användare som har avanmält sig från ett segment med hjälp av boolesk logik (&quot;AND NOT&quot;) i segmentpredikatet.

Mer information finns i dokumentet om [att hantera avanmälningsbegäranden](../../segmentation/honoring-opt-outs.md) i dokumentationen för Adobe Experience Platform Segmentation Service.

## Stöd för IAB TCF 2.0

[!DNL Real-time CDP] är en del av den registrerade [leverantörslistan](https://iabeurope.eu/vendor-list-tcf-v2-0/) för [!DNL Transparency & Consent Framework (TCF)], enligt vad som anges i [!DNL Interactive Advertising Bureau (IAB)]. I enlighet med kraven för TCF 2.0 kan ni samla in detaljerade data om kundgodkännande och integrera dem i era lagrade kundprofiler. [!DNL Real-time CDP] Dessa data om samtycke kan sedan beaktas för att avgöra om vissa profiler ingår i exporterade målgruppssegment, beroende på hur de används.

Mer information finns i översikten om stöd för [IAB TCF 2.0 i [!DNL Real-time CDP]](./iab/overview.md) .

## Nästa steg

Det här dokumentet innehåller en kort introduktion till sekretessfunktionerna i [!DNL Real-time CDP]. Mer information om de olika funktionerna finns i dokumentationen som är länkad till i den här handboken.