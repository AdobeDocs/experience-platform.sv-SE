---
title: XDM - personrelationsklass för affärsmöjlighet
description: Det här dokumentet innehåller en översikt över klassen XDM Business Opportunity Person Relation i Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 3%

---

# [!UICONTROL XDM Business Opportunity Person Relation] class

>[!NOTE]
>
>Den här klassen är bara tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

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
