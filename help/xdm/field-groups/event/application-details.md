---
title: Fältgrupp för programdetaljschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen Programinformation.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# [!UICONTROL Application Details] schemafältgrupp

[!UICONTROL Application Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `application` till ett schema, som samlar in programrelaterad information som krascher, funktionsanvändning, starter och uppgraderingar.

![](../../images/field-groups/application-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `application` | [[!UICONTROL Application]](../../data-types/financial-account.md) | Hämtar programinformation som är relaterad till en händelse, inklusive namnet på programmet, appversionen, installationer, starter, krascher och stängningar. Det kan antingen vara det program som händelsen aktiverar (till exempel målet för ett push-meddelande som skickas) eller det program som händelsen kommer från (till exempel ett klick eller en inloggning). |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
