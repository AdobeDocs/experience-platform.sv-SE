---
title: XDM Business Campaign-klass
description: Det här dokumentet innehåller en översikt över klassen XDM Business Campaign i Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign] class

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till CDP B2B Edition i realtid för att den här klassen ska kunna delta i [Kundprofil i realtid](../../../profile/home.md).

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

Se guiden [schemarelationer i realtid CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
