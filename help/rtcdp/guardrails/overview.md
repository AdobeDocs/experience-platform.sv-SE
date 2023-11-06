---
title: Real-Time CDP Guardrails
description: Läs mer om de olika tjänsterna och områdena i Real-Time CDP.
source-git-commit: c6daa645743331ba6fdf8f79e432ae150ee1ff9e
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Real-Time CDP Guardrails

Garantier är trösklar som ger vägledning för data- och systemanvändning, prestandaoptimering och undvikande av fel eller oväntade resultat i Real-Time CDP. Garantier kan avse din användning eller konsumtion av data och bearbetning i relation till dina licensrättigheter.

Börja här och följ länkarna nedan för att få en förståelse för alla skyddsprofiler för de olika tjänsterna och områdena i Real-Time CDP:

* [Skyddsritningar för dataöverföring](/help/ingestion/guardrails.md)
* [Guardrails for the [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Guardrails för [!DNL Real-Time Customer Profile] data och segmentering](/help/profile/guardrails.md)
* [Guardrails för [!DNL Identity Service] data](/help/identity-service/guardrails.md)
* [Guardrails för [!DNL Query Service]](/help/query-service/guardrails.md)
* [Garantier för dataaktivering via destinationer](/help/destinations/guardrails.md)

>[!TIP]
>
>Mer information finns i [den här sidan](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) för information om skyddsräcken för andra Experience Platform-appar, som [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html) och [Customer Journey Analytics](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)och [slingrande diagram](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.

## Skyddstyper {#guardrail-types}

Observera att de två skyddstyperna för alla Real-Time CDP områden och tjänster är:

| Typ av skyddsräcke | Beskrivning |
|----------|---------|
| **Prestandaskydd (mjuk gräns)** | Prestandaskydd är användarbegränsningar som relaterar till omfattningen av dina användningsfall. När du överskrider prestandaskyddet kan du uppleva prestandaförsämringar och fördröjning. Adobe ansvarar inte för sådana prestandaförsämringar. Kunder som genomgående överskrider ett prestandaresäkerhetsskydd kan välja att licensiera ytterligare kapacitet för att undvika prestandaförsämringar. |
| **Systemstyrda skyddsräcken (hård begränsning)** | Systemstyrda skyddsräcken används av Real-Time CDP gränssnitt eller API. Det här är begränsningar som du inte kan överskrida eftersom gränssnittet och API kommer att blockera dig från att göra det eller returnera ett fel. |

{style="table-layout:auto"}

## Real-Time CDP licensinformation och tillståndsinformation {#product-descriptions}

Se även produktbeskrivningslänkarna nedan för information om licenser och tillstånd baserat på den utgåva av Real-Time CDP och den nivå som du har köpt:

* [Alla produktbeskrivningar för Adobe](https://helpx.adobe.com/legal/product-descriptions.html)
* [Real-time Customer Data Platform (B2C Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Nästa steg

När du har förstått vilka skyddsprofiler som gäller för olika delar av Real-Time CDP kan du följa med i [exempel på användning vid en Real-Time CDP-implementering](/help/rtcdp/get-started.md).
