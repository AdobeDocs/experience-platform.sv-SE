---
title: Returdatatyp
description: Läs mer om datatypen XDM (Return Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 1%

---

# [!UICONTROL Return] datatyp

[!UICONTROL Return] är en XDM-datatyp (Standard Experience Data Model) som samlar in viktig information som rör en Return Merchandise Authorization (RMA).

![Ett diagram över datatypen Return.](../images/data-types/return.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Return ID] | `returnID` | string | Unik identifierare för denna RMA. |
| [!UICONTROL Return Status] | `returnStatus` | string | Aktuell status för RMA (till exempel Väntande eller Stängt). |
| [!UICONTROL Order Purchase ID] | `purchaseID` | string | Den unika identifieraren för den order/det inköp som RMA:n gäller. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

