---
title: XDM Business Campaign-klass
description: Det här dokumentet innehåller en översikt över klassen XDM Business Campaign i Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 4%

---

# [!UICONTROL XDM Business Campaign] class

>[!NOTE]
>
>Den här klassen är bara tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

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
