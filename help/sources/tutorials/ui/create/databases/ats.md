---
keywords: Experience Platform;hem;populära ämnen;Azure Table Storage;azure table storage;ats;ATS
solution: Experience Platform
title: Skapa en Azure Table Storage Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Azure Table Storage-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Skapa en [!DNL Azure Table Storage]-källanslutning i användargränssnittet

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Table Storage]-källkoppling (kallas nedan ATS) med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig ATS-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande värden för att komma åt ditt ATS-konto på [!DNL Experience Platform]:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | En anslutningssträng som ska anslutas till din [!DNL Azure Table Storage]-instans. Anslutningssträngen som ska anslutas till ATS-instansen. Anslutningssträngsmönstret för ATS är `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Mer information om hur du kommer igång finns i [det här [!DNL Azure Table Storage] dokumentet](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Anslut ditt [!DNL Azure Table Storage]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt ATS-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Azure Table Storage]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny ATS-anslutning.

![katalog](../../../../images/tutorials/create/ats/catalog.png)

Sidan **[!UICONTROL Connect to Azure Table Storage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina ATS-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![anslut](../../../../images/tutorials/create/ats/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det ATS-konto som du vill ansluta till och sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ats/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt ATS-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Experience Platform]](../../dataflow/databases.md).
