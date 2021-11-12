---
title: XDM Business Account Person Relationsklass
description: Det här dokumentet innehåller en översikt över klassen XDM Business Account Person Relation i Experience Data Model (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 2%

---

# [!UICONTROL XDM Business Account Person Relation] class

[!UICONTROL XDM Business Account Person Relation] är en XDM-klass (Standard Experience Data Model) som fångar upp de minsta nödvändiga egenskaperna för en person som är kopplad till ett företagskonto.

![](../../images/classes/b2b/business-account-person-relation.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kontot i relationen konto-person. |
| `accountPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för relationsenheten konto-person. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om relationen konto-person kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för personen i relationen konto-person. |
| `_id` | Sträng | En unik identifierare för posten. Det här är ett systemgenererat värde som är skilt från de andra ID-fälten som fångats av klassen. |
| `accountID` | Sträng | En unik identifierare för kontot i relationen konto-person. |
| `accountPersonID` | Sträng | En unik identifierare för relationsenheten konto-person. |
| `currencyCode` | Sträng | ISO 4217-valutakoden som används för relationen mellan kontot och personen. |
| `isActive` | Boolean | Anger om relationen mellan kontot och personen är aktiv. |
| `isDirect` | Boolean | Anger om detta är en direkt relation mellan kontot och personen. |
| `isPrimary` | Boolean | Anger om personen är den primära kontakten för det här kontot. |
| `personID` | Sträng | En unik identifierare för personen i relationen konto-person. |
| `personRole` | Sträng | Personens roll i relationen konto-person. |
| `relationEndDate` | DateTime | Datumet då relationen mellan kontot och personen avslutades. |
| `relationStartDate` | DateTime | Det datum då relationen mellan kontot och personen startades. |

{style=&quot;table-layout:auto&quot;}

Se guiden [schemarelationer i realtid CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
