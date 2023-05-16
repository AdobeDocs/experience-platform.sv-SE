---
description: Lär dig hur Experience Platform hanterar olika typer av fel som returneras av direktuppspelningsdestinationer och hur det försöker skicka data till målplattformen igen.
title: Hastighetsbegränsning och återförsöksprincip för direktuppspelningsmål som skapats med Destination SDK
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Hastighetsbegränsning och återförsöksprincip för direktuppspelningsmål som skapats med Destination SDK

Partnerbyggda destinationer kan returnera olika fel och ha olika hastighetsbegränsande principer. På den här sidan beskrivs hur Experience Platform hanterar olika typer av fel som returneras av direktuppspelningsmål.

När du konfigurerar ett mål med Destination SDK kan du välja mellan två aggregeringstyper - [bästa ansträngningsaggregering](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) och [konfigurerbar aggregering](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). Beroende på vilken aggregeringstyp du väljer kan du läsa nedan hur Experience Platform hanterar fel och hastighetsbegränsningar.

## Bästa ansträngningsaggregering {#best-effort-aggregation}

För HTTP-anrop som görs till destinationen och som misslyckas, försöker Experience Platform ringa anropet igen en gång till omedelbart efter det första anropet. Om samtalet fortfarande misslyckas vid det andra försöket, avbryter Experience Platform samtalet och försöker inte göra om det en tredje gång.

## Konfigurerbar aggregering {#configurable-aggregation}

När det gäller målplattformar som har konfigurerats med konfigurerbar aggregering skiljer Experience Platform mellan den feltyp som returneras av din plattform:

* Fel där Experience Platform försöker skicka data till din plattform igen:
   * HTTP-svarskoder 420 och 429
   * HTTP-svarskoder större än 500
* Fel där Experience Platform *inte* försök att skicka data till din plattform igen: alla andra som returneras av din plattform

### Återförsöksmetod beskrivs {#retry-approach}

Experience Platform för konfigurerbar aggregering beskrivs nedan. I det här exemplet antas att Experience Platform skickar data till en målplattform som börjar returnera 429 felkoder om den tar emot mer än 50 kB begäranden per minut:

* Minut 1: Experience Platform aggregerar 40 000 batchar med profiler som skickas till målplattformen. Experience Platform gör 40 kB HTTP-begäranden och alla fungerar.
* Minut 2: Experience Platform aggregerar 70 000 batchar med profiler som skickas till målplattformen. Experience Platform gör 70 kB HTTP-begäranden och 50 kB lyckas. Den andra 20 kB-filen får ett hastighetsbegränsande fel från slutpunkten och kommer att provas igen om 30 minuter.
* Minut 3: Experience Platform aggregerar 30 000 batchar med profiler som skickas till målplattformen. Experience Platform gör 30 kB HTTP-begäranden och alla fungerar.
* ...
* ...
* 32 minuter: Experience Platform försöker skicka de 20 kB-batchar som misslyckades vid minut 2. Alla samtal är slutförda.

## Nästa steg {#next-steps}

Du vet nu hur Experience Platform hanterar fel och hastighetsbegränsning från målplattformar, beroende på den aggregeringsprincip du valde när du konfigurerade ditt direktuppspelningsmål. Därefter kan du läsa följande dokumentation:

* [Testa målkonfigurationen](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Skicka för granskning av ett mål som skapats i Destination SDK](../guides/submit-destination.md)
