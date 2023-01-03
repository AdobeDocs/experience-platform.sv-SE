---
keywords: Experience Platform;hem;populära ämnen;Azure File Storage;Azure File Storage Connector
solution: Experience Platform
title: Skapa en Azure File Storage Source-anslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Azure File Storage-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# Skapa en [!DNL Azure File Storage] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för hur du autentiserar en [!DNL Azure File Storage] källkoppling med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Azure File Storage] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera [!DNL Azure File Storage] källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Slutpunkten för [!DNL Azure File Storage] -instans som du använder. |
| `userId` | Användaren har tillräcklig åtkomst till [!DNL Azure File Storage] slutpunkt. |
| `password` | The [!DNL Azure File Storage] åtkomstnyckel. |

Mer information om hur du kommer igång finns i [this [!DNL Azure File Storage] dokument](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Koppla samman [!DNL Azure File Storage] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Azure File Storage] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL Azure File Storage]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Azure File Storage] koppling.

![katalog](../../../../images/tutorials/create/azure-file-storage/catalog.png)

The **[!UICONTROL Connect to Azure File Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Azure File Storage] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/azure-file-storage/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Azure File Storage] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Azure File Storage] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
