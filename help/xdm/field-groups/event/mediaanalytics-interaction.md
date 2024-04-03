---
title: Schemafältgrupp för MediaAnalytics-interaktionsinformation
description: Läs mer om schemafältgruppen MediaAnalytics Interaction Details.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# [!UICONTROL MediaAnalytics Interaction Details] schemafältgrupp

[!UICONTROL MediaAnalytics Interaction Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Använd den här fältgruppen för att samla in datafält som innehåller omfattande övervakning och analys av interaktioner med mediematerial på olika plattformar eller i olika kanaler.

![Ett schemadiagram över [!UICONTROL MediaAnalytics Interaction Details] schemafältgrupp.](../../images/field-groups/mediaanalytics-interaction.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---| --- | --- | --- |
| [!UICONTROL Media Collection Details] | `mediaCollection` | [[!UICONTROL Media Collection details]](../../data-types/media-collection-details.md) | Attribut som är relaterade till en samling medieobjekt. Använd Media Collection-fälten för att hämta in data och skicka dem till andra Adobe-tjänster för vidare bearbetning. |
| [!UICONTROL Media Reporting Details] | `mediaReporting` | [[!UICONTROL Media Reporting details]](../../data-types/media-reporting-details.md) | Rapporteringsinformation och mätvärden som är kopplade till medieinnehållet. * Media Reporting-fält används av Adobe-tjänster för att analysera de Media Collection-fält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån. |
| [!UICONTROL List Of Media Collection Downloaded Content Events] | `mediaDownloadedEvents` | [!UICONTROL Array] av [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Händelser som spårar nedladdningen av innehåll i mediesamlingen. |

{style="table-layout:auto"}

>[!TIP]
>
>Du kan dölja fält som inte används av Media Edge API. Om du döljer dessa fält blir schemat enklare att läsa och förstå, men det är inte nödvändigt. Dessa fält refererar endast till fälten i [!UICONTROL MediaAnalytics Interaction Details] fältgrupp. Följ instruktionerna i [Media Analytics-dokumentation om hur du döljer oanvända fält](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
