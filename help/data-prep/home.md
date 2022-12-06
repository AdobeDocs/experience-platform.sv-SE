---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;data prep;data preparing;preparing data;
solution: Experience Platform
title: Dataförhandsgranskning
topic-legacy: overview
description: I det här dokumentet introduceras Data Prep i Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 61603d7516dbd859b0cce6c167c75aab42ca7171
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---


# Översikt över datapreflight

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM). Dataförinställning visas som ett steg för&quot;Karta&quot; i dataöverföringsprocesserna, inklusive arbetsflödet för CSV-inmatning. Datatekniker kan använda Data Prep för att utföra följande dataändringar vid förtäring:

- Definiera enkla direktmappningar för att tilldela indataattribut till XDM-attribut
- Skapa beräkningsfält för att utföra radberäkningar som kan tilldelas XDM-attribut
- Omforma data genom att använda strängar, numeriska funktioner eller datumfunktioner
- Skapa XDM-hierarkier med hjälp av hierarkiska funktioner
- Förhandsgranska data när de ändras i datapresentationen

Data Prep använder också flera inbyggda datavalideringar för att säkerställa att dataintegriteten bevaras när den importeras. När det är möjligt mappar Data Prep automatiskt inkommande datamodeller till XDM. Datatekniker kan ändra, korrigera och ta bort de föreslagna mappningarna och ersätta dem med mappningarna efter behov.

>[!NOTE]
>
>Om inte det resulterande meddelandet blir ogiltig XDM, kommer eventuella transformeringsfel i Data Prep att resultera i att attributen anges till `null`medan resten av raden kommer att kapslas. Om raden blir ogiltig XDM kommer raden att **not** vara förtjust. I båda dessa fall dokumenteras felet.

## Mappning

En mappning är en association av ett indataattribut eller beräknat fält till ett XDM-attribut. Ett enda attribut kan mappas till flera XDM-attribut genom att skapa enskilda mappningar.

Läs mer om de olika mappningsfunktionerna i [guide för mappningsfunktioner](./functions.md).

### Beräknade fält

Beräknade fält tillåter att värden skapas baserat på attributen i indatabladet. Dessa värden kan sedan tilldelas attribut i målschemat och ges ett namn och en beskrivning som gör det enklare att referera till. Beräknade fält får innehålla högst 4 096 tecken.

Läs mer om beräknade fält i [guide för beräknade fält](./functions.md#calculated-fields).

### Esc-specialtecken {#escape-special-characters}

Du kan undvika specialtecken i ett fält genom att använda `${...}`. JSON-filer som innehåller fält med punkt (`.`) stöds inte av den här mekanismen. Vid interaktion med hierarkier, om ett underordnat attribut har en punkt (`.`) måste du använda ett omvänt snedstreck (`\`) för att undvika specialtecken. Till exempel: `address` är ett objekt som innehåller attributet `street.name`kan det sedan kallas `address.street\.name` i stället för `address.street.name`.

## Mappningsuppsättning

En uppsättning mappningar som omformar ett schema till ett annat kallas tillsammans för en mappningsuppsättning. En enda mappningsuppsättning skapas som en del av varje dataflöde. En mappningsuppsättning är en integrerad del av dataflödena och skapas, redigeras och övervakas som en del av dataflödena.

Läs mer om mappningsuppsättningar, inklusive hur du använder fälten i en mappningsuppsättning i [guide för mappningsuppsättning](./mapping-set.md). Om du vill lära dig hur du skapar en mappningsuppsättning och använder andra API-anrop som är kopplade till mappningsuppsättningar läser du avsnittet om mappningsuppsättning i [utvecklarhandbok](./api/mapping-set.md).

## Dataformatshantering

Data Prep kan hantera olika dataformat som importerats till Platform på ett robust sätt. Läs mer om hur dataprep hanterar olika datatyper i [dataformatshantering - översikt](./data-handling.md).

## Skicka uppdateringar av delar av rader med [!DNL Data Prep]

Direktuppspelande överföringar i [!DNL Data Prep] kan du skicka uppdateringar av delar av rader till [!DNL Profile Service] data samtidigt som nya identitetslänkar skapas och etableras med en enda API-begäran. Mer information om hur du direktuppspelar överföringar i [!DNL Data Prep], se dokumentet på [skicka uppdateringar med partiella rader](./upserts.md).

## Attributbaserad åtkomstkontroll i [!DNL Data Prep]

Med attributbaserad åtkomstkontroll i Adobe Experience Platform kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut.

Attributbaserad åtkomstkontroll ser till att du bara kan mappa de attribut du har tillgång till. Attribut som du inte har åtkomst till kan inte användas i direktmappningar och beräkningsfält. Om du inte har åtkomst till ett obligatoriskt fält kan du inte spara en mappning. Du kan inte heller mappa objekt eller objektarrayer om du inte har tillgång till något av de underordnade attributen. Du kan mappa andra element inom objektet eller objektarrayen separat.

Se [attributbaserad åtkomstkontroll - översikt](../access-control/abac/overview.md) för mer information.

## Nästa steg

Det här dokumentet beskriver grunderna för Data Prep i Adobe Experience Platform. Läs mer om olika mappningsfunktioner i [guide för mappningsfunktioner](./functions.md). Läs mer om hur dataprep hanterar olika datatyper i [guide för hantering av dataformat](./data-handling.md#dates). Läs mer om hur du använder API:t för dataförberedelser i [Utvecklarhandbok för dataprep](api/overview.md).
