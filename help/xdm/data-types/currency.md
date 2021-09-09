---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;schemas;scheman;enhet;datatyp;datatyp;datatyp;valuta;
solution: Experience Platform
title: Datatyp för valuta
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över datatypen Currency XDM.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!UICONTROL Currency] datatyp

[!UICONTROL Currency] är en standard-XDM-datatyp som beskriver ett valutabelopp, inklusive valutatyp och konverteringsdatum.

![](../images/data-types/currency.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `amount` | Dubbel | Valutabeloppet som definieras av `currencyCode`. |
| `conversionDate` | DateTime | En tidsstämpel som anger när valutakonverteringen gjordes. |
| `currencyCode` | Sträng | En ISO 4217-kod som anger vilken typ av valuta som `amount` representerar. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
