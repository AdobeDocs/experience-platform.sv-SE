---
title: Prestandaskydd för Edge Network Server API
description: Lär dig hur du använder server-API:t med optimala prestandaresäkerhetsprofiler.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---


# Prestandaskydd för Edge Network Server API

## Översikt {#overview}

Prestandaskydd definierar användningsgränser som relaterar till användningsfall för Server API. Om du överskrider de prestandaskydd som beskrivs i den här artikeln kan prestandan försämras.

Adobe ansvarar inte för prestandaförsämringar orsakade av överskridna användningsgränser. Kunder som genomgående överskrider prestandaskyddsrutinerna kan begära ytterligare bearbetningskapacitet för att undvika prestandaförsämringar.

## Definitioner

* **Tillgänglighet** beräknas för varje femminutersintervall som procentandelen begäranden som bearbetas av Experience Platform Edge Network som inte misslyckas med fel och som endast gäller de tilldelade Edge Network API:erna. Om en klientorganisation inte har gjort några förfrågningar under ett givet femminutersintervall anses det intervallet vara 100 % tillgängligt.
* **Procentvärde för månatlig drifttid** för ett givet område beräknas som medelvärdet av tillgängligheten för alla femminutersintervall under en månad.
* An **uppströms** är en tjänst bakom Edge Network, som är aktiverad för ett specifikt datastream, till exempel Adobe Server Side Forwarding, Adobe Edge Segmentation eller Adobe Target.
* A **begärandeenhet** motsvarar ett 8 kB-fragment av en begäran och ett uppströms konfigurerat för ett datastream.
* A **förfrågan** är ett enda meddelande som skickas av ett kundägt program till [!DNL Server API]. En begäran kan innehålla en eller flera begärandeenheter.
* An **fel** är en begäran som misslyckas på grund av ett Edge Network [internt tjänstfel](error-handling.md).

## Tjänstbegränsningar

Alla datastreams tillämpar vissa användarbegränsningar, som huvudsakligen styr hur många händelser som kan skickas samtidigt, deras storlek och antalet tjänster i det föregående flödet som dessa begäranden dirigeras till.

### Begär enheter

Alla begränsningar tillämpas och normaliseras över en **begärandeenhet (RU)**, definierad som **8 kB-fragment** av en begäran som går till en tjänst som är konfigurerad i ett datastream.

#### Exempel

| Uppdateringar konfigurerade per datastream | Genomsnittlig begärandestorlek | Begär enheter |
| --- | --- | --- |
| 1 (Adobe Platform) | 8 kB (1 fragment) | 1 |
| 2 (Adobe Platform, Adobe Target) | 8 kB (1 fragment) | 2 |
| 2 (Adobe Platform, Adobe Target) | 16 kB (2 fragment) | 4 |
| 2 (Adobe Platform, Adobe Target) | 64 kB (8 fragment) | 16 |

### Gränser för begärandeenheter

Tabellen nedan visar standardgränsvärdena. Om du behöver större enhetsgränser för beställningar, kontakta din kontorepresentant.

| Slutpunkt | Begäranenheter per sekund |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Storleksgräns för HTTP-begäran

| Betalningsformat | Maximal storlek för en begäran | Max 8 kB begärandefragment |
| --- | --- | --- |
| JSON normal text | 64 kB | 8 |


>[!NOTE]
>
>Beroende på nyttolasten är binära format i allmänhet 20-40 % mer kompakta, vilket gör att du kan skicka mer data än vad du skulle göra med vanlig JSON. Kontakta din kundtjänstrepresentant om du behöver en högre kapacitet för dina dataströmmar.

## Nästa steg

Följande dokumentation innehåller mer information om andra Experience Platform-servicesäkrar, om total latenstid och licensinformation från Real-Time CDP produktbeskrivningsdokument:

* [Real-Time CDP skyddsräcken](/help/rtcdp/guardrails/overview.md)
* [Latensdiagram från början till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.
* [Real-time Customer Data Platform (B2C Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
