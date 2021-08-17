---
keywords: Azure Blob;Blob destination;s3;azure blob destination
title: Azure Blob-anslutning
description: Skapa en utgående liveanslutning till ditt Azure Blob-lagringsutrymme för att regelbundet exportera tabbavgränsade eller CSV-datafiler från Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---

# [!DNL Azure Blob] anslutning

## Översikt {#overview}

[!DNL Azure Blob] (nedan kallat  [!DNL Blob]) är Microsofts objektlagringslösning för molnet. I den här självstudien beskrivs stegen för hur du skapar ett [!DNL Blob]-mål med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL Blob]-mål kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om att [aktivera segment till ditt mål](../../ui/activate-batch-profile-destinations.md).

## Filformat som stöds {#file-formats}

[!DNL Experience Platform] stöder följande filformat som ska exporteras till  [!DNL Blob]:

* Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaavgränsade värden. Stöd för allmänna DSV-filer kommer att ges i framtiden.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Connection string]**: anslutningssträngen krävs för att komma åt data i blobblagringen. Anslutningssträngsmönstret [!DNL Blob] börjar med: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Mer information om hur du konfigurerar din [!DNL Blob]-anslutningssträng finns i [Konfigurera en anslutningssträng för ett Azure-lagringskonto](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) i Microsoft-dokumentationen.

* Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64]-kodad sträng.
* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL Container]**: Ange namnet på den  [!DNL Azure Blob Storage] behållare som ska användas för detta mål.

Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64]-kodad sträng.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att batchprofilens exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till det här målet.
