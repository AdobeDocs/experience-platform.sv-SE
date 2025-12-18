---
description: Lär dig hur Experience Platform hanterar olika typer av fel som returneras av direktuppspelningsmål och hur det försöker skicka data till målplattformen igen.
title: Regler för hastighetsbegränsning och återförsök för direktuppspelningsmål som skapats med Destination SDK
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Regler för hastighetsbegränsning och återförsök för direktuppspelningsmål som skapats med Destination SDK

Partnerbyggda destinationer kan returnera olika fel och ha olika hastighetsbegränsande principer. På den här sidan beskrivs hur Experience Platform hanterar olika typer av fel som returneras av direktuppspelningsmål.

När du konfigurerar ett mål med Destination SDK kan du välja mellan två aggregeringstyper - [bästa ansträngningsaggregering](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) och [konfigurerbar aggregering](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). Beroende på vilken aggregeringstyp du väljer kan du läsa nedan om hur Experience Platform hanterar fel och hastighetsbegränsningar.

## Bästa ansträngningsaggregering {#best-effort-aggregation}

Experience Platform försöker att returnera följande HTTP-svarskoder: **403, 408, 409, 429, 500, 502, 503, 504**. Två försök görs med följande intervall:

* Första försöket: efter 15 sekunder
* Andra försök: efter 30 sekunder

Experience Platform försöker *inte* anrop som returnerar andra HTTP-svarskoder, till exempel 400 (Ogiltig begäran). Om samtalet fortfarande misslyckas efter båda återförsöken, avbryter Experience Platform aktiveringen och försöker inte göra om den.

Du kan begära en annan återförsöksprincip för specifika dataflöden genom att kontakta kundsupport.

## Konfigurerbar aggregering {#configurable-aggregation}

När det gäller destinationsplattformar som har konfigurerats med konfigurerbar aggregering skiljer Experience Platform mellan den feltyp som returneras av din plattform:

* Fel där Experience Platform försöker skicka data till din plattform igen:
   * HTTP-svarskoder 420 och 429
   * HTTP-svarskoder större än 500
* Fel där Experience Platform *inte* försöker skicka data till din plattform igen: alla andra som returneras av din plattform

### Återförsöksmetod beskrivs {#retry-approach}

Experience Platform metod för konfigurerbar aggregering beskrivs nedan. I det här exemplet antas att Experience Platform skickar data till en målplattform som börjar returnera 429 felkoder om den tar emot mer än 50 kB begäranden per minut:

* Minut 1: Experience Platform samlar 40 000 batchar med profiler som skickas till målplattformen. Experience Platform gör 40 kB HTTP-begäranden och alla är lyckade.
* Minut 2: Experience Platform samlar 70 000 batchar med profiler som ska skickas till målplattformen. Experience Platform gör 70 kB HTTP-begäranden och 50 kB lyckas. Den andra 20 kB-filen får ett hastighetsbegränsande fel från slutpunkten och kommer att provas igen om 30 minuter.
* Minut 3: Experience Platform samlar 30 000 batchar med profiler som skickas till målplattformen. Experience Platform gör 30 kB HTTP-begäranden och alla är lyckade.
* ...
* ...
* Minut 32: Experience Platform försöker skicka de 20 kB-batchar som misslyckades vid minut 2. Alla samtal är slutförda.

## Nästa steg {#next-steps}

Du vet nu hur Experience Platform hanterar fel och hastighetsbegränsning från målplattformar, beroende på den aggregeringsprincip du valde när du konfigurerade ditt mål för direktuppspelning. Därefter kan du läsa följande dokumentation:

* [Testa målkonfigurationen](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Skicka för granskning till ett mål som skapats i Destination SDK](../guides/submit-destination.md)
