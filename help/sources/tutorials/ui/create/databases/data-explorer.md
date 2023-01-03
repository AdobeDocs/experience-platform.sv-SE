---
keywords: Experience Platform;hem;populära ämnen;Azure Data Explorer;azure data explorer;data explorer;Data Explorer
solution: Experience Platform
title: Skapa en Azure Data Explorer Source-anslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Azure Data Explorer-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Skapa en [!DNL Azure Data Explorer] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL Azure Data Explorer] (nedan kallad[!DNL Data Explorer]&quot;) som använder [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Data Explorer] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Data Explorer] konto på [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `endpoint` | Slutpunkten för [!DNL Data Explorer] server. |
| `database` | Namnet på [!DNL Data Explorer] databas. |
| `tenant` | Det unika klient-ID som används för att ansluta till [!DNL Data Explorer] databas. |
| `servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till [!DNL Data Explorer] databas. |
| `servicePrincipalKey` | Den unika huvudnyckeln för tjänsten som används för att ansluta till [!DNL Data Explorer] databas. |

Mer information om hur du kommer igång finns i [this [!DNL Data Explorer] dokument](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Koppla samman [!DNL Azure Data Explorer] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Data Explorer] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL Azure Data Explorer]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny Data Explorer-koppling.

![katalog](../../../../images/tutorials/create/data-explorer/catalog.png)

The **[!UICONTROL Connect to Azure Data Explorer]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Data Explorer] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/data-explorer/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Data Explorer] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/data-explorer/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Data Explorer] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
