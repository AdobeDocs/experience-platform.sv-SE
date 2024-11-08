---
keywords: Experience Platform;hem;populära ämnen;betalpal;PayPal
solution: Experience Platform
title: Skapa en PayPal Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en PayPal-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Skapa en [!DNL PayPal]-källanslutning i användargränssnittet

>[!WARNING]
>
>[!DNL PayPal]-källan kommer att bli inaktuell i slutet av maj 2025.

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL PayPal]-källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL PayPal]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/payments.md)

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande värden för att komma åt din [!DNL PayPal]-kontoplattform:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | URL:en för instansen [!DNL PayPal]. |
| `clientID` | Klient-ID som är associerat med ditt [!DNL PayPal]-program. |
| `clientSecret` | Klienthemligheten som är associerad med ditt [!DNL PayPal]-program. |

Mer information om hur du kommer igång finns i [[!DNL PayPal] dokumentet](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Anslut ditt [!DNL PayPal]-konto

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL PayPal]-konto till plattformen.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL PayPal]** under kategorin **[!UICONTROL Payments]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL PayPal]-koppling.

![katalog](../../../../images/tutorials/create/paypal/catalog.png)

Sidan **[!UICONTROL Connect to PayPal]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL PayPal]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![anslut](../../../../images/tutorials/create/paypal/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL PayPal]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/paypal/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL PayPal]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta betalningsdata till plattformen](../../dataflow/payments.md).
