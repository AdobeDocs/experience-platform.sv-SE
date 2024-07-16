---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;data prep;data preparing;preparing data;
solution: Experience Platform
title: Dataförhandsgranskning
description: I det här dokumentet introduceras Data Prep i Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '789'
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
>Om inte det resulterande meddelandet blir ogiltig XDM, kommer eventuella transformeringsfel i Data Prep att resultera i att attributen anges till `null`, medan resten av raden kommer att kapslas. Om raden leder till ogiltig XDM, kommer raden **inte** att kapslas. I båda dessa fall dokumenteras felet.

## Mappning

En mappning är en association av ett indataattribut eller beräknat fält till ett XDM-attribut. Ett enda attribut kan mappas till flera XDM-attribut genom att skapa enskilda mappningar.

Mer information om de olika mappningsfunktionerna finns i [guiden för mappningsfunktioner](./functions.md).

### Beräknade fält

Beräknade fält tillåter att värden skapas baserat på attributen i indatabladet. Dessa värden kan sedan tilldelas attribut i målschemat och ges ett namn och en beskrivning som gör det enklare att referera till. Beräknade fält får innehålla högst 4 096 tecken.

Om du vill veta mer om beräknade fält kan du läsa [handboken om beräknade fält](./functions.md#calculated-fields).

### Esc-specialtecken {#escape-special-characters}

Du kan undvika specialtecken i ett fält genom att använda `${...}`. JSON-filer som innehåller fält med en punkt (`.`) stöds dock inte av den här funktionen. Om ett underordnat attribut har en punkt (`.`) vid interaktion med hierarkier måste du använda ett omvänt snedstreck (`\`) för att undvika specialtecken. `address` är till exempel ett objekt som innehåller attributet `street.name`, som sedan kan kallas `address.street\.name` i stället för `address.street.name`.

## Mappningsuppsättning

En uppsättning mappningar som omformar ett schema till ett annat kallas tillsammans för en mappningsuppsättning. En enda mappningsuppsättning skapas som en del av varje dataflöde. En mappningsuppsättning är en integrerad del av dataflödena och skapas, redigeras och övervakas som en del av dataflödena.

Om du vill veta mer om mappningsuppsättningar, inklusive hur du använder fälten i en mappningsuppsättning, kan du läsa [guiden för mappningsuppsättning](./mapping-set.md). Om du vill lära dig hur du skapar en mappningsuppsättning och använder andra API-anrop som är relaterade till mappningsuppsättningar läser du avsnittet om mappningsuppsättning i [utvecklarhandboken](./api/mapping-set.md).

## Dataformatshantering

Data Prep kan hantera olika dataformat som importerats till Platform på ett robust sätt. Läs [översikten över dataformatshantering](./data-handling.md) om du vill veta mer om hur dataprep hanterar olika datatyper.

## Skicka uppdateringar av delar av rader med [!DNL Data Prep]

Med direktuppspelande uppdateringar i [!DNL Data Prep] kan du skicka partiella raduppdateringar till [!DNL Profile Service]-data samtidigt som du skapar och upprättar nya identitetslänkar med en enda API-begäran. Mer information om hur du direktuppspelar uppladdningar i [!DNL Data Prep] finns i dokumentet om att [skicka uppdateringar till delar av rader](./upserts.md).

## Attributbaserad åtkomstkontroll i [!DNL Data Prep]

Med attributbaserad åtkomstkontroll i Adobe Experience Platform kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut.

Attributbaserad åtkomstkontroll ser till att du bara kan mappa de attribut du har tillgång till. Attribut som du inte har åtkomst till kan inte användas i direktmappningar och beräkningsfält. Om du inte har åtkomst till ett obligatoriskt fält kan du inte spara en mappning. Du kan inte heller mappa objekt eller objektarrayer om du inte har tillgång till något av de underordnade attributen. Du kan dock mappa andra element inom objektet eller objektarrayen separat.

Mer information finns i [attributbaserad åtkomstkontroll](../access-control/abac/overview.md).

## Nästa steg

Det här dokumentet beskriver grunderna för Data Prep i Adobe Experience Platform. Om du vill veta mer om olika mappningsfunktioner kan du läsa [guiden för mappningsfunktioner](./functions.md). Läs [Handboken för dataformatshantering](./data-handling.md#dates) om du vill veta mer om hur dataprep hanterar olika datatyper. Läs [Utvecklarhandboken för dataförberedelser](api/overview.md) om du vill lära dig hur du använder API:t för dataförberedelser.
