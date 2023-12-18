---
title: XDM Business Account-klass
description: Läs mer om XDM Business Account-klassen i Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!UICONTROL XDM Business Account] class

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till Real-Time CDP B2B Edition för att den här klassen ska kunna delta i [Kundprofil i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Account] är en XDM-klass (Experience Data Model) som hämtar de minsta nödvändiga egenskaperna för ett företagskonto.

![Strukturen för XDM Business Account-klassen så som den visas i användargränssnittet](../../images/classes/b2b/business-account.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kontoentiteten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kontot kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `accountKey` identifierare. |
| `isDeleted` | Boolean | Anger om den här kontoentiteten har tagits bort i Marketo Engage.<br><br>När du använder [Marketo källanslutning](../../../sources/connectors/adobe-applications/marketo/marketo.md), återspeglas alla poster som tas bort i Marketo automatiskt i kundprofilen i realtid. Poster som rör dessa profiler kan dock fortfarande finnas kvar i datasjön. Efter inställning `isDeleted` till `true`kan du använda fältet för att filtrera bort vilka poster som har tagits bort från dina källor när du frågar efter datasjön. |

{style="table-layout:auto"}

Se guiden på [schemarelationer i Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet.
