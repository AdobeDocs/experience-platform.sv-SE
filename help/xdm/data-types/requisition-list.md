---
title: Datatyp för rekvisitionslista
description: Läs mer om datatypen XDM (Requisition List Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# [!UICONTROL Requisition List] datatyp

[!UICONTROL Requisition List] är en XDM-datatyp (Standard Experience Data Model) som beskriver en förvaltad samling av objekt för inköp eller upphandling. Använd [!UICONTROL Requisition List] datatyp för att identifiera och beskriva rekvisitionslistor.

![Ett diagram över [!UICONTROL Requisition List] datatyp.](../images/data-types/requisition-list.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL Requisition List ID] | `ID` | string | Den unika identifieraren för rekvisitionslistan. |
| [!UICONTROL Requisition List Name] | `name` | string | Namnet på den rekvisitionslista som har angetts av kunden. |
| [!UICONTROL Requisition List Description] | `description` | string | En beskrivning av rekvisitionslistan som anges av kunden. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
