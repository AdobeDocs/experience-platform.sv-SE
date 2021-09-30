---
title: Klassen XDM Business Marketing List-medlemmar
description: Det här dokumentet innehåller en översikt över XDM Business Marketing List-medlemsklassen i Experience Data Model (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List Members] class

>[!NOTE]
>
>Den här klassen är endast tillgänglig för organisationer som har åtkomst till kunddataplattformen B2B Edition i realtid.

[!UICONTROL XDM Business Marketing List Members] är en XDM-klass (Experience Data Model) som beskriver medlemmar, personer eller kontakter som är kopplade till en marknadsföringslista.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om medlemskapet för marknadsföringslistan kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den marknadsföringslista som personen är medlem i. |
| `marketingListMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för medlemsenheten för marknadsföringslistan. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den person som är medlem i marknadsföringslistan. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `marketingListMemberID`. |
| `marketingListID` | Sträng | Ett unikt ID för marknadsföringslistan. |
| `marketingListMemberID` | Sträng | Ett unikt ID för medlemsenheten för marknadsföringslistan. |
| `personId` | Sträng | Ett unikt ID för personen. |

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
