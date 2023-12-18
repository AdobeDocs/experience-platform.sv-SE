---
title: Datatyp för handelsomfång
description: Läs mer om datatypen XDM (Commerce Scope Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!UICONTROL Commerce Scope] datatyp

[!UICONTROL Commerce Scope] är en XDM-datatyp (Standard Experience Data Model) som definierar identifierare för var en händelse inträffade i ett e-handelssystem. Det skiljer ut miljöer, webbplatser, butiker och butiksvyer.

![Ett diagram över datatypen Commerce Scope.](../images/data-types/commerce-scope.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Environment ID] | `environmentID` | string | Händelse-ID. Ett 32-siffrigt alfanumeriskt ID. |
| [!UICONTROL Website Code] | `websiteCode` | string | Den unika webbplatskoden i en miljö. |
| [!UICONTROL Store Code] | `storeCode` | string | Den unika butikskoden på en webbplats. |
| [!UICONTROL Store View Code] | `storeViewCode` | string | Den unika butiksvykoden i en butik. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
