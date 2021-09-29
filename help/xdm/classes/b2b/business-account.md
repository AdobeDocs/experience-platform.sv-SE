---
title: XDM Business Account-klass
description: Det här dokumentet innehåller en översikt över XDM Business Account-klassen i Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---

# [!UICONTROL XDM Business Account] klass (Beta)

>[!IMPORTANT]
>
>Den här klassen finns som en del av Real-time Customer Data Platform B2B Edition, som för närvarande är en betaversion. Dokumentationen och funktionerna kan komma att ändras.

[!UICONTROL XDM Business Account] är en XDM-klass (Experience Data Model) som hämtar de minsta nödvändiga egenskaperna för ett företagskonto.

![](../../images/classes/b2b/business-account.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kontoentiteten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kontot kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `accountID`. |
| `accountID` | Sträng | En unik identifierare för kontoentiteten. |

{style=&quot;table-layout:auto&quot;}

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
