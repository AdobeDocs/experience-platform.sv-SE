---
title: Uppdatering av urvalskriterier för segment
description: Lär dig mer om uppdateringar av kriterier för att välja om du vill ha rätt till segmentering, som påverkar de typer av målgrupper som kan utvärderas med hjälp av strömning och kantsegmentering.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: 2af73be351cb818862006adc8d0f1a33f95d93cf
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Uppdatering av urvalskriterier

>[!IMPORTANT]
>
>Alla befintliga segmentdefinitioner som för närvarande utvärderas med hjälp av direktuppspelning eller kantsegmentering fortsätter att fungera som de är, såvida de inte redigeras eller uppdateras.

Från och med 20 maj 2025 kommer tre uppdateringar att göras som påverkar möjligheten att segmentera.

1. Berättigad regeluppsättning
2. Rätt till tidsfönster
3. Inkludera batchdata i strömmande målgrupper
4. Aktiva kopplingsprofiler

## Linjeset {#ruleset}

Alla **nya eller redigerade**-segmentdefinitioner som matchar följande regeluppsättningar utvärderas **inte längre** med hjälp av direktuppspelning eller kantsegmentering. I stället utvärderas de med gruppsegmentering.

- En enstaka händelse med ett tidsfönster längre än 24 timmar
   - Aktivera en målgrupp med alla profiler som har visat en webbsida de senaste tre dagarna.
- En enda händelse utan tidsfönster
   - Aktivera en målgrupp med alla profiler som visade en webbsida.

## Tidsfönster {#time-window}

För att kunna utvärdera en målgrupp med direktuppspelningssegmentering måste **måste** begränsas inom ett 24-timmarsfönster.

## Inkludera batchdata i strömmande målgrupper {#include-batch-data}

Före den här uppdateringen kan du skapa en definition för direktuppspelad målgrupp som kombinerar både batchdatakällor och strömmande datakällor. I och med den senaste uppdateringen utvärderas dock möjligheten att skapa en målgrupp med både batch- och direktuppspelningsdatakällor med hjälp av gruppsegmentering.

Om du behöver utvärdera en segmentdefinition med hjälp av direktuppspelning eller kantsegmentering som matchar den uppdaterade regeluppsättningen, måste du explicit skapa en grupp- och direktuppspelningsregeluppsättning och kombinera dem med segment. Den här gruppregeluppsättningen **måste** baseras på ett profilschema.

Låt oss till exempel säga att du har två målgrupper, med en målgrupps schemadata och andra schemadata för boendeupplevelser:

| Målgrupp | Schema | Source type | Frågedefinition | Målgrupps-ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Kalifornien | Profil | Grupp | Hemadressen är i delstaten Kalifornien | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Senaste utcheckningar | Experience Event | Direktuppspelning | Har minst en utcheckning de senaste 24 timmarna | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Om du vill använda gruppkomponenten i din direktuppspelande målgrupp måste du skapa en referens till gruppmålgruppen med hjälp av segment.

En exempelregeluppsättning som skulle kombinera de två målgrupperna skulle se ut så här:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

Den resulterande målgruppen *kommer* att utvärderas med direktuppspelningssegmentering, eftersom den utnyttjar gruppmålgruppens medlemskap genom att referera till gruppmålskomponenten.

Om du vill kombinera två målgrupper med händelsedata kan du **inte** bara kombinera de två händelserna. Du måste skapa båda målgrupperna och sedan skapa en annan målgrupp som använder `inSegment` för att referera till båda dessa målgrupper.

Låt oss till exempel säga att ni har två målgrupper, med båda målgrupperna som har händelseschemadata för upplevelsehändelser:

| Målgrupp | Schema | Source type | Frågedefinition | Målgrupps-ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Senaste avhopp | Experience event | Grupp | Har minst en händelse om att användaren överger den under de senaste 24 timmarna | `7deb246a-49b4-4687-95f9-6316df049948` |
| Senaste utcheckningar | Experience Event | Direktuppspelning | Har minst en utcheckning de senaste 24 timmarna | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

I den här situationen skulle du behöva skapa en tredje målgrupp enligt följande:

```
inSegment("7deb246a-49b4-4687-95f9-6316df049948") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Alla befintliga segmentdefinitioner som matchar linjalerna utvärderas fortfarande med hjälp av direktuppspelning eller kantsegmentering tills de redigeras.
>
>Dessutom kommer alla befintliga segmentdefinitioner som för närvarande uppfyller de andra kriterierna för utvärdering av direktuppspelning eller kantsegmentering att utvärderas även fortsättningsvis med hjälp av direktuppspelning eller kantsegmentering.

## Kopplingsprincip {#merge-policy}

Alla **nya eller redigerade**-segmentdefinitioner som kvalificerar för direktuppspelning eller kantsegmentering **måste** finnas i sammanfogningsprincipen Aktiv på Edge.

Om det inte finns någon aktiv sammanfogningsprincip måste du [konfigurera din sammanfogningsprincip](../profile/merge-policies/ui-guide.md#configure) och ange att den ska vara aktiv vid sidan.
