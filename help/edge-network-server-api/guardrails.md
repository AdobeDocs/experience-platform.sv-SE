---
title: Servicenivåavtal och -mål
description: Lär dig hur du konfigurerar autentisering för API:t för Edge Network Server
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: datainsamling;samling;edge network;api;sla;slt;service levels
hide: true
hidefromtoc: true
source-git-commit: 50a688e2f19f4fda2fc4cca823edb5886ad32bba
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---


# Guardrails

## Översikt {#overview}

Adobe kommer att göra kommersiellt rimliga ansträngningar för att [!DNL Server API] som är tillgängliga inom en månatlig drifttid på minst 99,9 % för varje region, under varje månatlig faktureringscykel.

## Definitioner

* **Tillgänglighet** beräknas för varje femminutersintervall som den procentandel begäranden som bearbetas av Experience Adobe Experience Platform Edge Network och som inte misslyckas med fel och som endast gäller de Adobe Experience Platform Edge Network API:er som tillhandahålls. Om en klientorganisation inte har gjort några förfrågningar under ett givet femminutersintervall anses det intervallet vara 100 % tillgängligt.
* **Procentvärde för månatlig drifttid** för ett givet område beräknas som medelvärdet av tillgängligheten för alla femminutersintervall under en månad.
* An **uppström** är en tjänst bakom Adobe Edge Network, som har aktiverats för ett specifikt datastream, till exempel Adobe Server Side Forwarding, Adobe Edge Segmentation eller Adobe Target.
* A **förfrågan** som skickas till Server-API:t definieras som en eller flera begärandatsenheter.
* A **begärandeenhet** motsvarar ett 8 kB-fragment av en begäran och ett uppströms konfigurerat för ett datastream.
* An **fel** är en begäran som misslyckas på grund av ett Adobe Experience Platform Edge Network [internt tjänstfel](error-handling.md).

## Interna mål

Adobe ingenjörsteam driftsätter nära telemetri i realtid, övervakning och utskalning för att säkerställa följande mål:

* Mindre än 1 % av HTTP-begäranden returnerar `5xx` fel de senaste fem minuterna
* Färre än 1 % av uppströmsanslutningarna returnerar ett fel under de senaste fem minuterna
* En eventuell innehavarkapacitet fördubblas på mindre än 10 minuter från det att en gräns nås.

## Undantag för serviceavtal

Det åtagande på tjänstenivå som beskrivs ovan gäller inte problem med tillgänglighet eller prestanda som orsakas av följande händelser:

* Faktorer som ligger utanför vår rimliga kontroll, inklusive Internet-åtkomst eller relaterade problem utanför Adobe infrastruktur.
* All felaktig användning av [!DNL Server API], enligt de gränser som anges nedan.

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

| Nyttolastformat | Maximal storlek för en begäran | Max 8 kB begärandefragment |
| --- | --- | --- |
| JSON normal text | 64 kB | 8 |


>[!NOTE]
>
>Beroende på nyttolasten är binära format i allmänhet 20-40 % mer kompakta, vilket gör att du kan skicka mer data än vad du skulle göra med vanlig JSON. Kontakta din kundtjänstrepresentant om du behöver en högre kapacitet för dina dataströmmar.

