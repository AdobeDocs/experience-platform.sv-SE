---
keywords: Experience Platform;datastyrning;kundai;populära ämnen
solution: Experience Platform
feature: Customer AI
title: Datastyrning i kundens AI
description: Adobe Experience Platform tillhandahåller flera tjänster och verktyg som gör att du kan kontrollera dina insamlade upplevelsedata på ett säkert sätt för att följa din affärspraxis, juridiska skyldigheter och utvecklingsprocess.
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Kundens AI och datastyrning i kundens AI

Alla datastyrningsrelaterade inställningar i Kundens AI ärvs från Adobe Experience Platform.

## Datastyrning {#governance}

Integrationen mellan kundens AI och Adobe Experience Platform Data Governance ger er möjlighet att kontrollera och förstå data under hela kundresan via Platform. Detta innebär att upprätthålla datakvalitet, datalinje, datakatalogisering med mera.

Dataanvändningsetiketter och policyer som har skapats för datauppsättningar som används av plattformen kan visas i kundens arbetsflöde för AI-konfiguration. Dessa etiketter stoppar eller varnar användare som använder etiketterade fält.

Tack vare den här integreringen kan ni hantera regelefterlevnaden effektivare. Datahanteringen i organisationen kan ange regler som begränsar användningen. Det innebär att du kan använda data som överensstämmer med policyer som definieras av data stewards. Läs dokumentationen på [Etiketter och profiler](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html) om du vill veta mer.

## Samtyckesprincip {#consent-policy}

Kunds-AI följer dina önskemål om samtycke. En gång har du [konfigurera och aktivera din policy för samtycke](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#consent-policy), kommer kundens AI att respektera de data ni samlar in. Endast godkända data används för att bedöma modellen i efterföljande körningar av modellen. De nya poängen ersätter de gamla poängen och kan användas vid segmentering. Den här funktionen är för närvarande endast tillgänglig för kunder som har skölden för hälso- och sjukvård samt för kunder som har skölden för skydd av privatlivet och privatlivet.

Du kan läsa mer om den här funktionen här:

[Komma igång med kundens AI](../../customer-ai/getting-started.md)
[Adobe Experience Platform och program](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Adobe Experience Cloud arkitekturdiagram](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
