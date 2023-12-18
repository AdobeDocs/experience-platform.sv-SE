---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;device;data type;data type;
solution: Experience Platform
title: Marknadsföringsdatatyp
description: Läs mer om datatypen Marketing XDM.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!UICONTROL Marketing] datatyp

[!UICONTROL Marketing] är en standard-XDM-datatyp som beskriver marknadsföringsaktiviteter som är aktiva med en viss kontaktyta.

![](../images/data-types/marketing.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `campaignGroup` | Sträng | Namnet på kampanjgruppen (om flera kampanjer grupperas tillsammans, som `50%_DISCOUNT`). |
| `campaignName` | Sträng | Namnet på marknadsföringskampanjen, till exempel `50%_DISCOUNT_USA` eller `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Sträng | Den spårningskod som kan användas för att identifiera marknadsföringskampanjen som händelsen är kopplad till. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
