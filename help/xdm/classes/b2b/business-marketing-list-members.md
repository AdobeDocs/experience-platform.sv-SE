---
title: Klassen XDM Business Marketing List-medlemmar
description: Det här dokumentet innehåller en översikt över XDM Business Marketing List-medlemsklassen i Experience Data Model (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---

# [!UICONTROL XDM Business Marketing List Members] class

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till Real-Time CDP B2B Edition för att den här klassen ska kunna delta i [Kundprofil i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List Members] är en XDM-klass (Experience Data Model) som beskriver medlemmar, personer eller kontakter som är kopplade till en marknadsföringslista.

![Strukturen för XDM Business Marketing List-medlemsklassen som den visas i användargränssnittet](../../images/classes/b2b/business-marketing-list-members.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om medlemskapet för marknadsföringslistan kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den marknadsföringslista som personen är medlem i. |
| `marketingListMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för medlemsenheten för marknadsföringslistan. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den person som är medlem i marknadsföringslistan. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `marketingListMemberID`. |
| `isDeleted` | Boolean | Anger om den här medlemsentiteten för marknadsföringslistan har tagits bort i Marketo Engage.<br><br>När du använder [Marketo källanslutning](../../../sources/connectors/adobe-applications/marketo/marketo.md), återspeglas alla poster som tas bort i Marketo automatiskt i kundprofilen i realtid. Poster som rör dessa profiler kan dock fortfarande finnas kvar i datasjön. Efter inställning `isDeleted` till `true`kan du använda fältet för att filtrera bort vilka poster som har tagits bort från dina källor när du frågar efter datasjön. |
| `marketingListID` | Sträng | Ett unikt ID för marknadsföringslistan. |
| `marketingListMemberID` | Sträng | Ett unikt ID för medlemsenheten för marknadsföringslistan. |
| `personId` | Sträng | Ett unikt ID för personen. |

{style="table-layout:auto"}

Se guiden [schemarelationer i Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
