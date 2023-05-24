---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;schemas;scheman;enhet;datatyp;datatyp;datatyp;valuta;
solution: Experience Platform
title: Datatyp för valuta
description: Det här dokumentet innehåller en översikt över datatypen Currency XDM.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---

# [!UICONTROL Currency] datatyp

[!UICONTROL Currency] är en standard-XDM-datatyp som beskriver ett valutabelopp, inklusive valutatyp och konverteringsdatum.

![](../images/data-types/currency.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `amount` | Dubbel | Valutabeloppet som definieras av `currencyCode`. |
| `conversionDate` | DateTime | En tidsstämpel som anger när valutakonverteringen gjordes. |
| `currencyCode` | Sträng | En ISO 4217-kod som anger vilken typ av valuta som `amount` representerar. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
