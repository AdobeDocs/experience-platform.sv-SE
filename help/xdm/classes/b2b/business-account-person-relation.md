---
title: XDM Business Account Person Relationsklass
description: Det här dokumentet innehåller en översikt över klassen XDM Business Account Person Relation i Experience Data Model (XDM).
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# [!UICONTROL XDM Business Account Person Relation] klass (Beta)

>[!IMPORTANT]
>
>Den här klassen finns som en del av Real-time Customer Data Platform B2B Edition, som för närvarande är en betaversion. Dokumentationen och funktionerna kan komma att ändras.

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

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
