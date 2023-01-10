---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;schemas;scheman;webbläsare;webbläsarinformation;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Datatypen Webbläsarinformation
description: Dokumentet innehåller en översikt över XDM-datatypen Browser Details.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

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
| `quicktimeVersion` | Sträng | Den version av Apple Quicktime som stöds under observationen. |
| `thirdPartyCookiesEnabled` | Boolean | Anger om cookies från tredje part aktiverades i enheten som observationen gjordes från. |
| `userAgent` | Sträng | HTTP-användaragentsträngen från klientbegäran. |
| `vendor` | Sträng | Programmet eller webbläsarleverantören. |
| `version` | Sträng | Program- eller webbläsarversionen. |
| `viewportHeight` | Heltal | Den lodräta storleken i pixlar i fönstret som händelsen visades inuti. För en webbvyhändelse är detta höjden på webbläsarens visningsruta. |
| `viewportWidth` | Heltal | Den vågräta storleken i pixlar på fönstret där händelsen visades. För en webbvyhändelse är detta bredden på webbläsarens visningsruta. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
