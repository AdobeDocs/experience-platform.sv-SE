---
title: XDM Business Opportunity Class
description: Det här dokumentet innehåller en översikt över klassen XDM Business Opportunity i Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# [!UICONTROL XDM Business Opportunity] class

[!UICONTROL XDM Business Opportunity] är en XDM-klass (Experience Data Model) som fångar upp de minsta nödvändiga egenskaperna för en affärsmöjlighet.

![](../../images/classes/b2b/business-opportunity.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för det konto som affärsmöjligheten är kopplad till. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om affärsmöjligheten kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för affärsmöjlighetsenheten. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `opportunityID`. |
| `accountID` | Sträng | Ett unikt ID för kontot som affärsmöjligheten är kopplad till. |
| `opportunityDescription` | Sträng | En beskrivning av affärsmöjligheten. |
| `opportunityID` | Sträng | Ett unikt ID för affärsmöjlighetsenheten. |
| `opportunityName` | Sträng | Namnet på affärsmöjligheten. |
| `opportunityStage` | Sträng | Affärsmöjlighetens försäljningsstadium. |
| `opportunityType` | Sträng | Typ av affärsmöjlighet. |

{style=&quot;table-layout:auto&quot;}

Se guiden [schemarelationer i realtid CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
