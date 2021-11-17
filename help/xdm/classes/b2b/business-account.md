---
title: XDM Business Account-klass
description: Det här dokumentet innehåller en översikt över XDM Business Account-klassen i Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 1%

---

# [!UICONTROL XDM Business Account] class

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till CDP B2B Edition i realtid för att den här klassen ska kunna delta i [Kundprofil i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Account] är en XDM-klass (Experience Data Model) som hämtar de minsta nödvändiga egenskaperna för ett företagskonto.

![](../../images/classes/b2b/business-account.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kontoentiteten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kontot kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `accountID`. |
| `accountID` | Sträng | En unik identifierare för kontoentiteten. |

{style=&quot;table-layout:auto&quot;}

Se guiden [schemarelationer i realtid CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
