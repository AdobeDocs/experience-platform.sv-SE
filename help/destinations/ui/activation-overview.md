---
keywords: aktivera mål;aktivera data
title: Aktiveringsöversikt
type: Tutorial
description: Lär dig hur du aktiverar målgrupper i Adobe Experience Platform till olika typer av destinationer.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Aktiveringsöversikt

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Adobe Experience Platform har stöd för ett stort antal destinationer. Arbetsflödet för målgruppsaktivering varierar mellan olika mål, beroende på vilken typ av målgruppsdata de stöder och frekvensen för dataexporten.

## Aktiveringsmetoder {#activation-methods}

Efter dig [konfigurera ditt mål](connect-destination.md)kan ni aktivera målgrupper på flera sätt:

### Aktivera målgrupper från målkatalogen

Mer information om hur du aktiverar målgrupper till ditt mål från målkatalogen finns i följande handböcker:

* [Aktivera målgruppsdata för direktuppspelad målgruppsexport](activate-segment-streaming-destinations.md)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
* [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)

### Aktivera målgrupper från [!UICONTROL Browse] page

Följ stegen nedan för att aktivera data till dina destinationer från **[!UICONTROL Browse]** sida.

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Browse]** -fliken.

   ![Fliken Bläddra](../assets/ui/activation-overview/browse-tab.png)

1. Sök efter den målanslutning som du vill använda för att aktivera dina segment, välj de tre punkterna i dialogrutan [!UICONTROL Name] kolumn, markera **[!UICONTROL Activate audiences]**.

   ![Knappen Aktivera målgrupper](../assets/ui/activation-overview/activate-segments.png)

1. Beroende på vilket mål du väljer följer du de steg som beskrivs i artiklarna nedan, med början med **[!UICONTROL Select segments]** för att slutföra aktiveringsarbetsflödet:

   * [Aktivera målgruppsdata för direktuppspelad målgruppsexport](activate-segment-streaming-destinations.md)
   * [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
   * [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)

### Aktivera målgrupper från informationssidan för målgrupper {#activate-audience-details}

Du kan aktivera målgrupper till mål från sidan med målgruppsinformation. Se [Målgruppsinformation](../../segmentation/ui/audience-portal.md#audience-details) för mer information.

Beroende på det valda målet följer du stegen som beskrivs i artiklarna nedan för att slutföra aktiveringsarbetsflödet:

* [Aktivera målgruppsdata för direktuppspelad målgruppsexport](activate-segment-streaming-destinations.md)
* [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](activate-streaming-profile-destinations.md)
* [Aktivera målgruppsdata för att batchprofilera exportmål](activate-batch-profile-destinations.md)
