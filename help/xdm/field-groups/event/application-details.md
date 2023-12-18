---
title: Fältgrupp för programdetaljschema
description: Läs mer om schemafältgruppen Programinformation.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# [!UICONTROL Application Details] schemafältgrupp

[!UICONTROL Application Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `application` till ett schema, som samlar in programrelaterad information som krascher, funktionsanvändning, starter och uppgraderingar.

![](../../images/field-groups/application-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `application` | [[!UICONTROL Application]](../../data-types/financial-account.md) | Hämtar programinformation som är relaterad till en händelse, inklusive namnet på programmet, appversionen, installationer, starter, krascher och stängningar. Det kan antingen vara det program som händelsen aktiverar (till exempel målet för ett push-meddelande som skickas) eller det program som händelsen kommer från (till exempel ett klick eller en inloggning). |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
