---
keywords: Experience Platform;home;popular topics;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: Skapa en Google Big Query-källkoppling i användargränssnittet
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en Google Big Query-källkoppling (nedan kallad GBQ) med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: 74fbf388cf645c89f9f6d00a5ae2e59ba94041b9
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Skapa en [!DNL Google Big Query]-källkoppling i användargränssnittet

>[!NOTE]
>
> [!DNL Google BigQuery]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Google Big Query]-källkoppling (kallas nedan &quot;BigQuery&quot;) med hjälp av användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig BigQuery-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt BigQuery-konto på [!DNL Platform] måste du ange följande OAuth 2.0-autentiseringsvärden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `project` | Projekt-ID för det [!DNL BigQuery] standardprojekt som ska frågas mot. |
| `clientID` | ID-värdet som används för att generera uppdateringstoken. |
| `clientSecret` | Det hemliga värde som används för att generera uppdateringstoken. |
| `refreshToken` | Uppdateringstoken som hämtats från [!DNL Google] som används för att auktorisera åtkomst till [!DNL BigQuery]. |

Mer information om dessa värden finns i [det här BigQuery-dokumentet](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Anslut ditt Google BigQuery-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt BigQuery-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Google Big Query]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny BigQuery-koppling.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Sidan **[!UICONTROL Connect to Google Big Query]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina BigQuery-inloggningsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det BigQuery-konto som du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt GBQ-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).