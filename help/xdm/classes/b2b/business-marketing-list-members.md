---
title: Klassen XDM Business Marketing List-medlemmar
description: Det här dokumentet innehåller en översikt över XDM Business Marketing List-medlemsklassen i Experience Data Model (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List Members] klass (Beta)

>[!IMPORTANT]
>
>Den här klassen finns som en del av Real-time Customer Data Platform B2B Edition, som för närvarande är en betaversion. Dokumentationen och funktionerna kan komma att ändras.

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

{style=&quot;table-layout:auto&quot;}

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
