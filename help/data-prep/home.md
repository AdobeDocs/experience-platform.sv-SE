---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;data prep;data preparing;preparing data;
solution: Experience Platform
title: Dataförhandsgranskning
topic: overview
description: I det här dokumentet introduceras Data Prep i Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: 827a593c046530edba701edf26d9a47918cfd8f8
workflow-type: tm+mt
source-wordcount: '389'
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

## Mappning

En mappning är en association av ett indataattribut eller beräknat fält till ett XDM-attribut. Ett enda attribut kan mappas till flera XDM-attribut genom att skapa enskilda mappningar.

Läs guiden [mappningsfunktioner](./functions.md) om du vill veta mer om de olika mappningsfunktionerna.

## Mappningsuppsättning

En uppsättning mappningar som omformar ett schema till ett annat kallas tillsammans för en mappningsuppsättning. En enda mappningsuppsättning skapas som en del av varje dataflöde. En mappningsuppsättning är en integrerad del av dataflödena och skapas, redigeras och övervakas som en del av dataflödena.

## Dataformatshantering

Data Prep kan hantera olika dataformat som importerats till Platform på ett robust sätt. Om du vill veta mer om hur dataprep hanterar olika datatyper kan du läsa [översikten över dataformatshantering](./data-handling.md).

## Nästa steg

Det här dokumentet beskriver grunderna för Data Prep i Adobe Experience Platform. Läs guiden [mappningsfunktioner](./functions.md) om du vill veta mer om olika mappningsfunktioner. Läs [Handboken för dataformatshantering](./data-handling.md#dates) om du vill veta mer om hur dataprep hanterar olika datatyper. Läs [Utvecklarhandboken för dataprep](api/overview.md) om du vill lära dig hur du använder API:t för dataprep.
