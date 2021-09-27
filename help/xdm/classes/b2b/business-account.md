---
title: XDM Business Account-klass
description: Det här dokumentet innehåller en översikt över XDM Business Account-klassen i Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 2%

---

# [!UICONTROL XDM Business Account] class

>[!NOTE]
>
>Den här klassen är bara tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

[!UICONTROL XDM Business Account] är en XDM-klass (Experience Data Model) som hämtar de minsta nödvändiga egenskaperna för ett företagskonto.

![](../../images/classes/b2b/business-account.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kontoentiteten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kontot kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `accountID`. |
| `accountID` | Sträng | En unik identifierare för kontoentiteten. |
