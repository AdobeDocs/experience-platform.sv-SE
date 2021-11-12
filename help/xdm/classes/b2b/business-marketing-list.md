---
title: XDM Business Marketing List-klass
description: Det här dokumentet innehåller en översikt över klassen XDM Business Marketing List i Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List] class

[!UICONTROL XDM Business Marketing List] är en XDM-klass (Standard Experience Data Model) som fångar upp de minsta nödvändiga egenskaperna för en marknadsföringslista. Med marknadsföringslistor kan ni prioritera kunder som är mest benägna att köpa er produkt.

![](../../images/classes/b2b/business-marketing-list.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om marknadsföringslistan kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för marknadsföringslistentiteten. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `marketingListID`. |
| `marketingListDescription` | Sträng | En beskrivning av marknadsföringslistan. |
| `marketingListID` | Sträng | Ett unikt ID för marknadsföringslistentiteten. |
| `marketingListName` | Sträng | Marknadsföringslistans namn. |

{style=&quot;table-layout:auto&quot;}

Se guiden [schemarelationer i realtid CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
