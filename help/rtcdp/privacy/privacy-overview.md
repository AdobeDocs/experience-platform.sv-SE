---
keywords: datastyrning rtcdp;rtcdp datastyrning;kunddataprofildatastyrning i realtid;sekretess rtcdp;rtcdp sekretess
title: Integritet i Real-Time Customer Data Platform
description: Med Adobe Real-Time Customer Data Platform kan ni effektivisera processen att se till att era dataåtgärder följer sekretessreglerna.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Integritet i Real-Time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) hjälper marknadsförare att samla data från flera företagssystem så att de bättre kan identifiera, förstå och engagera sina kunder. Adobe har en grundläggande designprincip som integritetsskydd för konsumentdata och tillhandahåller olika kontroller som hjälper marknadsförarna att hantera sina kunders datasekretess.

Huvuddelen av [!DNL Real-Time CDP]-funktionerna drivs av Adobe Experience Platform. Det här dokumentet innehåller information om de olika tekniker för integritetsförbättring som stöds av [!DNL Real-Time CDP], med länkar till [!DNL Experience Platform]-dokumentationen för mer information.

## Klara förfrågningar om kundåtkomst och -borttagning

Juridiska sekretessbestämmelser som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA) ger kunderna rätt att begära åtkomst till eller radering av de personuppgifter som ni samlar in från dem. Eftersom [!DNL Real-Time CDP] utnyttjar [!DNL Experience Platform]-funktioner för datainsamling och lagring bör kundförfrågningar om åtkomst till och borttagning av deras personuppgifter hanteras i [!DNL Experience Platform]. Mer information finns i översikten om [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

>[!IMPORTANT]
>
> Begäran om sekretess som skickas in via Adobe Experience Platform Privacy Service för Adobe Marketo Engage gäller endast Real-Time CDP B2B-kunder.

## Avanmälningsfunktioner

[!DNL Real-Time CDP] tillåter kunder att avanmäla sig från att få sina personuppgifter inkluderade i användningsfall för segmentering. Kundernas avanmälningsinställningar hämtas och lagras av [!DNL Real-Time Customer Profile] och kan tillämpas genom att utesluta användare som har avanmält sig från en målgrupp med hjälp av boolesk logik (&quot;AND NOT&quot;) i segmentpredikatet.

Mer information finns i dokumentet om [att behandla avanmälningsbegäranden](../../segmentation/tutorials/consents.md) i dokumentationen för Adobe Experience Platform segmenteringstjänst.

## Stöd för IAB TCF 2.0

[!DNL Real-Time CDP] bygger på Adobe Experience Platform, som är en del av den registrerade [leverantörslistan](https://iabeurope.eu/vendor-list-tcf/) för [!DNL Transparency & Consent Framework (TCF)], enligt beskrivningen i [!DNL Interactive Advertising Bureau (IAB)]. I enlighet med kraven för TCF 2.0 kan Experience Platform samla in detaljerade data om kundgodkännande och integrera dessa i era lagrade kundprofiler. Dessa data om samtycke kan sedan beaktas för att avgöra om vissa profiler ska inkluderas i exporterade målgrupper, beroende på deras användningsfall.

Mer information finns i översikten om [stöd för IAB TCF 2.0 i Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).

## Nästa steg

Det här dokumentet innehåller en kort introduktion till sekretessfunktionerna för [!DNL Real-Time CDP]. Mer information om de olika funktionerna finns i dokumentationen som är länkad till i den här handboken.
