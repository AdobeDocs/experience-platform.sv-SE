---
title: Datatyp för annonsbrytning
description: Läs mer om datatypen XDM (Ad break Experience Data Model).
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 1%

---

# [!UICONTROL Ad break] datatyp

[!UICONTROL Ad break] är en XDM-datatyp (Standard Experience Data Model) som beskriver hur en tidsbestämd annons infogas i ett tidsbestämt medium.

![Datatypstruktur](../images/data-types/ad-break.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_dc.title` | Sträng | Ett eget namn för annonsbrytningen. |
| `_id` | Sträng | En unik identifierare för annonsbrytningen. |
| `offset` | Heltal | Förskjutningen i sekunder för annonsbrytningen från början av det primära innehållet. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
