---
title: Klassen XDM Business Campaign-medlemmar
description: Lär dig mer om XDM Business Campaign-klassen i Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# klassen [!UICONTROL XDM Business Campaign Members]

>[!IMPORTANT]
>
>Den här klassen är avsedd att användas av organisationer med åtkomst till [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Du måste ha tillgång till Real-Time CDP B2B Edition för att den här klassen ska kunna delta i [kundprofilen i realtid](../../../profile/home.md).

[!UICONTROL XDM Business Campaign Members] är en XDM-standardklass (Experience Data Model) som beskriver en kontakt eller lead som är associerad med en företagskampanj.

![Strukturen för XDM Business Campaign-medlemsklassen så som den visas i användargränssnittet](../../images/classes/b2b/business-campaign-members.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den associerade kampanjen. |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kampanjmedlemsenheten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kampanjmedlemskapet kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den person som är medlem i den associerade kampanjen. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `campaignMemberID`. |

{style="table-layout:auto"}

Om du vill lära dig hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform-gränssnittet läser du guiden om [schemarelationer i Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md)

Ytterligare fält som är kompatibla med den här klassen finns i fältgruppsreferensen för [[!UICONTROL XDM Business Campaign Member Details]](../../field-groups/b2b-campaign-members/details.md).
