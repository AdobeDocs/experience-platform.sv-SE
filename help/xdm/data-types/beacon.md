---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;beacon;interaktionsinformation;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Beacon-datatyp
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL Beacon] datatyp

[!UICONTROL Beacon] är en standard-XDM-datatyp som beskriver den trådlösa enheten som kommunicerar identitetsinformation till mobilprogram när mobila enheter finns inom räckhåll.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `beaconMajor` | Dubbel | Huvudvärden identifierar och särskiljer en grupp och heltalsvärden utan tecken mellan 1 och 65 535. |
| `beaconMinor` | Dubbel | Mindre värden identifierar och särskiljer enskilda och osignerade heltalsvärden mellan 1 och 65 535. |
| `proximity` | Sträng | Beräknat avstånd från beacon. Se [bilagan](#proximity) för godkända värden och definitioner. |
| `proximityUUID` | Sträng | En UUID för närhet (Universally Unique Identifier) är en speciell typ av identifierare som används för att skilja beacons i nätverket från alla andra beacons i nätverk utanför din kontroll. UUID för närhet konfigureras till en fyr som ska överföras till mobila enheter inom räckhåll för att identifiera en organisations fyrar. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Bilaga

Följande avsnitt innehåller ytterligare information om datatypen [!UICONTROL Beacon].

## Godkända värden för närhet {#proximity}

I följande tabell visas godkända värden för `proximity` och deras associerade betydelse:

| Värde | Beskrivning |
| --- | --- |
| `immediate` | Inom några centimeter. |
| `near` | Mindre än 10 meter bort. |
| `far` | Mer än 10 meter bort. |
| `unknown` | Avståndet kunde inte fastställas, troligen på grund av en svag signal. |
