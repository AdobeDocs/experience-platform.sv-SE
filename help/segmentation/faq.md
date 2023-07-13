---
title: Frågor och svar
description: Hitta svar på vanliga frågor om målgrupper.
source-git-commit: 562af647e21e8f9b9af495849f085e10f258952a
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---


# Frågor och svar

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från [!DNL Real-Time Customer Profile] data. Dessa målgrupper är centralt konfigurerade och underhållna på Platform och är tillgängliga för alla Adobe-lösningar. Nedan följer en lista med vanliga frågor om målgrupper och segmentering.

## Har jag tillgång till Audience Portal och Audience Composition?

Audience Portal och Audience Composition är tillgängliga för alla Real-Time CDP Prime- och Ultimate-kunder (B2C, B2B och B2P Editions) och Journey Optimizer Select-, Prime-, Ultimate Starter- och Ultimate-kunder.

I nuläget stöds endast profilbaserade målgrupper. Stöd för kontobaserade målgrupper kommer att läggas till i en senare version.

## Stöds externt genererade förbyggda målgrupper med Audience Portal?

Ja, externt genererade färdiga målgrupper stöds med Audience Portal. Nu kan du importera en externt genererad publik via en CSV-fil. I framtiden kommer ni att kunna lägga till målgrupper via batchanslutningar eller direktuppspelningsbaserade källkopplingar.

## Kan jag stämma av externt genererade målgruppsdata med en befintlig profil i Platform?

Ja, den externt genererade målgruppen sammanfogas med den befintliga profilen i plattformen om de primära identifierarna matchar. Det kan ta upp till 24 timmar att stämma av dessa data. Om det inte redan finns profildata skapas en ny profil när data hämtas.

## Kan jag använda en externt genererad publik för att bygga andra målgrupper?

Ja, alla externt genererade målgrupper visas i målgruppslagret och kan användas när målgrupper byggs inom [Segment Builder](./ui/segment-builder.md).

## Kan jag använda externt överförda attribut som en del av segmenteringen?

Nej, det kan du inte. Profilattribut är avsedda att vara långvariga attribut, medan externt genererade målgruppsdata som överförs bara innehåller kontextuella data som är kopplade till den externt genererade målgruppen.

Den externt genererade målgruppens kontextuella data, eller anrikningsattribut, är **not** de är långvariga, eftersom deras livscykel är knuten till den överförda publiken. På grund av sin övergående karaktär är dessa anrikningsattribut därför **not** som kan användas vid segmentering.

Men när ni mappar era målgrupper till batch- eller filbaserade mål kan ni använda dessa externt genererade berikande attribut för att förstärka era målgrupper och ytterligare aktiveringar i senare led.

Om du vill veta mer om den här funktionen kan du läsa guiden på [aktivera målgruppsdata till exportmål för gruppprofiler](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Kan jag aktivera externt genererade målgrupper för Adobe Journey Optimizer?

Vid den här tidpunkten, nej. Den här funktionen kommer dock att vara tillgänglig inom den närmaste framtiden.

## Kan jag ta bort en externt genererad publik?

Vid den här tidpunkten, nej. Du kan antingen inaktivera eller arkivera den här målgruppen istället. I det här läget, profiler **kommer** förbli aktiva för användning i nedströmstillämpningar. Stöd för att ta bort externt genererade målgrupper läggs till i en senare version.

## Hur interagerar Audience Portal och Audience Composition med Real-Time CDP Partner Data?

Målportalen och målgruppskompositionen samverkar med partnerdata på två sätt:

1. Om du importerar en lista över potentiella kunder som tillhandahållits av en partner med hjälp av klassen Prospect Profile och arbetsflödet behålls dessa potentiella kunder **separat** från att sammanfoga kundprofiler i profiltjänsten. Detta innebär att listor över potentiella kunder **not** visas i antingen Audience Portal eller Audience Composition för användning.
2. Om du använder attribut som tillhandahålls av partners för att berika **befintlig** förstahandsprofiler, dessa målgrupper som bygger på partnerdata **kommer** visas i både Audience Portal och Audience Composition för användning.

## Kan jag använda externt genererade målgrupper i Audience Composition?

Vid den här tidpunkten, nej. Denna kapacitet bör dock vara tillgänglig inom den närmaste framtiden.

## Kan jag skicka målgrupper från Audience Composition till alla destinationer och kanaler längre fram i kedjan?

Vid den här tidpunkten, nej. För närvarande kan ni använda målgrupper från Audience Composition i Adobe Journey Optimizer Campaigns och CDP-destinationer i realtid. Adobe Journey Optimizer Journeys kommer att få stöd i en kommande version.

## Finns det några skyddsräcken för antalet kompositioner?

För tillfället kan du bara ha **10** publicerade kompositioner per sandlåda. Garantin planeras att utökas i en framtida version.

## Vilka är arbetsflödesgarantierna för Audience Composition?

Komponentplaceringen följer en hård struktur enligt följande:

1. Du **alltid** börja med [!UICONTROL Audience] -block för att välja din startaktivitet. Du kan ha högst **en** [!UICONTROL Audience] -block.
2. Du kan lägga till en [!UICONTROL Exclude] -block som följer [!UICONTROL Audience] -block.
3. Du kan lägga till en [!UICONTROL Rank] eller [!UICONTROL Split] -block. Du kan **endast** har ett av dessa block per komposition.
4. Du **alltid** end with a [!UICONTROL Save] blockera för att rädda er målgrupp.

Mer information om hur du använder Audience Composition finns i [Användargränssnittsguide för målgruppskomposition](./ui/audience-composition.md).

## Kan jag använda en Audience Composition i en annan komposition?

Nej, målgrupper skapade med Audience Composition **inte** användas som indata i en annan målgruppssammansättning.

## Hur fungerar delning i Audience Composition?

Genom att dela målgrupper kan ni ytterligare dela upp er målgrupp i mindre grupper. Denna delning tvingar fram ömsesidigt uteslutande mellan grupperna. Det innebär att om en post uppfyller villkoren för flera delade sökvägar tilldelas den **först** till vänster och **not** som tilldelats någon av de andra sökvägarna.

Mer information om det delade blocket finns i [Användargränssnittsguide för målgruppskomposition](./ui/audience-composition.md#split).

## Kan jag använda alla segmenteringstyper i arbetsflödet Målgruppskomposition?

Ja, alla segmenteringstyper (gruppsegmentering, direktuppspelningssegmentering och kantsegmentering) stöds i arbetsflödet för målgruppssammansättning. Men eftersom kompositioner för närvarande bara körs en gång per dag, även om en målgrupp som är en direktuppspelnings- eller edge-utvärderad målgrupp inkluderas, kommer resultatet att baseras på målgruppsmedlemskap när kompositionen utfördes.

## Hur kan jag bekräfta en profils medlemskap för en viss målgrupp?

Om du vill bekräfta en profils målgruppsmedlemskap går du till sidan med profilinformation för den profil du vill bekräfta. Välj **[!UICONTROL Attributes]**, följt av **[!UICONTROL View JSON]** och du kan bekräfta att `segmentMembership` -objektet innehåller målgruppens ID.
