---
keywords: Experience Platform;hem;populära ämnen;mysql;MySQL
solution: Experience Platform
title: Skapa en MySQL-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en MySQL-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---

# Skapa en [!DNL MySQL] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL MySQL] källanslutning med Adobe Experience Platform UI.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL MySQL] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL MySQL] konto på [!DNL Platform]måste du ange följande värde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | The [!DNL MySQL] anslutningssträng som är kopplad till ditt konto. The [!DNL MySQL] anslutningssträngsmönstret är: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Du kan lära dig mer om anslutningssträngar och hur du hämtar dem genom att läsa [[!DNL MySQL] dokument](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Koppla samman [!DNL MySQL] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL MySQL] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL MySQL]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL MySQL] koppling.

![](../../../../images/tutorials/create/my-sql/catalog.png)

The **[!UICONTROL Connect to MySQL]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL MySQL] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/my-sql/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL MySQL] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt MySQL-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
