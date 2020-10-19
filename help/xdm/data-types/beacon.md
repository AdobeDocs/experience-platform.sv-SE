---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Beacon, datatyp
topic: overview
description: Det här dokumentet innehåller en översikt över klassen XDM Individual Profile.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---


# [!UICONTROL Beacon] datatyp

[!UICONTROL Beacon] är en standard-XDM-datatyp som beskriver den trådlösa enheten som kommunicerar identitetsinformation till mobilprogram när mobila enheter finns inom räckhåll.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `beaconMajor` | Dubbel | Huvudvärden identifierar och särskiljer en grupp och heltalsvärden utan tecken mellan 1 och 65 535. |
| `beaconMinor` | Dubbel | Mindre värden identifierar och särskiljer enskilda och osignerade heltalsvärden mellan 1 och 65 535. |
| `proximity` | Sträng | Beräknat avstånd från beacon. I [bilagan](#proximity) finns godkända värden och definitioner. |
| `proximityUUID` | Sträng | En UUID för närhet (Universally Unique Identifier) är en speciell typ av identifierare som används för att skilja beacons i nätverket från alla andra beacons i nätverk utanför din kontroll. UUID för närhet konfigureras till en fyr som ska överföras till mobila enheter inom räckhåll för att identifiera en organisations fyrar. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Bilaga

Följande avsnitt innehåller ytterligare information om [!UICONTROL Beacon] datatypen.

## Godkända värden för närhet {#proximity}

I följande tabell beskrivs godkända värden för `proximity` och deras innebörd:

| Värde | Beskrivning |
| --- | --- |
| `immediate` | Inom några centimeter. |
| `near` | Mindre än 10 meter bort. |
| `far` | Mer än 10 meter bort. |
| `unknown` | Avståndet kunde inte fastställas, troligen på grund av en svag signal. |