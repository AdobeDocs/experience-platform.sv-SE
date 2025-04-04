---
keywords: Experience Platform;hem;populära ämnen;förminska;förminska
solution: Experience Platform
title: Skapa en Shopify Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Shopify-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Skapa en [!DNL Shopify]-källanslutning i användargränssnittet

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Shopify]-källkoppling med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL Shopify]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde för en eCommerce-anslutning](../../dataflow/ecommerce.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Shopify]-konto på [!DNL Experience Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Slutpunkten för [!DNL Shopify]-servern. |
| `accessToken` | Åtkomsttoken för ditt [!DNL Shopify]-användarkonto. |

Mer information om hur du kommer igång finns i det här [[!DNL Shopify] dokumentet](https://shopify.dev/concepts/about-apis/authentication).

## Anslut ditt [!DNL Shopify]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Shopify]-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Shopify]** under kategorin **[!UICONTROL eCommerce]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Shopify]-koppling.

![katalog](../../../../images/tutorials/create/shopify/catalog.png)

Sidan **[!UICONTROL Connect to Shopify]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Shopify]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![anslut](../../../../images/tutorials/create/shopify/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Shopify]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/shopify/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Shopify]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta e-handelsdata till [!DNL Experience Platform]](../../dataflow/ecommerce.md).
