---
title: Licenshantering och kapacitet
description: Läs mer om licensanvändningen och kapacitetsbegränsningarna i Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: b3b0792a1a1dd5270dec697539ed58d895814fc8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# Licensanvändning och licenskapacitet

I Adobe Experience Platform kan du ta reda på om din organisation har överskridit några av dina skyddsprofiler och få information om hur du åtgärdar dessa problem.

Mer information om skyddsutkast i Experience Platform finns i [Real-Time CDP skyddsöversikt](../../rtcdp/guardrails/overview.md).

## Kapacitet, beteende {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Strömmande genomströmning"
>abstract="Värdet för direktuppspelningsgenomströmning mäter de kombinerade topphändelserna för inkommande trafik per sekund för direktuppspelning till profiltjänsten, i alla dina produktions- och utvecklingssandlådor."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Antal direktuppspelade målgrupper"
>abstract="Maximalt antal direktuppspelade målgrupper per sandlåda. Detta antal är inklusive antalet kantmålgrupper du har i din sandlåda."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Edge målgrupper"
>abstract="Maximalt antal kantmålgrupper per sandlåda."

För närvarande stöder Capacity följande tjänster:

- Direktuppspelningssegmentering
- Direktinmatning

Inom dessa tjänster spåras följande skyddsräcken:

- Maximalt antal direktuppspelade målgrupper är 500
   - Av dessa 500 direktuppspelade målgrupper är det maximala antalet kantmålgrupper 150
- Maximal kombinerad genomströmning för direktuppspelningssegmentering är 1 500 poster per sekund (rps)

Målgruppskapaciteten är på en **sandbox**-nivå. Det innebär att ni för varje sandlåda ni har i organisationen kan ha 500 direktuppspelade målgrupper, varav 150 av dessa kan vara gränspubliken.

Genomströmningskapaciteten är på **organisationsnivå** och kan distribueras till dina enskilda sandlådor. Med till exempel 1500 rps för direktuppspelad segmenteringsgenomströmning kan du ange att din produktionssandlåda ska vara 1500 rps och att din utvecklingssandlåda ska vara 150 rps.

Experience Platform beräknar sandlådans genomströmning i 15 minuters rullande intervall. Detta genomflöde mäts i realtid och data uppdateras var 60:e sekund.

Om din användning når upp till 80 % och 90 % av den licensierade kapaciteten skickar Experience Platform ut ett varningsmeddelande som meddelar att du har nått den angivna kapaciteten. Du kan ändra inställningarna för att anpassa kapacitetsprocenten för att ta emot aviseringen eller ta bort aviseringen helt.

Om din användning överstiger 100 % av den licensierade kapaciteten anses du bryta mot din kapacitet. I det här skedet kommer du att uppleva prestandatlatens och dina servicenivåmål (SLT) **inte** kommer att garanteras.

## Vanliga frågor och svar

I följande avsnitt beskrivs vanliga frågor om kapacitet.

### Kan jag ha en maximal kombinerad genomströmningsgräns som summerar till mindre än min högsta målgräns?

+++ Svar

Nej. Den maximala sammanlagda genomströmningsgränsen **måste** summeras till din organisations säkerhetsgräns.

+++

### Vad händer om jag överskrider min maximala kapacitet?

+++ Svar

Detta beror på vilken kapacitet som överskrids.

Om du för närvarande överskrider det högsta tillåtna antalet målgrupper påverkas inte de överdrivna målgrupperna. Möjligheten att skapa nya målgrupper kan dock begränsas i framtiden.

Om du överskrider strömningsflödet kommer du att uppleva prestandatlatens i din inmatning och segmentering.

+++

### Varför ska jag hålla mig till min maximala kapacitet?

+++ Svar

Om ni arbetar inom era maximala möjligheter kan ni säkerställa att era data är enhetliga och att dataintegriteten är intakt.

Ni ser till att resultatet blir konsekvent vid högbelastade händelser och undviker tekniska problem som kan påverka systemets prestanda negativt och påverka kundupplevelserna längre fram i kedjan, vilket i slutänden förbättrar er datthygien och övergripande systemprestanda.

+++

### Vilka är de bästa sätten att hantera direktuppspelad segmenteringsgenomströmning?

+++ Svar

För att hantera strömmande segmenteringsgenomströmning på bästa sätt bör ni utvärdera era datauppsättningar och försäkra er om att de prioriterar de data som behövs för personalisering.


Om realtidsbearbetning inte behövs bör du använda batchinmatning i stället för direktuppspelning.

+++
