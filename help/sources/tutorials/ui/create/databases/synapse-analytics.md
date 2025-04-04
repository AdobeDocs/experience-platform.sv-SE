---
title: Skapa en Azure Synapse Analytics Source Connection i användargränssnittet
description: Lär dig hur du skapar en källanslutning för Azure Synapse Analytics (nedan kallad Synapse) med hjälp av Adobe Experience Platform användargränssnitt.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Skapa en [!DNL Azure Synapse Analytics]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL Azure Synapse Analytics] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Synapse Analytics]-källkoppling (kallas nedan [!DNL Synapse]) med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Synapse]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Synapse]-konto på [!DNL Experience Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med din [!DNL Synapse]-autentisering. Anslutningssträngsmönstret [!DNL Synapse] är `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Mer information om det här värdet finns i [det här [!DNL Synapse] dokumentet](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse).

## Anslut ditt [!DNL Synapse]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Synapse]-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Azure Synapse Analytics]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Synapse]-koppling.

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

Sidan **[!UICONTROL Connect to Azure Synapse Analytics]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Synapse]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Synapse]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Synapse]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Experience Platform]](../../dataflow/databases.md).
