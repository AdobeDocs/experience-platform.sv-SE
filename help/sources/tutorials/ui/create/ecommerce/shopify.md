---
keywords: Experience Platform;hem;populära ämnen;förminska;förminska
solution: Experience Platform
title: Skapa en anslutning för att förminska källa i användargränssnittet
topic: översikt
type: Självstudiekurs
description: Lär dig hur du skapar en Shopify-källanslutning med Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Skapa en [!DNL Shopify]-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du skapar en [!DNL Shopify]-källkoppling med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL Shopify]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde för en eCommerce-koppling](../../dataflow/ecommerce.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Shopify]-konto på [!DNL Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Slutpunkten för [!DNL Shopify]-servern. |
| `accessToken` | Åtkomsttoken för ditt [!DNL Shopify]-användarkonto. |

Mer information om hur du kommer igång finns i det här [[!DNL Shopify] dokumentet](https://shopify.dev/concepts/about-apis/authentication).

## Anslut ditt [!DNL Shopify]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Shopify]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Shopify]** under kategorin **[!UICONTROL eCommerce]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Shopify]-koppling.

![katalog](../../../../images/tutorials/create/shopify/catalog.png)

Sidan **[!UICONTROL Connect to Shopify]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL Shopify] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/shopify/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Shopify]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/shopify/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Shopify]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta e-handelsdata till [!DNL Platform]](../../dataflow/ecommerce.md).