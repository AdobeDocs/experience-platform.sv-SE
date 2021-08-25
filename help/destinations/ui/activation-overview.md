---
keywords: aktivera mål;aktivera data
title: Aktiveringsöversikt
type: Tutorial
seo-title: Activation overview
description: Lär dig hur du aktiverar målgruppsdata i Adobe Experience Platform till olika typer av destinationer.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Aktiveringsöversikt

Adobe Experience Platform har stöd för ett stort antal destinationer. Arbetsflödet för målgruppsaktivering varierar mellan olika mål, beroende på vilken typ av målgruppsdata de stöder och frekvensen för dataexporten.

## Aktiveringsmetoder {#activation-methods}

När du har [konfigurerat dina mål](connect-destination.md) kan du aktivera målgruppssegment på flera sätt:

### Aktivera målgrupper från målkatalogen

Mer information om hur du aktiverar målgrupper till ditt mål från målkatalogen finns i följande handböcker:

* [Aktivera målgruppsdata för att direktuppspela segmentexportmål](activate-segment-streaming-destinations.md)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
* [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)

### Aktivera målgrupper från sidan [!UICONTROL Browse]

Följ stegen nedan för att aktivera data till dina mål från sidan **[!UICONTROL Browse]**.

1. Gå till **[!UICONTROL Connections > Destinations]** och välj fliken **[!UICONTROL Browse]**.

   ![Fliken Bläddra](../assets/ui/activation-overview/browse-tab.png)

1. Hitta målanslutningen som du vill använda för att aktivera dina segment, markera de tre punkterna i kolumnen [!UICONTROL Name] och välj sedan **[!UICONTROL Activate segments]**.

   ![Knappen Aktivera segment](../assets/ui/activation-overview/activate-segments.png)

1. Beroende på det valda målet följer du stegen som beskrivs i artiklarna nedan, med början i **[!UICONTROL Select segments]**-steget, för att slutföra aktiveringsarbetsflödet:

   * [Aktivera målgruppsdata för att direktuppspela segmentexportmål](activate-segment-streaming-destinations.md)
   * [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
   * [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)

### Aktivera målgrupper från sidan med segmentinformation {#activate-segment-details}

Du kan aktivera segment till mål från sidan med segmentinformation. Mer information finns i [Segmentinformation](../../segmentation/ui/overview.md#segment-details).

Beroende på det valda målet följer du stegen som beskrivs i artiklarna nedan för att slutföra aktiveringsarbetsflödet:

* [Aktivera målgruppsdata för att direktuppspela segmentexportmål](activate-segment-streaming-destinations.md)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
* [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)