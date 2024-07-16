---
title: XDM Business Opportunity Class
description: Läs mer om XDM-klassen för affärsmöjligheter i Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# klassen [!UICONTROL XDM Business Opportunity]

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till Real-Time CDP B2B Edition för att den här klassen ska kunna delta i [kundprofilen i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity] är en XDM-standardklass (Experience Data Model) som hämtar de minsta nödvändiga egenskaperna för en affärsmöjlighet.

![Strukturen för XDM-klassen för affärsmöjligheter så som den visas i användargränssnittet](../../images/classes/b2b/business-opportunity.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för det konto som affärsmöjligheten är kopplad till. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om affärsmöjligheten kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för affärsmöjlighetsenheten. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `opportunityID`. |
| `accountID` | Sträng | Ett unikt ID för kontot som affärsmöjligheten är kopplad till. |
| `isDeleted` | Boolean | Anger om den här marknadsföringslistentiteten har tagits bort i Marketo Engage.<br><br>När du använder [Marketo-källkopplingen](../../../sources/connectors/adobe-applications/marketo/marketo.md) återspeglas alla poster som tas bort i Marketo automatiskt i kundprofilen i realtid. Poster som rör dessa profiler kan dock fortfarande finnas kvar i datasjön. Genom att ställa in `isDeleted` på `true` kan du använda fältet för att filtrera bort vilka poster som har tagits bort från dina källor när du frågar i datasjön. |
| `opportunityDescription` | Sträng | En beskrivning av affärsmöjligheten. |
| `opportunityID` | Sträng | Ett unikt ID för affärsmöjlighetsenheten. |
| `opportunityName` | Sträng | Namnet på affärsmöjligheten. |
| `opportunityStage` | Sträng | Affärsmöjlighetens försäljningsstadium. |
| `opportunityType` | Sträng | Typ av affärsmöjlighet. |

{style="table-layout:auto"}

Läs guiden om [schemarelationer i Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
