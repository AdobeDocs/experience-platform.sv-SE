---
keywords: Azure Blob;Blob destination;s3;azure blob destination
title: Azure Blob-anslutning
description: Skapa en utgående liveanslutning till ditt Azure Blob-lagringsutrymme för att regelbundet exportera CSV-datafiler från Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 1dd87ce19c3d9f4eb07c49968754ab979b4dee5c
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# [!DNL Azure Blob] anslutning

## Översikt {#overview}

[!DNL Azure Blob] (nedan kallad [!DNL Blob]) är Microsoft lösning för lagring av objekt i molnet. Den här självstudiekursen innehåller steg för att skapa en [!DNL Blob] mål med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Blob] mål kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [aktivera segment till ditt mål](../../ui/activate-batch-profile-destinations.md).

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Filformat som stöds {#file-formats}

[!DNL Experience Platform] stöder följande filformat som ska exporteras till [!DNL Azure Blob]:

* Kommaavgränsade värden (CSV): Stödet för exporterade datafiler är för närvarande begränsat till kommaavgränsade värden.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64-encoded] sträng. Visa ett exempel på en korrekt formaterad nyckel i dokumentationslänken nedan."

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Connection string]**: anslutningssträngen krävs för att komma åt data i blobblagringen. The [!DNL Blob] anslutningssträngsmönster börjar med: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Mer information om hur du konfigurerar [!DNL Blob] anslutningssträng, se [Konfigurera en anslutningssträng för ett Azure-lagringskonto](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) i Microsoft-dokumentationen.
* **[!UICONTROL Encryption key]**: Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64-encoded] sträng. Visa ett exempel på en korrekt formaterad, base64-kodad nyckel i dokumentationslänken nedan. Mittdelen förkortas av utrymmesskäl.

![Bild som visar ett exempel på en korrekt formaterad och base64-krypterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL Container]**: ange namnet på [!DNL Azure Blob Storage] behållare som ska användas av det här målet.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

För [!DNL Azure Blob Storage] destinationer, [!DNL Platform] skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringssjälvstudiekursen.