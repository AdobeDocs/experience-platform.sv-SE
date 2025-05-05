---
keywords: Experience Platform;datastyrning;kundai;populära ämnen
solution: Experience Platform
feature: Customer AI
title: Datastyrning i kundens AI
description: Adobe Experience Platform tillhandahåller flera tjänster och verktyg som gör att du kan kontrollera dina insamlade upplevelsedata på ett säkert sätt för att följa din affärspraxis, juridiska skyldigheter och utvecklingsprocess.
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Kundens AI och datastyrning i kundens AI

Alla datastyrningsrelaterade inställningar i Kundens AI ärvs från Adobe Experience Platform.

## Dataförvaltning {#governance}

Integrationen mellan kundens AI och Adobe Experience Platform Data Governance ger er möjlighet att kontrollera och förstå data under hela kundresan via Experience Platform. Detta innebär att upprätthålla datakvalitet, datalinje, datakatalogisering med mera.

Dataanvändningsetiketter och policyer som har skapats för datauppsättningar som används av Experience Platform kan visas i kundens arbetsflöde för AI-konfiguration. Dessa etiketter stoppar eller varnar användare som använder etiketterade fält.

Tack vare den här integreringen kan ni hantera regelefterlevnaden effektivare. Datahanteringen i organisationen kan ange regler som begränsar användningen. Det innebär att du kan använda data som överensstämmer med policyer som definieras av data stewards. Läs dokumentationen om [Etiketter och profiler](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html?lang=sv-SE) om du vill veta mer.

## Samtyckesprincip {#consent-policy}

Kunds-AI följer dina önskemål om samtycke. När du har [konfigurerat och aktiverat din medgivandeprincip](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=sv-SE#consent-policy) respekterar kundens AI de medgivandedata som samlats in från dig. Endast godkända data används för att bedöma modellen i efterföljande körningar av modellen. De nya poängen ersätter de gamla poängen och kan användas vid segmentering. Den här funktionen är för närvarande endast tillgänglig för kunder som har skölden för hälso- och sjukvård samt för kunder som har skölden för skydd av privatlivet och privatlivet.

Du kan läsa mer om den här funktionen här:

[Komma igång med kundens AI](../../customer-ai/getting-started.md)
[Adobe Experience Platform &amp; Applications ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=sv-SE)
[Adobe Experience Cloud-arkitekturdiagram](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html?lang=sv-SE)
