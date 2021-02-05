---
keywords: Experience Platform;hem;populära ämnen;Azure Event Hubs;Event Hubs;azure event hubs
solution: Experience Platform
title: Skapa en Azure Event Hubs-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en Azure Event Hubs-källanslutning med Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Skapa en [!DNL Azure Event Hubs]-källanslutning i användargränssnittet

>[!NOTE]
>
> [!DNL Azure Event Hubs]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du autentiserar en [!DNL Azure Event Hubs]-källkoppling (kallas nedan &quot;[!DNL Event Hubs]&quot;) med hjälp av användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Event Hubs]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/streaming/cloud-storage-streaming.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera din [!DNL Event Hubs]-källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Den genererade signaturen för delad åtkomst. |
| `namespace` | Namnområdet för [!DNL Event Hubs] som du försöker komma åt. |

Mer information om dessa värden finns i [det här [!DNL Event Hubs] dokumentet](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Anslut ditt [!DNL Event Hubs]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Event Hubs]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. På fliken **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Azure Event Hubs]** under kategorin **[!UICONTROL Cloud Storage]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny händelsehubbar.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Dialogrutan **[!UICONTROL Connect to Azure Event Hubs]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL Event Hubs] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Event Hubs]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit ditt [!DNL Event Hubs]-konto till [!DNL Platform]. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).