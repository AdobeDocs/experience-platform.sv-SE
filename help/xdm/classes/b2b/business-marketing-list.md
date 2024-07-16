---
title: XDM Business Marketing List-klass
description: Läs mer om klassen XDM Business Marketing List i Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# klassen [!UICONTROL XDM Business Marketing List]

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till Real-Time CDP B2B Edition för att den här klassen ska kunna delta i [kundprofilen i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List] är en XDM-standardklass (Experience Data Model) som hämtar de minsta nödvändiga egenskaperna för en marknadsföringslista. Med marknadsföringslistor kan ni prioritera kunder som är mest benägna att köpa er produkt.

![Strukturen för klassen XDM Business Marketing List så som den visas i gränssnittet](../../images/classes/b2b/business-marketing-list.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om marknadsföringslistan kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för marknadsföringslistentiteten. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `marketingListID`. |
| `isDeleted` | Boolean | Anger om den här marknadsföringslistentiteten har tagits bort i Marketo Engage.<br><br>När du använder [Marketo-källkopplingen](../../../sources/connectors/adobe-applications/marketo/marketo.md) återspeglas alla poster som tas bort i Marketo automatiskt i kundprofilen i realtid. Poster som rör dessa profiler kan dock fortfarande finnas kvar i datasjön. Genom att ställa in `isDeleted` på `true` kan du använda fältet för att filtrera bort vilka poster som har tagits bort från dina källor när du frågar i datasjön. |
| `marketingListDescription` | Sträng | En beskrivning av marknadsföringslistan. |
| `marketingListID` | Sträng | Ett unikt ID för marknadsföringslistentiteten. |
| `marketingListName` | Sträng | Namnet på marknadsföringslistan. |

{style="table-layout:auto"}

Läs guiden om [schemarelationer i Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
