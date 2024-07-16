---
title: Returdatatyp
description: Läs mer om datatypen XDM (Return Experience Data Model).
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 1%

---

# Datatypen [!UICONTROL Return]

[!UICONTROL Return] är en XDM-datatyp (Standard Experience Data Model) som samlar in viktig information som rör en RMA (Return Merchandise Authorization).

![Ett diagram över returdatatypen.](../images/data-types/return.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Return ID] | `returnID` | string | Unik identifierare för denna RMA. |
| [!UICONTROL Return Status] | `returnStatus` | string | Aktuell status för RMA (till exempel Väntande eller Stängt). |
| [!UICONTROL Order Purchase ID] | `purchaseID` | string | Den unika identifieraren för den order/det inköp som RMA:n gäller. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)
