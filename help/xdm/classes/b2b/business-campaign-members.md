---
title: Klassen XDM Business Campaign-medlemmar
description: Det här dokumentet innehåller en översikt över XDM Business Campaign-medlemsklassen i Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign Members] class

[!UICONTROL XDM Business Campaign Members] är en XDM-klass (Experience Data Model) som beskriver en kontakt eller ett lead som är kopplat till en företagskampanj.

![](../../images/classes/b2b/business-campaign-members.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den associerade kampanjen. |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kampanjmedlemsenheten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kampanjmedlemskapet kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den person som är medlem i den associerade kampanjen. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `campaignMemberID`. |
| `campaignID` | Sträng | Ett unikt ID för den associerade kampanjen. |
| `campaignMemberID` | Sträng | Ett unikt ID för kampanjmedlemsenheten. |
| `personId` | Sträng | Ett unikt ID för den person som är medlem i den associerade kampanjen. |

{style=&quot;table-layout:auto&quot;}

Se guiden [schemarelationer i realtid CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
