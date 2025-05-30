---
title: Aktivera Audience Manager-målgrupper genom utökad aktivering
description: Lär dig hur du kan aktivera Audience Manager målgrupper för sociala medier och annonser via Audience Manager Expanded Activation (aktivering).
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Aktivera målgrupper med Audience Manager Expanded Activation

På den här sidan beskrivs det kompletta arbetsflöde som du måste följa för att aktivera målgrupper från Audience Manager till målplattformarna som stöds av Expanded Activation (Utökad aktivering).

## Innan du börjar {#before-you-begin}

Stegen som beskrivs i den här guiden förutsätter att du har läst översiktssidan för [Utökad aktivering](overview.md) och att du har bekräftat att du uppfyller kraven för målgruppsaktivering.

>[!IMPORTANT]
>
>Om du vill aktivera målgrupper via [!DNL Expanded Activation] kontrollerar du att dina Audience Manager-målgrupper är baserade på **hashade e-postadresser**. Mer information finns i [förutsättningarna](overview.md#prerequisites).

## Steg 1: Konfigurera Audience Manager-källanslutningen {#configure-source}

[Audience Manager-källkopplingen](../sources/connectors/adobe-applications/audience-manager.md) skickar målgruppsdata som samlats in i Adobe Audience Manager för aktivering på de målplattformar som stöds av utökad aktivering.

Följ guiden om hur du [skapar en Audience Manager-källanslutning](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) för att konfigurera din källanslutning.

![Experience Platform UI-bild som visar fliken Källor med Audience Manager-källanslutningen.](assets/sources-tab.png)

>[!TIP]
>
>Adobe Audience Manager-källkopplingen är den enda källkopplingen som är tillgänglig vid utökad aktivering.
>
>Om du vill importera målgrupper baserat på ytterligare identifierare måste du köpa en utgåva av [Real-Time CDP](../rtcdp/overview.md). Kontakta Adobe om du vill ha mer information.

### Visa och övervaka importerade målgrupper {#view-audiences}

Publiken som du aktiverar via utökad aktivering från Audience Manager är tillgängliga för dig att visa på kontrollpanelen **[!UICONTROL Audiences]**.

Om du vill visa dina målgrupper går du till **[!UICONTROL Customer]** -> **[!UICONTROL Audiences]** -> **[!UICONTROL Browse]**.

![Experience Platform-gränssnittsbild som visar sidan Publiker.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Det kan ta upp till 48 timmar för publiken att utnyttja den utökade aktiveringen fullt ut. Detta gäller även för uppdateringar av befintliga Audience Manager-målgrupper.
>* Nyligen skapade Audience Manager-målgrupper visas inte automatiskt i Utökad aktivering. Om du vill importera nya segment i den utökade aktiveringen måste du lägga till dem via Audience Manager källanslutning.

Gå till [steg 2](#create-destination-connection) när du har konfigurerat din Audience Manager-källanslutning.

## Steg 2: Skapa en ny målanslutning {#create-destination-connection}

Innan du kan skicka dina Audience Manager-målgrupper till en önskad målplattform måste du först skapa en anslutning till en målplattform.

Gå till **[!UICONTROL Connections]** -> **[!UICONTROL Destinations]** -> **[!UICONTROL Catalog]** i vänster sidofält.

De tillgängliga målkategorierna för [!DNL Expanded Activation] är [advertising](../destinations/catalog/advertising/overview.md) och [social](../destinations/catalog/social/overview.md).

![Experience Platform-gränssnittsbild visar målkatalogen för utökad aktivering.](assets/destination-catalog.png)

Om du vill skapa en ny anslutning till en målplattform följer du guiden [Skapa en ny målanslutning](../destinations/ui/connect-destination.md). Gå sedan till [steg 3](#activate-audiences).

## Steg 3: Aktivera målgrupper till er målgrupp {#activate-audiences}

När du har [kapslat in Audience Manager-målgrupper](#configure-source) och [skapat en ny målanslutning](#create-destination-connection) kan du nu aktivera dina målgrupper till den målplattform du väljer.

![Experience Platform-gränssnittsbild visar målkatalogen för utökad aktivering.](assets/activate-audiences.png)

Om du vill aktivera målgrupper till ditt mål följer du guiden [hur du aktiverar målgrupper till direktuppspelningsmål](../destinations/ui/activate-segment-streaming-destinations.md).

## Verifiera målgruppsaktivering {#verify}

Mer information om hur du övervakar dataflödet till dina mål finns i [dokumentationen för målövervakning](../dataflows/ui/monitor-destinations.md).
