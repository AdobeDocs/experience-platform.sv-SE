---
keywords: Experience Platform;hem;populära ämnen;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Skapa en Amazon Kinesis Source Connection i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Amazon Kinesis med Adobe Experience Platform gränssnitt.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
translation-type: tm+mt
source-git-commit: d6f1521470b8dc630060584189690545c724de6b
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# Skapa en [!DNL Amazon Kinesis]-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du autentiserar en [!DNL Amazon Kinesis]-källkoppling (kallas nedan [!DNL "Kinesis"]) med hjälp av användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Kinesis]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/streaming/cloud-storage-streaming.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera din [!DNL Kinesis]-källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID för ditt [!DNL Kinesis]-konto. |
| `Secret access key` | Den hemliga åtkomstnyckeln för ditt [!DNL Kinesis]-konto. |
| `region` | AWS-serverns region. |

Mer information om dessa värden finns i [det här [!DNL Kinesis] dokumentet](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Anslut ditt [!DNL Kinesis]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Kinesis]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Amazon Kinesis]** under kategorin **[!UICONTROL Cloud Storage]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Kinesis]-koppling.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Dialogrutan **[!UICONTROL Connect to Amazon Kinesis]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL Kinesis] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Kinesis]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit till ditt [!DNL Kinesis]-konto till [!DNL Platform]. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
