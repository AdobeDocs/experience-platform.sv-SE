---
keywords: Experience Platform;hem;populära ämnen;Greenplum;Greenplum
solution: Experience Platform
title: Skapa en anslutning till en källa för GreenPlum i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en GreenPlum-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# Skapa en [!DNL GreenPlum] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL GreenPlum] källkoppling med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL GreenPlum] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL GreenPlum] med [!DNL Flow Service] API.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till [!DNL GreenPlum] -instans. Anslutningssträngsmönstret för [!DNL GreenPlum] är `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Mer information om hur du kommer igång finns i [det här GreenPlum-dokumentet](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Koppla samman [!DNL GreenPlum] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL GreenPlum] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL GreenPlum]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL GreenPlum] koppling.

![katalog](../../../../images/tutorials/create/greenplum/catalog.png)

The **[!UICONTROL Connect to GreenPlum]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL GreenPlum] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/greenplum/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL GreenPlum] konto som du vill ansluta till och välj **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![befintlig](../../../../images/tutorials/create/greenplum/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL GreenPlum] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
