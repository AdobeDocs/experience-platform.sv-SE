---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;mått;datatyp;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Mätdatatyp
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen Mät Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# [!UICONTROL Measure] datatyp

[!UICONTROL Measure] är en XDM-datatyp (Standard Experience Data Model) som innehåller en kvantifierbar datapunkt för ett visst mätvärde. Ett mått består av en unik identifierare och ett värde.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `id` | Sträng | Den unika identifieraren för den här åtgärden. Vid datainsamling med förstörande kommunikationskanaler, t.ex. mobilappar eller webbplatser med offlinefunktion där det inte går att säkerställa överföring av åtgärder, innehåller denna egenskap ett klientgenererat, unikt ID för den vidtagna åtgärden. Det är god praxis att göra detta tillräckligt långt för att säkerställa tillräcklig slumpmässighet. <br><br> Om information som tidsstämpel, enhets-ID, IP, MAC-adress eller andra potentiellt användaridentifierande värden ingår i genereringen av  `id`ska resultatet hashas. Detta garanterar att ingen PII-kod kodas i värdet, eftersom målet inte är att identifiera en användare eller enhet, utan det specifika tidsmåttet. |
| `value` | Dubbel | Det kvantifierbara värdet av denna åtgärd. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)