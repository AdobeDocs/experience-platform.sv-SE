---
keywords: Experience Platform;hem;populära ämnen;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: Skapa en Google Big Query Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Google Big Query-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---

# Skapa en [!DNL Google Big Query] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL Google Big Query] källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Google BigQuery] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Google BigQuery] på Platform måste du ange följande OAuth 2.0-autentiseringsvärden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `project` | Standardprojektets ID [!DNL Google BigQuery] projekt att fråga efter. |
| `clientID` | ID-värdet som används för att generera uppdateringstoken. |
| `clientSecret` | Det hemliga värde som används för att generera uppdateringstoken. |
| `refreshToken` | Uppdateringstoken som hämtats från [!DNL Google] används för att auktorisera åtkomst till [!DNL Google BigQuery]. |

Mer information om dessa värden finns i [this [!DNL Google BigQuery] dokument](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Anslut ditt Google BigQuery-konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Databases] kategori, välj **[!UICONTROL Google BigQuery]** och sedan markera **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

The **[!UICONTROL Connect to Google Big Query]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Google BigQuery] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Google BigQuery] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/google-big-query/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Google BigQuery] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).
