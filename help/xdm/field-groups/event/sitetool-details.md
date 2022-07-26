---
title: Schemafältgrupp för systeminformation
description: Det här dokumentet innehåller en översikt över schemafältgruppen Sektionsverktygsinformation.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---

# [!UICONTROL Sitetool Details] schemafältgrupp

[!UICONTROL Sitetool Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `sitetool` till ett schema, som samlar in information som samlats in av ett sitetool.

![Fältgruppstruktur](../../images/field-groups/sitetool-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `dataGatheringEvent` | Objekt | Anger om den här händelsen är en datainsamlingshändelse tillsammans med annan relaterad information. Innehåller följande egenskaper:<ul><li>`data`: (Karta) Innehåller de JSON-data som samlas in och skickas som en del av frågebatterier, enkäter eller omröstningshändelser.</li><li>`isTrue`: (Boolean) Anger om den här händelsen är en datainsamlingshändelse som frågor, undersökning eller omröstning.</li><li>`score`: (Heltal) Det poängvärde som säkras av skådespelaren baserat på händelsesvar.</li></ul> |
| `actor` | Sträng | En person/medlem som utförde åtgärden. |
| `actorID` | Sträng | En unik identifierare för den person/medlem som utförde åtgärden. |
| `isKeyEvent` | Boolean | Anger om den här händelsen är en nyckelhändelse. |
| `name` | Sträng | Platsverktygets namn, till exempel chatbot, survey och så vidare. |
| `section` | Sträng | Den relevanta delen av sitetool som huvud eller sub. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
