---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;sökning;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Sökdatatyp
description: Det här dokumentet innehåller en översikt över datatypen XDM (Search Experience Data Model).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '182'
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
| `slot` | Sträng | Det namngivna avsnittet på sidan där sökresultatet visades. Värdet för den här egenskapen måste vara lika med ett av de kända enum-värden som du definierar, till exempel `top`, `side`, eller `bottom`. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
