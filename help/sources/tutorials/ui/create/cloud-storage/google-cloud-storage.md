---
keywords: Experience Platform;hem;populära ämnen;Google Cloud-lagring;Google molnlagring;GCS;gcs
solution: Experience Platform
title: Skapa en Google Cloud-anslutning för lagringskälla i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en Google Cloud-anslutning för lagringskälla med Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---


# Skapa en [!DNL Google Cloud Storage]-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Google Cloud Storage]-källkoppling (kallas nedan &quot;GCS&quot;) med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig GCS-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

[!DNL Experience Platform] har stöd för följande filformat som ska importeras från externa lagringsplatser:

* Avgränsaravgränsade värden (DSV): Stödet för DSV-formaterade datafiler är för närvarande begränsat till kommaavgränsade värden. Värdet för fältrubriker i DSV-formaterade filer får endast bestå av alfanumeriska tecken och understreck. Stöd för allmänna DSV-filer kommer att ges i framtiden.
* JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
* Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till dina GCS-data på [!DNL Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Åtkomstnyckel-ID | Åtkomstnyckel-ID för [!DNL Google Cloud Storage]-kontot. |
| Nyckel för hemlig åtkomst | Klienthemligheten för [!DNL Google Cloud Storage]-kontot. |

Mer information om hur du kommer igång finns i [autentiseringsguiden för server-till-server](https://cloud.google.com/docs/authentication/production) för [!DNL Google Cloud Storage].

## Anslut ditt [!DNL Google Cloud Storage]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt GCS-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Google Cloud Storage]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny GCS-koppling.

![katalog](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Sidan **[!UICONTROL Connect to Google Cloud Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina GCS-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det GCS-konto som du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt GCS-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/batch/cloud-storage.md).