---
title: Real-Time CDP Guardrails
description: Läs mer om de olika tjänsterna och områdena i Real-Time CDP.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Real-Time CDP Guardrails

Garantier är trösklar som ger vägledning för data- och systemanvändning, prestandaoptimering och undvikande av fel eller oväntade resultat i Real-Time CDP. Garantier kan avse din användning eller konsumtion av data och bearbetning i relation till dina licensrättigheter.

>[!IMPORTANT]
>
>Kontrollera dina licensrättigheter i din försäljningsorder och motsvarande [produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions.html) om faktiska användningsbegränsningar, utöver den här sidan med skyddsförslag.

Börja här och följ länkarna nedan för att få en förståelse för alla skyddsprofiler för de olika tjänsterna och områdena i Real-Time CDP:

* [Skyddsritningar för dataöverföring](/help/ingestion/guardrails.md)
* [Guardrails för  [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Garantier för  [!DNL Real-Time Customer Profile] data och segmentering](/help/profile/guardrails.md)
* [Skyddsritningar för  [!DNL Identity Service] data](/help/identity-service/guardrails.md)
* [Guardrails för  [!DNL Query Service]](/help/query-service/guardrails.md)
* [Garantier för dataaktivering via destinationer](/help/destinations/guardrails.md)
* [Guardrails för Real-Time CDP B2B](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>Besök även [planerna för digitala upplevelser](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) om du vill ha mer information, till exempel [heltidsdiagram](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.

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
* [Real-time Customer Data Platform (B2C-utgåva - Premiere- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P-utgåva - Premiere- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B-utgåva - Premiere- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Skyddsritningar för andra Experience Platform-program  {#guardrails-other-aep-apps}

Det finns liknande skyddsräcken för andra Experience Platform-program. Mer information finns på länkarna nedan:

* [Adobe Journey Optimizer skyddsräcken](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [Customer Journey Analytics skyddsräcken](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## Nästa steg

När du har förstått vilka skyddsutkast som gäller för olika områden och tjänster i Real-Time CDP kan du följa med i ett [exempel på användning av en Real-Time CDP-implementering](/help/rtcdp/get-started.md).
