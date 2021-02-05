---
keywords: Experience Platform;home;populära topics;Azure synapse Analytics;Synapse;synapse;azure synapse analytics
solution: Experience Platform
title: Skapa en Azure synapse Analytics-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en källanslutning för Azure synapse Analytics (nedan kallad Synapse) med hjälp av Adobe Experience Platform användargränssnitt.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Skapa en [!DNL Azure Synapse Analytics]-källanslutning i användargränssnittet

>[!NOTE]
>
> [!DNL Azure Synapse Analytics]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du skapar en [!DNL Azure Synapse Analytics]-källkoppling (kallas nedan &quot;[!DNL Synapse]&quot;) med hjälp av användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Synapse]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Synapse]-konto på [!DNL Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med din [!DNL Synapse]-autentisering. Anslutningssträngsmönstret [!DNL Synapse] är `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Mer information om det här värdet finns i [det här [!DNL Synapse] dokumentet](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse).

## Anslut ditt [!DNL Synapse]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Synapse]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Azure Synapse Analytics]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Synapse]-koppling.

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

Sidan **[!UICONTROL Connect to Azure Synapse Analytics]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL Synapse] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Synapse]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Synapse]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).