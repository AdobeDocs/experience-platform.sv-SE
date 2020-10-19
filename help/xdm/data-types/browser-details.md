---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;browser;browser details;datatype;data-type;data type;
solution: Experience Platform
title: Datatypen Webbläsarinformation
topic: overview
description: Dokumentet innehåller en översikt över XDM-datatypen Browser Details.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---


# [!UICONTROL Browser details] datatyp

[!UICONTROL Browser details] är en standard-XDM-datatyp som beskriver information som rör en webbläsare eller ett program.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `acceptLanguage` | Sträng | En IETF-språktagg ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Boolean | Anger om användarens inställningar tillåter att cookies skrivs. |
| `javaEnabled` | Boolean | Anger om Java var aktiverat i enheten som observationen gjordes från. |
| `javaScriptEnabled` | Boolean | Anger om JavaScript var aktiverat på enheten som observationen gjordes från. |
| `javaScriptVersion` | Sträng | Den version av JavaScript som stöds under observationen. |
| `javaVersion` | Sträng | Den version av Java som stöds under observationen. |
| `name` | Sträng | Program- eller webbläsarnamnet. |
| `quicktimeVersion` | Sträng | Den version av Apple QuickTime som stöds under observationen. |
| `thirdPartyCookiesEnabled` | Boolean | Anger om cookies från tredje part aktiverades i enheten som observationen gjordes från. |
| `userAgent` | Sträng | HTTP-användaragentsträngen från klientbegäran. |
| `vendor` | Sträng | Programmet eller webbläsarleverantören. |
| `version` | Sträng | Program- eller webbläsarversionen. |
| `viewportHeight` | Heltal | Den lodräta storleken i pixlar i fönstret som händelsen visades inuti. För en webbvyhändelse är detta höjden på webbläsarens visningsruta. |
| `viewportWidth` | Heltal | Den vågräta storleken i pixlar på fönstret där händelsen visades. För en webbvyhändelse är detta bredden på webbläsarens visningsruta. |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)