---
title: XDM Business Campaign-klass
description: Det här dokumentet innehåller en översikt över klassen XDM Business Campaign i Experience Data Model (XDM).
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign] klass (Beta)

>[!IMPORTANT]
>
>Den här klassen finns som en del av Real-time Customer Data Platform B2B Edition, som för närvarande är en betaversion. Dokumentationen och funktionerna kan komma att ändras.

[!UICONTROL XDM Business Campaign] är en XDM-standardklass (Experience Data Model) som fångar upp de minsta nödvändiga egenskaperna för en företagskampanj.

![](../../images/classes/b2b/business-campaign.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kampanjentiteten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kampanjen kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `campaignID`. |
| `campaignDescription` | Sträng | En beskrivning av kampanjen. |
| `campaignID` | Sträng | En unik identifierare för kampanjentiteten. |
| `campaignName` | Sträng | Namnet på kampanjen. |
| `campaignType` | Sträng | Kampanjtypen eller målgruppen. |

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
