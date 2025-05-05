---
title: Schemafältgrupp för MediaAnalytics-interaktionsinformation
description: Läs mer om schemafältgruppen MediaAnalytics Interaction Details.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL MediaAnalytics Interaction Details]

[!UICONTROL MediaAnalytics Interaction Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md). Använd den här fältgruppen för att samla in datafält som innehåller omfattande övervakning och analys av interaktioner med mediematerial på olika plattformar eller i olika kanaler.

![Ett schemadiagram för schemafältgruppen [!UICONTROL MediaAnalytics Interaction Details].](../../images/field-groups/mediaanalytics-interaction.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---| --- | --- | --- |
| [!UICONTROL Media Collection Details] | `mediaCollection` | [[!UICONTROL Media Collection details]](../../data-types/media-collection-details.md) | Attribut som är relaterade till en samling medieobjekt. Använd Media Collection-fälten för att hämta in data och skicka dem till andra Adobe-tjänster för vidare bearbetning. |
| [!UICONTROL Media Reporting Details] | `mediaReporting` | [[!UICONTROL Media Reporting details]](../../data-types/media-reporting-details.md) | Rapporteringsinformation och mätvärden som är kopplade till medieinnehållet. * Media Reporting-fält används av Adobe-tjänster för att analysera de Media Collection-fält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån. |
| [!UICONTROL List Of Media Collection Downloaded Content Events] | `mediaDownloadedEvents` | [!UICONTROL Array] av [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Händelser som spårar nedladdningen av innehåll i mediesamlingen. |

{style="table-layout:auto"}

>[!TIP]
>
>Du kan dölja fält som inte används av Media Edge API. Om du döljer dessa fält blir schemat enklare att läsa och förstå, men det är inte nödvändigt. Dessa fält refererar endast till fälten i fältgruppen [!UICONTROL MediaAnalytics Interaction Details]. Om du vill förbättra läsbarheten i användargränssnittet för Experience Platform följer du instruktionerna i [dokumentationen för Media Analytics om hur du döljer oanvända fält](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html?lang=sv-SE#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html?lang=sv-SE#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
