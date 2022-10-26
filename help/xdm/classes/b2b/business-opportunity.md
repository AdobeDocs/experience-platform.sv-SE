---
title: XDM Business Opportunity Class
description: Det här dokumentet innehåller en översikt över klassen XDM Business Opportunity i Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 2%

---

# [!UICONTROL XDM Business Opportunity] class

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till Real-Time CDP B2B Edition för att den här klassen ska kunna delta i [Kundprofil i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity] är en XDM-klass (Experience Data Model) som fångar upp de minsta nödvändiga egenskaperna för en affärsmöjlighet.

![Strukturen för XDM-klassen för affärsmöjligheter så som den visas i användargränssnittet](../../images/classes/b2b/business-opportunity.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för det konto som affärsmöjligheten är kopplad till. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om affärsmöjligheten kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för affärsmöjlighetsenheten. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `opportunityID`. |
| `accountID` | Sträng | Ett unikt ID för kontot som affärsmöjligheten är kopplad till. |
| `isDeleted` | Boolean | Anger om den här marknadsföringslistentiteten har tagits bort i Marketo Engage.<br><br>När du använder [Marketo källanslutning](../../../sources/connectors/adobe-applications/marketo/marketo.md), återspeglas alla poster som tas bort i Marketo automatiskt i kundprofilen i realtid. Poster som rör dessa profiler kan dock fortfarande finnas kvar i datasjön. Efter inställning `isDeleted` till `true`kan du använda fältet för att filtrera bort vilka poster som har tagits bort från dina källor när du frågar efter datasjön. |
| `opportunityDescription` | Sträng | En beskrivning av affärsmöjligheten. |
| `opportunityID` | Sträng | Ett unikt ID för affärsmöjlighetsenheten. |
| `opportunityName` | Sträng | Namnet på affärsmöjligheten. |
| `opportunityStage` | Sträng | Affärsmöjlighetens försäljningsstadium. |
| `opportunityType` | Sträng | Typ av affärsmöjlighet. |

{style=&quot;table-layout:auto&quot;}

Se guiden [schemarelationer i Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
