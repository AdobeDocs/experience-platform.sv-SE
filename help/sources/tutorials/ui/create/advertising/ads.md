---
title: Skapa en Google Ads Source Connection i användargränssnittet
description: Lär dig hur du skapar en Google Ads-källanslutning med Adobe Experience Platform användargränssnitt.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Skapa en Google Ads-källanslutning i användargränssnittet

>[!WARNING]
>
>The [!DNL Google Ads] källan är inte tillgänglig för tillfället. Adobe arbetar med att lösa problem med den här källan.

>[!NOTE]
>
>Google Ads-källan är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

I den här självstudiekursen beskrivs hur du skapar en Google Ads-källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig Google Ads-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/advertising.md)

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till din Google Ads-kontoplattform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Kund-ID för kund | Klientens kund-ID är det kontonummer som motsvarar det Google Ads-klientkonto som du vill hantera med API:t för Google Ads. Detta ID följer mallen för `123-456-7890`. |
| ID för inloggningskund | Kund-ID för inloggning är det kontonummer som motsvarar ditt Google Ads Manager-konto och används för att hämta rapportdata från en viss kund. Mer information om användar-ID för inloggningskund finns i [API-dokumentation för Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| Utvecklartoken | Med utvecklartoken får du tillgång till Google Ads API. Du kan använda samma utvecklartoken för att göra förfrågningar mot alla dina Google Ads-konton. Hämta din utvecklartoken från [logga in på ditt chefskonto](https://ads.google.com/home/tools/manager-accounts/) och sedan navigera till sidan API Center. |
| Uppdatera token | Uppdateringstoken är en del av [!DNL OAuth2] autentisering. Med denna token kan du återskapa dina åtkomsttoken när de har upphört att gälla. |
| Klient-ID | Klient-ID används tillsammans med klienthemligheten som en del av [!DNL OAuth2] autentisering. Tillsammans gör klient-ID och klienthemlighet det möjligt för programmet att agera för ditt kontos räkning genom att identifiera ditt program för Google. |
| Klienthemlighet | Klienthemligheten används tillsammans med klient-ID som en del av [!DNL OAuth2] autentisering. Tillsammans gör klient-ID och klienthemlighet det möjligt för programmet att agera för ditt kontos räkning genom att identifiera ditt program för Google. |

Läs API-översiktsdokumentet för [mer information om hur du kommer igång med Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Anslut ditt Google Ads-konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Advertising]** kategori, välj **[!UICONTROL Google Ads]** och sedan markera **[!UICONTROL Add data]**.

![Källkatalogen i användargränssnittet i Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

The **[!UICONTROL Connect to Google Ads]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det Google Ads-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Urvalssidan för befintliga konton i källarbetsflödet.](../../../../images/tutorials/create/ads/existing.png).

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina Google Ads-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet i källarbetsflödet.](../../../../images/tutorials/create/ads/new.png).

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Google Ads-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta annonsdata till plattformen](../../dataflow/advertising.md).
