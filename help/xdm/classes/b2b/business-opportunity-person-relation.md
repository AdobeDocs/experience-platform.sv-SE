---
title: XDM - personrelationsklass för affärsmöjlighet
description: Det här dokumentet innehåller en översikt över klassen XDM Business Opportunity Person Relation i Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 2%

---

# [!UICONTROL XDM Business Opportunity Person Relation] class

[!UICONTROL XDM Business Opportunity Person Relation] är en XDM-klass (Standard Experience Data Model) som fångar upp de minsta nödvändiga egenskaperna för en person som är kopplad till en affärsmöjlighet.

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om affärspersonsrelationen kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för affärsmöjligheten i affärsmöjlighetsrelationen. |
| `opportunityPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för relationen affärsmöjlighet-person. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för personen i affärsmöjlighetsrelationen. |
| `_id` | Sträng | En unik identifierare för posten. Det här är ett systemgenererat värde som är skilt från de andra ID-fälten som fångats av klassen. |
| `opportunityID` | Sträng | En unik identifierare för affärsmöjligheten i affärsmöjlighetsrelationen. |
| `opportunityPersonID` | Sträng | En unik identifierare för relationen affärsmöjlighet-person |
| `isPrimary` | Boolean | Anger om personen är den primära kontakten för affärsmöjligheten. |
| `personID` | Sträng | En unik identifierare för personen i affärsmöjlighetsrelationen. |
| `personRole` | Sträng | Personens roll i relationen affärsmöjlighet-person. |

{style=&quot;table-layout:auto&quot;}

Se guiden [schemarelationer i realtid CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
