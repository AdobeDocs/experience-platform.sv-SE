---
title: Uppdatering av urvalskriterier för segment
description: Lär dig mer om uppdateringar av kriterier för att välja om du vill ha rätt till segmentering, som påverkar de typer av målgrupper som kan utvärderas med hjälp av strömning och kantsegmentering.
hide: true
hidefromtoc: true
source-git-commit: 0bbee2100ed6fdc0f40457965e195d07de6eb2a1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Uppdatering av urvalskriterier

Från och med den 24 september 2024 kommer två uppdateringar att göras som påverkar möjligheten att segmentera.

1. Frågetyper för strömning och kantsegmentering
2. Sammanslagningspolicyer för direktuppspelning och kantsegmentering

## Frågetyper

Alla **nya eller redigerade**-segmentdefinitioner som matchar följande frågetyper utvärderas **inte längre** med hjälp av direktuppspelning eller kantsegmentering. I stället utvärderas de med gruppsegmentering.

- En enstaka händelse med ett tidsfönster längre än 24 timmar
   - Aktivera en målgrupp med alla profiler som har visat en webbsida de senaste tre dagarna.
- En enda händelse utan tidsfönster
   - Aktivera en målgrupp med alla profiler som visade en webbsida.

Om du behöver utvärdera en segmentdefinition med hjälp av direktuppspelning eller kantsegmentering som matchar den uppdaterade frågetypen, kan du explicit skapa en batch- och direktuppspelningsfråga och kombinera dem med segment.

Om du till exempel behöver aktivera en målgrupp med alla profiler som har visat en webbsida de senaste tre dagarna med direktuppspelningssegmentering, kan du skapa följande frågor:

- Q1 (direktuppspelning): Alla profiler som har visat en webbsida de senaste 24 timmarna
- Q2 (Gruppera): Alla profiler som har visat en webbsida de senaste tre dagarna

Sedan kan ni kombinera dem genom att hänvisa till Q1 eller Q2.

Om du behöver aktivera en målgrupp med alla profiler som visade en webbsida kan du skapa följande frågor:

- Q3 (direktuppspelning): Alla profiler som har visat en webbsida de senaste 24 timmarna
- Q4 (Gruppera): Alla profiler som visade en webbsida.

Sedan kan ni kombinera dem genom att hänvisa till Q3 eller Q4.

>[!IMPORTANT]
>
>Alla befintliga segmentdefinitioner som matchar frågetyperna utvärderas fortfarande med hjälp av strömning eller kantsegmentering tills de redigeras.
>
>Dessutom kommer alla befintliga segmentdefinitioner som för närvarande uppfyller de andra kriterierna för utvärdering av direktuppspelning eller kantsegmentering att utvärderas även fortsättningsvis med hjälp av direktuppspelning eller kantsegmentering.

## Kopplingsprincip

Alla **nya eller redigerade**-segmentdefinitioner som kvalificerar för direktuppspelning eller kantsegmentering **måste** finnas i sammanfogningsprincipen Aktiv på Edge.

Alla befintliga segmentdefinitioner som utvärderas med hjälp av direktuppspelning eller kantsegmentering fortsätter att fungera som de är.
