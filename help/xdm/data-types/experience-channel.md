---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;Webbsidesinformation;datatyp;datatyp;webbsida
solution: Experience Platform
title: Typ av Experience Channel-data
description: Det här dokumentet innehåller en översikt över datatypen Experience channel Experience Data Model (XDM).
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# [!UICONTROL Experience channel] datatyp

[!UICONTROL Experience channel] är en XDM-datatyp (Standard Experience Data Model) som beskriver en upplevelsekanal. En upplevelsekanal representerar en metod eller väg för hur digitala upplevelser konsumeras.

Det finns flera olika upplevelsekanaler, var och en med olika begränsningar för hur innehåll levereras, hur kundinteraktion kan observeras och hur data samlas in. I en kanal kan upplevelserna levereras till specifika platser. Platserna och platstyperna som finns i en kanal skiljer sig från kanal till kanal.

![](../images/data-types/experience-channel.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_id` | Sträng | Ett ID som unikt identifierar kanalen. Varje specifik upplevelsekanal definierar en konstant `@id`. |
| `_type` | Sträng | Tillhandahåller en grov klassificeringsetikett för kanaler med liknande egenskaper. |
| `contentTypes` | Array med strängar | De innehållstyper som den här kanalen kan leverera. |
| `locationTypes` | Array med strängar | De typer av platser (virtuella platser) som den här kanalen består av och kan leverera innehåll till. |
| `mediaAction` | Sträng | Beskriver en Experience Event-medieåtgärd, om tillämpligt. |
| `mediaType` | Sträng | Anger om medietypen är betald, ägd eller förtjänad. |
| `metricTypes` | Array med strängar | De mätvärden som kan samlas in i den här kanalen. |
| `mode` | Sträng | Hur upplevelser levereras i den här kanalen. |
| `typeAtSource` | Sträng | Ett anpassat namn för kanalen. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
