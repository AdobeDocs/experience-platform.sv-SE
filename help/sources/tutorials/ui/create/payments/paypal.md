---
keywords: Experience Platform;hem;populära ämnen;betalpal;PayPal
solution: Experience Platform
title: Skapa en PayPal-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en PayPal-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Skapa en [!DNL PayPal] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL PayPal] källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL PayPal] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/payments.md)

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL PayPal] account Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | URL:en för [!DNL PayPal] -instans. |
| `clientID` | Klient-ID som är kopplat till din [!DNL PayPal] program. |
| `clientSecret` | Klienthemligheten som är kopplad till din [!DNL PayPal] program. |

Mer information om hur du kommer igång finns i [[!DNL PayPal] dokument](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Koppla samman [!DNL PayPal] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL PayPal] konto till plattform.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Payments]** kategori, välj **[!UICONTROL PayPal]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL PayPal] koppling.

![katalog](../../../../images/tutorials/create/paypal/catalog.png)

The **[!UICONTROL Connect to PayPal]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL PayPal] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/paypal/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL PayPal] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/paypal/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL PayPal] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta betalningsdata till plattformen](../../dataflow/payments.md).
