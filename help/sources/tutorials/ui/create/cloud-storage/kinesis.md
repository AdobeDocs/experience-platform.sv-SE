---
keywords: Experience Platform;hem;populära ämnen;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Skapa en Amazon Kinesis Source Connection i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Amazon Kinesis med Adobe Experience Platform gränssnitt.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# Skapa en [!DNL Amazon Kinesis] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för hur du autentiserar en [!DNL Amazon Kinesis] (nedan kallad [!DNL "Kinesis"]) med hjälp av [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Kinesis] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/streaming/cloud-storage-streaming.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera [!DNL Kinesis] källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID för din [!DNL Kinesis] konto. |
| `Secret access key` | Den hemliga åtkomstnyckeln för [!DNL Kinesis] konto. |
| `region` | Regionen för din AWS-server. |

Mer information om dessa värden finns i [this [!DNL Kinesis] dokument](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Koppla samman [!DNL Kinesis] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Kinesis] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Cloud Storage]** kategori, välj **[!UICONTROL Amazon Kinesis]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Kinesis] koppling.

![](../../../../images/tutorials/create/kinesis/catalog.png)

The **[!UICONTROL Connect to Amazon Kinesis]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och din [!DNL Kinesis] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Kinesis] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit till [!DNL Kinesis] konto till [!DNL Platform]. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
