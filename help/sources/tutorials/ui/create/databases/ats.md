---
keywords: Experience Platform;hem;populära ämnen;Azure Table Storage;azure table storage;ats;ATS
solution: Experience Platform
title: Skapa en Azure Table Storage Source-anslutning i gränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Azure Table Storage-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# Skapa en [!DNL Azure Table Storage] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL Azure Table Storage] (nedan kallad ATS) källkontakt som använder [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig ATS-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt ATS-konto på [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | En anslutningssträng att ansluta till [!DNL Azure Table Storage] -instans. Anslutningssträngen som ska anslutas till ATS-instansen. Anslutningssträngsmönstret för ATS är `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Mer information om hur du kommer igång finns i [this [!DNL Azure Table Storage] dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Koppla samman [!DNL Azure Table Storage] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt ATS-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL Azure Table Storage]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny ATS-kontakt.

![katalog](../../../../images/tutorials/create/ats/catalog.png)

The **[!UICONTROL Connect to Azure Table Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina ATS-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/ats/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det ATS-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ats/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt ATS-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
