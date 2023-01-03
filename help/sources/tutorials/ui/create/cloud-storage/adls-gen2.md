---
keywords: Experience Platform;hem;populära ämnen;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls connector
solution: Experience Platform
title: Skapa en källanslutning för Azure Data Lake Storage Gen2 i gränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Azure Data Lake Storage Gen2-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# Skapa en [!DNL Azure Data Lake Storage Gen2] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för hur du autentiserar en [!DNL Azure Data Lake Storage Gen2] (nedan kallad[!DNL ADLS Gen2]&quot;) som använder [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig ADLS Gen2-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera [!DNL ADLS Gen2] källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | Slutpunkten för [!DNL ADLS Gen2]. |
| `servicePrincipalId` | Programmets klient-ID. |
| `servicePrincipalKey` | Programmets nyckel. |
| `tenant` | Klientinformationen som innehåller ditt program. |

Mer information om dessa värden finns i [this [!DNL ADLS Gen2] dokument](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Koppla samman [!DNL ADLS Gen2] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL ADLS Gen2] konto att ansluta till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL Azure Data Lake Gen2]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny ADLS Gen2-anslutning.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

The **[!UICONTROL Connect to Azure Data Lake Gen2]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och din [!DNL ADLS Gen2] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL ADLS Gen2] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL ADLS Gen2] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
