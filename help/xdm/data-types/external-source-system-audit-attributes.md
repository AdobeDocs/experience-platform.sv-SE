---
title: Datatypen för externa källsystemsgranskningsattribut
description: Det här dokumentet innehåller en översikt över datatypen XDM (External Source System Audit Attributes Experience Data Model).
source-git-commit: 8bf0c63f33ae9cbfb01d4db9e5220c6762575c5b
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 1%

---

# [!UICONTROL External Source System Audit Attributes] datatyp

>[!NOTE]
>
>Den här datatypen är endast tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

[!UICONTROL External Source System Audit Attributes] är en XDM-datatyp (Standard Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

![](../images/data-types/external-source-system-audit-attributes.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL B2B Source]](./b2b-source.md) | En sammansatt identifierare för källan som används för granskning. |
| `createdBy` | Sträng | Namnet på den användare som skapade den här posten. |
| `createdDate` | DateTime | Datumet då posten skapades. |
| `externalID` | Sträng | Extern unik identifierare för källan. Det här värdet används för att identifiera och deduplicera vid behov. |
| `lastActivityDate` | DateTime | Det senaste aktivitetsdatumet för källsystemet. |
| `lastReferencedDate` | DateTime | Det senaste referensdatumet för källsystemet. |
| `lastUpdatedBy` | Sträng | Namnet på den person som senast uppdaterade den här posten. |
| `lastUpdatedDate` | DateTime | Det senaste uppdateringsdatumet för källsystemet. |
| `lastViewedDate` | DateTime | Det senast visade datumet för källsystemet. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
