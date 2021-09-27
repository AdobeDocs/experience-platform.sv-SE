---
title: Klassen XDM Business Marketing List-medlemmar
description: Det här dokumentet innehåller en översikt över XDM Business Marketing List-medlemsklassen i Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 3%

---

# [!UICONTROL XDM Business Marketing List Members] class

>[!NOTE]
>
>Den här klassen är bara tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

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
