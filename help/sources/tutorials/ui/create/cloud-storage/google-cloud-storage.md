---
title: Skapa en Google Cloud-anslutning för lagringskälla i användargränssnittet
description: Lär dig hur du skapar en källanslutning till en lagringskälla i Google Cloud med hjälp av Adobe Experience Platform användargränssnitt.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---

# Skapa en [!DNL Google Cloud Storage] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Google Cloud Storage] källanslutning med Adobe Experience Platform UI.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Google Cloud Storage] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Filformat som stöds

[!DNL Experience Platform] har stöd för följande filformat som ska importeras från externa lagringsplatser:

* Avgränsaravgränsade värden (DSV): Alla värden med ett tecken kan användas som avgränsare för DSV-formaterade datafiler.
* JavaScript-objektnotation (JSON): JSON-formaterade datafiler måste vara XDM-kompatibla.
* Apache Parquet: Parquet-formaterade datafiler måste vara XDM-kompatibla.

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Google Cloud Storage] data på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Åtkomstnyckel-ID | En 61-siffrig alfanumerisk sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform. |
| Nyckel för hemlig åtkomst | En 40-siffrig, base-64-kodad sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform. |
| Bucketnamn | Namnet på [!DNL Google Cloud Storage] bucket. Du måste ange ett bucketnamn om du vill ge åtkomst till en viss undermapp i molnlagringen. |
| Mappsökväg | Sökvägen till mappen som du vill ge åtkomst till. |

Mer information om dessa värden finns i [Google Cloud Storage HMAC-nycklar](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guide. Anvisningar om hur du skapar ditt eget ID för åtkomstnyckel och hemlig åtkomstnyckel finns i [[!DNL Google Cloud Storage] översikt](../../../../connectors/cloud-storage/google-cloud-storage.md).

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Google Cloud Storage] konto till plattform.

## Koppla samman [!DNL Google Cloud Storage] konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Google Cloud Storage]** och sedan markera **[!UICONTROL Add data]**.

![Plattformens användargränssnitt visar källkatalogsidan.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

The **[!UICONTROL Connect to Google Cloud Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Google Cloud Storage] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![Plattformsgränssnittsskärmen visar den befintliga kontosidan för en Google Cloud-lagringskälla](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Google Cloud Storage] autentiseringsuppgifter. Under det här steget kan du även ange vilka undermappar ditt konto ska ha åtkomst till genom att definiera namnet på sökvägen till undermappen.

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Plattformsgränssnittsskärmen visar den nya kontosidan för en Google Cloud-lagringskälla.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Google Cloud Storage] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
