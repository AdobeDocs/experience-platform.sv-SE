---
keywords: datastyrning rtcdp;rtcdp datastyrning;kunddataprofildatastyrning i realtid;sekretess rtcdp;rtcdp sekretess
title: Integritet i Real-time Customer Data Platform
description: Med Adobe Real-time Customer Data Platform kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 2a0ebe1e92ea21ff45051096d5a6969839c2f947
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Integritet i Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) hjälper marknadsförare att samla data från flera olika företagssystem så att de bättre kan identifiera, förstå och engagera sina kunder. Adobe har konsumentdatasekretess som en grundläggande designprincip och tillhandahåller olika kontroller för att hjälpa marknadsförarna att hantera sina kunders datasekretess.

Majoriteten av [!DNL Real-Time CDP] funktioner drivs av Adobe Experience Platform. Det här dokumentet innehåller information om de olika tekniker för integritetsförbättring som stöds av [!DNL Real-Time CDP], med länkar till [!DNL Experience Platform] mer information.

## Klara förfrågningar om kundåtkomst och -borttagning

Lagliga sekretessregler som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA) ger kunderna rätt att begära åtkomst till eller radering av de personuppgifter som ni samlar in från dem. Sedan [!DNL Real-Time CDP] hävstångar [!DNL Experience Platform] funktioner för datainsamling och lagring, kundförfrågningar om åtkomst till och radering av personuppgifter bör hanteras inom [!DNL Platform]. Se översikten på [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) för mer information.

>[!IMPORTANT]
>
> Begäran om sekretess som skickas in via Adobe Experience Platform Privacy Service för Adobe Marketo Engage gäller endast Real-Time CDP B2B-kunder.

## Avanmälningsfunktioner

[!DNL Real-Time CDP] ger kunderna möjlighet att välja bort att deras personuppgifter ska ingå i användningsfall för segmentering. Kundernas avanmälningsinställningar hämtas och lagras av [!DNL Real-Time Customer Profile]och kan framtvingas genom att man utesluter användare som har avanmält sig från ett segment med hjälp av boolesk logik (&quot;AND NOT&quot;) i segmentpredikatet.

Visa dokumentet på [uppfylla avanmälningsbegäranden](../../segmentation/consents.md) mer information finns i dokumentationen till Adobe Experience Platform Segmentation Service.

## Stöd för IAB TCF 2.0

[!DNL Real-Time CDP] bygger på Adobe Experience Platform, som ingår i [leverantörslista](https://iabeurope.eu/vendor-list-tcf/) för [!DNL Transparency & Consent Framework (TCF)], enligt konturerna i [!DNL Interactive Advertising Bureau (IAB)]. I enlighet med kraven för TCF 2.0 kan du med Platform samla in detaljerade data om kundernas samtycke och integrera dem i era lagrade kundprofiler. Dessa data om samtycke kan sedan beaktas för att avgöra om vissa profiler ingår i exporterade målgruppssegment, beroende på hur de används.

Se översikten på [Stöd för IAB TCF 2.0 i Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) för mer information.

## Nästa steg

Det här dokumentet innehåller en kort introduktion till sekretessfunktionerna i [!DNL Real-Time CDP]. Mer information om de olika funktionerna finns i dokumentationen som är länkad till i den här handboken.
