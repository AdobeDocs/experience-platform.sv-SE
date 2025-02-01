---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;schemas;scheman;webbläsare;webbläsarinformation;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Datatypen Webbläsarinformation
description: Läs mer om datatypen XDM i webbläsarinformationen.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Datatypen [!UICONTROL Browser details]

[!UICONTROL Browser details] är en standard-XDM-datatyp som beskriver information som relaterar till en webbläsare eller ett program.

![](../images/data-types/browser-details.png){width=450}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `acceptLanguage` | Sträng | En IETF-språktagg ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Boolean | Anger om användarens inställningar tillåter att cookies skrivs. |
| `javaEnabled` | Boolean | Anger om Java var aktiverat i enheten som observationen gjordes från. |
| `javaScriptEnabled` | Boolean | Anger om JavaScript var aktiverat i den enhet som observationen gjordes från. |
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

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
