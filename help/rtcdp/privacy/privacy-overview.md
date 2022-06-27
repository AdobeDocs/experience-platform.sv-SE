---
keywords: datastyrning rtcdp;rtcdp datastyrning;kunddataprofildatastyrning i realtid;sekretess rtcdp;rtcdp sekretess
title: Integritet i Real-time Customer Data Platform
description: Med Real-time Customer Data Platform kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Integritet i Real-time Customer Data Platform

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) hjälper marknadsförare att samla data från flera olika företagssystem så att de bättre kan identifiera, förstå och engagera sina kunder. Adobe har konsumentdatasekretess som en grundläggande designprincip och tillhandahåller olika kontroller för att hjälpa marknadsförarna att hantera sina kunders datasekretess.

Huvuddelen av [!DNL Real-time CDP] funktioner drivs av Adobe Experience Platform. Det här dokumentet innehåller information om de olika tekniker för integritetsförbättring som stöds av [!DNL Real-time CDP], med länkar till [!DNL Experience Platform] mer information.

## Klara förfrågningar om kundåtkomst och -borttagning

Lagliga sekretessregler som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA) ger kunderna rätt att begära åtkomst till eller radering av de personuppgifter som ni samlar in från dem. Sedan [!DNL Real-time CDP] hävstångar [!DNL Experience Platform] funktioner för datainsamling och lagring, kundförfrågningar om åtkomst till och radering av personuppgifter bör hanteras inom [!DNL Platform]. Se översikten på [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) för mer information.

>[!IMPORTANT]
>
> Sekretessförfrågningar som skickas in via Adobe Experience Platform Privacy Service för Adobe Marketo Engage gäller endast CDP B2B-kunder i realtid.

## Avanmälningsfunktioner

[!DNL Real-time CDP] ger kunderna möjlighet att välja bort att deras personuppgifter ska ingå i användningsfall för segmentering. Kundernas avanmälningsinställningar hämtas och lagras av [!DNL Real-time Customer Profile]och kan framtvingas genom att man utesluter användare som har avanmält sig från ett segment med hjälp av boolesk logik (&quot;AND NOT&quot;) i segmentpredikatet.

Visa dokumentet på [uppfylla avanmälningsbegäranden](../../segmentation/consents.md) mer information finns i dokumentationen till Adobe Experience Platform Segmentation Service.

## Stöd för IAB TCF 2.0

[!DNL Real-time CDP] bygger på Adobe Experience Platform, som ingår i [leverantörslista](https://iabeurope.eu/vendor-list-tcf-v2-0/) för [!DNL Transparency & Consent Framework (TCF)], enligt konturerna i [!DNL Interactive Advertising Bureau (IAB)]. I enlighet med kraven för TCF 2.0 kan du med Platform samla in detaljerade data om kundernas samtycke och integrera dem i era lagrade kundprofiler. Dessa data om samtycke kan sedan beaktas för att avgöra om vissa profiler ingår i exporterade målgruppssegment, beroende på hur de används.

Se översikten på [Stöd för IAB TCF 2.0 i Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) för mer information.

## Nästa steg

Det här dokumentet innehåller en kort introduktion till sekretessfunktionerna i [!DNL Real-time CDP]. Mer information om de olika funktionerna finns i dokumentationen som är länkad till i den här handboken.
