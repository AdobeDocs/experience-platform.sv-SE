---
keywords: aktivera mål;aktivera data
title: Aktiveringsöversikt
type: Tutorial
seo-title: Activation overview
description: Lär dig hur du aktiverar målgruppsdata i Adobe Experience Platform till olika typer av destinationer.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: 5240e0db96a5072ab02a4c8b52e9c2d3dd4d6aa0
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Aktiveringsöversikt

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Adobe Experience Platform har stöd för ett stort antal destinationer. Arbetsflödet för målgruppsaktivering varierar mellan olika mål, beroende på vilken typ av målgruppsdata de stöder och frekvensen för dataexporten.

## Aktiveringsmetoder {#activation-methods}

Efter [konfigurera ditt mål](connect-destination.md)kan ni aktivera målgruppssegment på flera sätt:

### Aktivera målgrupper från målkatalogen

Mer information om hur du aktiverar målgrupper till ditt mål från målkatalogen finns i följande handböcker:

* [Aktivera målgruppsdata för att direktuppspela segmentexportmål](activate-segment-streaming-destinations.md)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
* [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)

### Aktivera målgrupper från [!UICONTROL Browse] page

Följ stegen nedan för att aktivera data till dina destinationer från **[!UICONTROL Browse]** sida.

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Browse]** -fliken.

   ![Fliken Bläddra](../assets/ui/activation-overview/browse-tab.png)

1. Hitta den målanslutning som du vill använda för att aktivera dina segment, välj de tre punkterna i dialogrutan [!UICONTROL Name] kolumn, markera **[!UICONTROL Activate segments]**.

   ![Knappen Aktivera segment](../assets/ui/activation-overview/activate-segments.png)

1. Beroende på vilket mål du väljer följer du de steg som beskrivs i artiklarna nedan, med början med **[!UICONTROL Select segments]** för att slutföra aktiveringsarbetsflödet:

   * [Aktivera målgruppsdata för att direktuppspela segmentexportmål](activate-segment-streaming-destinations.md)
   * [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
   * [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)

### Aktivera målgrupper från sidan med segmentinformation {#activate-segment-details}

Du kan aktivera segment till mål från sidan med segmentinformation. Se [Segmentinformation](../../segmentation/ui/overview.md#segment-details) för mer information.

Beroende på det valda målet följer du stegen som beskrivs i artiklarna nedan för att slutföra aktiveringsarbetsflödet:

* [Aktivera målgruppsdata för att direktuppspela segmentexportmål](activate-segment-streaming-destinations.md)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
* [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)
