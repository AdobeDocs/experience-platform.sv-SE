---
keywords: Experience Platform;home;populära topics;Google AdWords;Google AdWords source connector;google adwords connector
solution: Experience Platform
title: Skapa en Google AdWords-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Google AdWords-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Skapa en [!DNL Google AdWords]-källanslutning i användargränssnittet

>[!NOTE]
>
>[!DNL Google AdWords]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du skapar en [!DNL Google AdWords]-källkoppling med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Google AdWords]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/payments.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Google AdWords]-konto [!DNL Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `clientCustomerId` | Kundens ID för [!DNL AdWords]-kontot. |
| `developerToken` | Utvecklartoken som är associerad med hanterarkontot. |
| `refreshToken` | Uppdateringstoken som hämtats från [!DNL Google] för auktorisering av åtkomst till [!DNL AdWords]. |
| `clientId` | Klient-ID:t för [!DNL Google]-programmet som används för att hämta uppdateringstoken. |
| `clientSecret` | Klienthemligheten för [!DNL Google]-programmet som används för att hämta uppdateringstoken. |

Mer information om hur du kommer igång finns i det här [[!DNL Google AdWords] dokumentet](https://developers.google.com/adwords/api/docs/guides/authentication).

## Anslut ditt [!DNL Google AdWords]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Google AdWords]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Google AdWords]** under kategorin **[!UICONTROL Advertising]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Google AdWords]-koppling.

![katalog](../../../../images/tutorials/create/ads/catalog.png)

Sidan **[!UICONTROL Connect to Google AdWords]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL Google AdWords] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/ads/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Google AdWords]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ads/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Google AdWords]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta annonsdata till [!DNL Platform]](../../dataflow/advertising.md).
