---
keywords: Experience Platform;hem;populära ämnen;Azure Event Hubs;Event Hubs;azure event hubs
solution: Experience Platform
title: Skapa en Azure Event Hubs-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Azure Event Hubs-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Skapa en [!DNL Azure Event Hubs] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för hur du autentiserar en [!DNL Azure Event Hubs] (nedan kallad[!DNL Event Hubs]&quot;) som använder [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Event Hubs] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/streaming/cloud-storage-streaming.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera [!DNL Event Hubs] källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `sasKeyName` | Auktoriseringsregelns namn, som också kallas SAS-nyckelnamn. |
| `sasKey` | Primärnyckeln för [!DNL Event Hubs] namnutrymme. The `sasPolicy` som `sasKey` motsvarar måste ha `manage` rättigheter som konfigurerats för [!DNL Event Hubs] lista som ska fyllas i. |
| `namespace` | Namnutrymmet för [!DNL Event Hubs] du försöker komma åt. |

Mer information om dessa värden finns i [this [!DNL Event Hubs] dokument](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Koppla samman [!DNL Event Hubs] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Event Hubs] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** På -fliken visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Cloud Storage]** kategori, välj **[!UICONTROL Azure Event Hubs]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny Event Hubs-anslutning.

![](../../../../images/tutorials/create/eventhub/catalog.png)

The **[!UICONTROL Connect to Azure Event Hubs]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och din [!DNL Event Hubs] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Event Hubs] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du kopplat samman [!DNL Event Hubs] konto till [!DNL Platform]. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
