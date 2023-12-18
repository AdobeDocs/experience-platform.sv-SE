---
title: XDM Business Campaign-klass
description: Läs mer om klassen XDM Business Campaign i Experience Data Model (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# [!UICONTROL XDM Business Campaign] class

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till Real-Time CDP B2B Edition för att den här klassen ska kunna delta i [Kundprofil i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] är en XDM-standardklass (Experience Data Model) som fångar upp de minsta nödvändiga egenskaperna för en företagskampanj.

![Strukturen för XDM Business Campaign-klassen så som den visas i användargränssnittet](../../images/classes/b2b/business-campaign.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kampanjentiteten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kampanjen kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `campaignID`. |
| `campaignDescription` | Sträng | En beskrivning av kampanjen. |
| `campaignID` | Sträng | En unik identifierare för kampanjentiteten. |
| `campaignName` | Sträng | Namnet på kampanjen. |
| `campaignType` | Sträng | Kampanjtypen eller målgruppen. |

{style="table-layout:auto"}

Om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet läser du i handboken [schemarelationer i Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Ytterligare fält som är kompatibla med den här klassen finns i fältgruppsreferensen för [[!UICONTROL XDM Business Campaign Details]](../../field-groups/b2b-campaign/details.md).
