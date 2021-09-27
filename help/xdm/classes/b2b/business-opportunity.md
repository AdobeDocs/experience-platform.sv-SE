---
title: XDM Business Opportunity Class
description: Det här dokumentet innehåller en översikt över klassen XDM Business Opportunity i Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 5%

---

# [!UICONTROL XDM Business Opportunity] class

>[!NOTE]
>
>Den här klassen är bara tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

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
