---
title: Aktivera Audience Manager-målgrupper genom utökad aktivering
description: Lär dig hur du kan aktivera Audience Manager-målgrupper för sociala medier och annonser via Audience Manager Expanded Activation (aktivering).
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# Aktivera målgrupper via Audience Manager-utökad aktivering

På den här sidan beskrivs det kompletta arbetsflöde som du måste följa för att aktivera målgrupper från Audience Manager till målplattformarna som stöds av Expanded Activation (Utökad aktivering).

## Innan du börjar {#before-you-begin}

Stegen som beskrivs i den här guiden förutsätter att du har läst [Översikt över utökad aktivering](overview.md) och du har bekräftat att du uppfyller kraven för målgruppsaktivering.

>[!IMPORTANT]
>
>Aktivera målgrupper genom [!DNL Expanded Activation], se till att era Audience Manager-målgrupper är baserade på **hash-kodade e-postadresser**. Se [krav](overview.md#prerequisites) för mer information.

## Steg 1: Konfigurera Audience Manager-källanslutningen {#configure-source}

The [Audience Manager-källanslutning](../sources/connectors/adobe-applications/audience-manager.md) skickar målgruppsdata som samlats in i Adobe Audience Manager för aktivering på de målplattformar som stöds av Expanded Activation (Expanded Activation).

Följ guiden om hur du [skapa en Audience Manager-källanslutning](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) för att konfigurera din källanslutning.

![Bild av användargränssnittet för plattformen som visar fliken Källor med Audience Manager-källanslutningen.](assets/sources-tab.png)

>[!TIP]
>
>Adobe Audience Manager-källkopplingen är den enda källkopplingen som är tillgänglig vid utökad aktivering.
>
>Om du vill importera målgrupper baserat på ytterligare identifierare måste du köpa en utgåva av [Real-Time CDP](../rtcdp/overview.md). Kontakta din Adobe-representant om du vill ha mer information.

### Visa och övervaka importerade målgrupper {#view-audiences}

De målgrupper du har aktiverat i Expanded Activation från Audience Manager finns tillgängliga i **[!UICONTROL Audiences]** kontrollpanel.

Om du vill se era målgrupper går du till **[!UICONTROL Customer]** -> **[!UICONTROL Audiences]** -> **[!UICONTROL Browse]**.

![Plattformsgränssnittsbild som visar sidan Publiker.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Det kan ta upp till 48 timmar för publiken att utnyttja den utökade aktiveringen fullt ut. Detta gäller även för uppdateringar av befintliga Audience Manager-målgrupper.
>* Nyligen skapade målgrupper i Audience Manager visas inte automatiskt i Utökad aktivering. Om du vill importera nya segment i utökad aktivering måste du lägga till dem via Audience Manager-källkopplingen.

När du har konfigurerat Audience Manager-källkopplingen går du till [steg 2](#create-destination-connection).

## Steg 2: Skapa en ny målanslutning {#create-destination-connection}

Innan du kan skicka målgrupper från Audience Manager till den målplattform du föredrar måste du först skapa en anslutning till en målplattform.

Gå till vänster sidofält **[!UICONTROL Connections]** -> **[!UICONTROL Destinations]** -> **[!UICONTROL Catalog]**.

Tillgängliga målkategorier för [!DNL Expanded Activation] är [reklam](../destinations/catalog/advertising/overview.md) och [social](../destinations/catalog/social/overview.md).

![Plattformsgränssnittsbild som visar målkatalogen för utökad aktivering.](assets/destination-catalog.png)

Om du vill skapa en ny anslutning till en målplattform följer du guiden på [hur du skapar en ny målanslutning](../destinations/ui/connect-destination.md). Gå sedan till [steg 3](#activate-audiences).

## Steg 3: Aktivera målgrupper till er målgrupp {#activate-audiences}

När du har lyckats [målgrupper med inkapslade Audience Manager](#configure-source) och [skapade en ny målanslutning](#create-destination-connection)kan ni nu aktivera era målgrupper på valfri målplattform.

![Plattformsgränssnittsbild som visar målkatalogen för utökad aktivering.](assets/activate-audiences.png)

Om du vill aktivera målgrupper till ditt mål följer du guiden [aktivera målgrupper för direktuppspelningsmål](../destinations/ui/activate-segment-streaming-destinations.md).

## Verifiera målgruppsaktivering {#verify}

Kontrollera [dokumentation för målövervakning](../dataflows/ui/monitor-destinations.md) om du vill ha detaljerad information om hur du övervakar dataflödet till dina mål.