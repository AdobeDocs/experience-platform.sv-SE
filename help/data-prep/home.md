---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data prep;data preparation;preparing data;
solution: Experience Platform
title: Mappningsfunktioner
topic: overview
description: I det här dokumentet introduceras Data Prep i Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Dataprep

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM). Dataförinställning visas som ett steg för&quot;Karta&quot; i dataöverföringsprocesserna, inklusive arbetsflödet för CSV-inmatning. Datatekniker kan använda Data Prep för att utföra följande dataändringar vid förtäring:

- Definiera enkla direktmappningar för att tilldela indataattribut till XDM-attribut
- Skapa beräkningsfält för att utföra radberäkningar som kan tilldelas XDM-attribut
- Omforma data genom att använda strängar, numeriska funktioner eller datumfunktioner
- Skapa XDM-hierarkier med hjälp av hierarkiska funktioner
- Förhandsgranska data när de ändras i datapresentationen

Data Prep använder också flera inbyggda datavalideringar för att säkerställa att dataintegriteten bevaras när den importeras. När det är möjligt mappar Data Prep automatiskt inkommande datamodeller till XDM. Datatekniker kan ändra, korrigera och ta bort de föreslagna mappningarna och ersätta dem med mappningarna efter behov.

## Mappning

En mappning är en association av ett indataattribut eller beräknat fält till ett XDM-attribut. Ett enda attribut kan mappas till flera XDM-attribut genom att skapa enskilda mappningar.

Mer information om de olika mappningsfunktionerna finns i [guiden](./functions.md)för mappningsfunktioner.

## Mappningsuppsättning

En uppsättning mappningar som omformar ett schema till ett annat kallas tillsammans för en mappningsuppsättning. En enda mappningsuppsättning skapas som en del av varje dataflöde. En mappningsuppsättning är en integrerad del av dataflödena och skapas, redigeras och övervakas som en del av dataflödena.

## Nästa steg

Det här dokumentet beskriver grunderna för Data Prep i Adobe Experience Platform. Mer information om olika mappningsfunktioner finns i [guiden](./functions.md)för mappningsfunktioner. Mer information om de olika datumtidssträngarna finns i [strängguiden](./dates.md).