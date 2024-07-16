---
title: Datatyp för rekvisitionslista
description: Läs mer om datatypen XDM (Requisition List Experience Data Model).
exl-id: cbea6b08-9d4d-4cbe-b0c5-506bccc6df67
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Datatypen [!UICONTROL Requisition List]

[!UICONTROL Requisition List] är en XDM-datatyp (Standard Experience Data Model) som beskriver en förvaltad samling med objekt för inköp eller upphandling. Använd datatypen [!UICONTROL Requisition List] för att identifiera och beskriva rekvisitionslistor.

![Ett diagram över datatypen [!UICONTROL Requisition List].](../images/data-types/requisition-list.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL Requisition List ID] | `ID` | string | Den unika identifieraren för rekvisitionslistan. |
| [!UICONTROL Requisition List Name] | `name` | string | Namnet på den rekvisitionslista som har angetts av kunden. |
| [!UICONTROL Requisition List Description] | `description` | string | En beskrivning av rekvisitionslistan som anges av kunden. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
