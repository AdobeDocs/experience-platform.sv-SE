---
title: Klassen XDM Business Campaign-medlemmar
description: Det här dokumentet innehåller en översikt över XDM Business Campaign-medlemsklassen i Experience Data Model (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign Members] klass (Beta)

>[!IMPORTANT]
>
>Den här klassen finns som en del av Real-time Customer Data Platform B2B Edition, som för närvarande är en betaversion. Dokumentationen och funktionerna kan komma att ändras.

[!UICONTROL XDM Business Campaign Members] är en XDM-klass (Experience Data Model) som beskriver en kontakt eller ett lead som är kopplat till en företagskampanj.

![](../../images/classes/b2b/business-campaign-members.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den associerade kampanjen. |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för kampanjmedlemsenheten. |
| `extSourceSystemAudit` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Om kampanjmedlemskapet kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den person som är medlem i den associerade kampanjen. |
| `_id` | Sträng | En unik identifierare för posten. Detta är ett systemgenererat värde som är skilt från `campaignMemberID`. |
| `campaignID` | Sträng | Ett unikt ID för den associerade kampanjen. |
| `campaignMemberID` | Sträng | Ett unikt ID för kampanjmedlemsenheten. |
| `personId` | Sträng | Ett unikt ID för den person som är medlem i den associerade kampanjen. |

{style=&quot;table-layout:auto&quot;}

Läs guiden om [schemarelationer i CDP B2B Edition](../../tutorials/relationship-b2b.md) i realtid om du vill veta hur den här klassen begreppsmässigt relaterar till de andra B2B-klasserna och hur du kan etablera dessa relationer i Adobe Experience Platform användargränssnitt.
