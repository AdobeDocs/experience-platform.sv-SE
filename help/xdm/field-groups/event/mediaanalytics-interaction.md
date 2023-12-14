---
title: Schemafältgrupp för MediaAnalytics-interaktionsinformation
description: Läs mer om schemafältgruppen MediaAnalytics Interaction Details.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# [!UICONTROL MediaAnalytics Interaction Details] schemafältgrupp

[!UICONTROL MediaAnalytics Interaction Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Använd den här fältgruppen för att samla in datafält som innehåller omfattande övervakning och analys av interaktioner med mediematerial på olika plattformar eller i olika kanaler.

![Ett schemadiagram över [!UICONTROL MediaAnalytics Interaction Details] schemafältgrupp.](../../images/field-groups/mediaanalytics-interaction.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---| --- | --- | --- |
| [!UICONTROL Media Collection Details] | `mediaCollection` | [[!UICONTROL Media details information]](../../data-types/media-details-information.md) | Attribut som är relaterade till en samling medieobjekt. |
| [!UICONTROL Media Reporting Details] | `mediaReporting` | [[!UICONTROL Media details information]](../../data-types/media-details-information.md) | Rapporteringsinformation och mätvärden som är kopplade till medieinnehållet. |
| [!UICONTROL List Of Media Collection Downloaded Content Events] | `mediaDownloadedEvents` | [!UICONTROL Array] av [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Händelser som spårar nedladdningen av innehåll i mediesamlingen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
