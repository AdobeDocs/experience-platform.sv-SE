---
keywords: Experience Platform;home;popular topics;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: Skapa en Google Big Query-källkoppling i användargränssnittet
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en Google Big Query-källkoppling (nedan kallad GBQ) med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---


# Skapa en [!DNL Google Big Query] källanslutning i användargränssnittet

>[!NOTE]
>
> Kopplingen [!DNL Google BigQuery] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Google Big Query] (nedan kallad GBQ) källkoppling med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig GBQ-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt GBQ-konto [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `project` | Projekt-ID:t för det standardprojekt [!DNL BigQuery] som frågan ska skickas till. |
| `clientID` | ID-värdet som används för att generera uppdateringstoken. |
| `clientSecret` | Det hemliga värde som används för att generera uppdateringstoken. |
| `refreshToken` | Uppdateringstoken som hämtats från [!DNL Google] som används för att auktorisera åtkomst till [!DNL BigQuery]. |

Mer information om dessa värden finns i [det här GBQ-dokumentet](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Anslut ditt GBQ-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt GBQ-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under **[!UICONTROL Databases]** kategorin **[!UICONTROL Google Big Query]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny GBQ-anslutning.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Sidan visas **[!UICONTROL Connect to Google Big Query]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina GBQ-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det GBQ-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt GBQ-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).