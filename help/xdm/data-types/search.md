---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;sökning;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Sökdatatyp
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM (Search Experience Data Model).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---


# [!UICONTROL Search] datatyp

[!UICONTROL Search] är en XDM-datatyp (Experience Data Model) som innehåller information om webbsökningsaktivitet.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `isPaid` | Boolean | Används för att ange om sökningen är betald eller inte. |
| `keywords` | Sträng | Nyckelorden för sökningen. |
| `pageDepth` | Heltal | Siddjupet i sökresultaten. |
| `position` | Heltal | Listans position eller rangordning på sökresultatsidan. |
| `searchEngine` | Sträng | Sökmotorn som används av sökningen. |
| `searchEngineID` | Sträng | Programspecifik identifierare som används för att identifiera sökmotorn. |
| `slot` | Sträng | Det namngivna avsnittet på sidan där sökresultatet visades. Värdet för den här egenskapen måste vara lika med ett av de kända enum-värden som du definierar, till exempel `top`, `side` eller `bottom`. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)