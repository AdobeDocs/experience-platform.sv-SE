---
keywords: Experience Platform;hem;populära ämnen;hubspot;Hubspot
solution: Experience Platform
title: Skapa en HubSpot-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en HubSpot-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# Skapa en [!DNL HubSpot] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL HubSpot] källkoppling med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL HubSpot] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL HubSpot] konto på [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `clientId` | Klient-ID som är kopplat till din [!DNL HubSpot] program. |
| `clientSecret` | Klienthemligheten som är kopplad till din [!DNL HubSpot] program. |
| `accessToken` | Åtkomsttoken som fås när din OAuth-integration autentiseras initialt. |
| `refreshToken` | Den uppdateringstoken som erhölls när OAuth-integreringen autentiserades initialt. |

Mer information om hur du kommer igång finns i [[!DNL HubSpot] dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Koppla samman [!DNL HubSpot] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL HubSpot] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Marketing automation]** kategori, välj **[!UICONTROL HubSpot]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL HubSpot] koppling.

![katalog](../../../../images/tutorials/create/hubspot/catalog.png)

The **[!UICONTROL Connect to HubSpot]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL HubSpot] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/hubspot/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL HubSpot] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/hubspot/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL HubSpot] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att få in data från automatiserade marknadsföringssystem i [!DNL Platform]](../../dataflow/marketing-automation.md).
