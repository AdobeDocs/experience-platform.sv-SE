---
title: XDM Business Campaign-klass
description: Det här dokumentet innehåller en översikt över klassen XDM Business Campaign i Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '180'
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

{style=&quot;table-layout:auto&quot;}

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
