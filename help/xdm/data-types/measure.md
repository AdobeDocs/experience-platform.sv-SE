---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;mått;datatyp;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Mätdatatyp
description: Läs mer om datatypen Mät Experience Data Model (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Datatypen [!UICONTROL Measure]

[!UICONTROL Measure] är en XDM-datatyp (Standard Experience Data Model) som innehåller en konkret kvantifierbar datapunkt för ett visst mått. Ett mått består av en unik identifierare och ett värde.

![mät bild](../images/data-types/measure.PNG){width=500}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `id` | Sträng | Den unika identifieraren för den här åtgärden. Vid datainsamling med förstörande kommunikationskanaler, t.ex. mobilappar eller webbplatser med offlinefunktion där det inte går att säkerställa överföring av åtgärder, innehåller denna egenskap ett klientgenererat, unikt ID för den vidtagna åtgärden. Det är god praxis att göra detta tillräckligt långt för att säkerställa tillräcklig slumpmässighet. <br><br> Om information som tidsstämpel, enhets-ID, IP-adress, MAC-adress eller andra potentiellt användaridentifieringsvärden ingår i genereringen av `id` bör resultatet hash-kodas. Detta garanterar att ingen PII-kod kodas i värdet, eftersom målet inte är att identifiera en användare eller enhet, utan det specifika tidsmåttet. |
| `value` | Dubbel | Det kvantifierbara värdet av denna åtgärd. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
