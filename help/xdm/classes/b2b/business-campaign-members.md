---
title: Klassen XDM Business Campaign-medlemmar
description: Det här dokumentet innehåller en översikt över XDM Business Campaign-medlemsklassen i Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign Members] class

>[!NOTE]
>
>Den här klassen är endast tillgänglig för organisationer som har åtkomst till kunddataplattformen B2B Edition i realtid.

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

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
