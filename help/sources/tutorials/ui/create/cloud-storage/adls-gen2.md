---
keywords: Experience Platform;hem;populära ämnen;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls connector
solution: Experience Platform
title: Skapa en källanslutning för Azure Data Lake Storage Gen2 i gränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en Azure Data Lake Storage Gen2-källanslutning med Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# Skapa en [!DNL Azure Data Lake Storage Gen2]-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du autentiserar en [!DNL Azure Data Lake Storage Gen2]-källkoppling (kallas nedan &quot;[!DNL ADLS Gen2]&quot;) med hjälp av användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig ADLS Gen2-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera din [!DNL ADLS Gen2]-källkoppling måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | Slutpunkten för [!DNL ADLS Gen2]. |
| `servicePrincipalId` | Programmets klient-ID. |
| `servicePrincipalKey` | Programmets nyckel. |
| `tenant` | Klientinformationen som innehåller ditt program. |

Mer information om dessa värden finns i [det här [!DNL ADLS Gen2] dokumentet](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Anslut ditt [!DNL ADLS Gen2]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL ADLS Gen2]-konto för att ansluta till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Azure Data Lake Gen2]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny ADLS Gen2-koppling.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Dialogrutan **[!UICONTROL Connect to Azure Data Lake Gen2]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL ADLS Gen2] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL ADLS Gen2]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL ADLS Gen2]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till [!DNL Platform]](../../dataflow/batch/cloud-storage.md).