---
title: Schemafältgrupp för systeminformation
description: Lär dig mer om schemafältgruppen Sektionsverktygsinformation.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Sitetool Details]

[!UICONTROL Sitetool Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md). Fältgruppen tillhandahåller ett enskilt `sitetool`-objekt till ett schema, som samlar in information som samlats in av ett sitetool.

![Fältgruppsstruktur](../../images/field-groups/sitetool-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `dataGatheringEvent` | Objekt | Anger om den här händelsen är en datainsamlingshändelse tillsammans med annan relaterad information. Innehåller följande egenskaper:<ul><li>`data`: (Karta) Innehåller JSON-data som samlas in och skickas som en del av frågesport, enkät eller poll-sändningshändelse.</li><li>`isTrue`: (Boolean) Anger om den här händelsen är en datainsamlingshändelse som frågor, undersökning eller omröstning.</li><li>`score`: (heltal) Det poängvärde som säkras av skådespelaren baserat på händelsesvar.</li></ul> |
| `actor` | Sträng | En person/medlem som utförde åtgärden. |
| `actorID` | Sträng | En unik identifierare för den person/medlem som utförde åtgärden. |
| `isKeyEvent` | Boolean | Anger om händelsen är en nyckelhändelse. |
| `name` | Sträng | Platsverktygets namn, till exempel chatbot, survey och så vidare. |
| `section` | Sträng | Den relevanta delen av sitetool som huvud eller sub. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
