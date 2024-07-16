---
keywords: Experience Platform;hem;populära ämnen;Fyrkant;Fyrkant
title: Skapa en fyrkantig Source-anslutning i användargränssnittet
description: Lär dig hur du skapar en fast källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Skapa en [!DNL Square]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Square]-källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande värden för att komma åt din [!DNL Square]-kontoplattform:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | URL:en för instansen [!DNL Square]. |
| Klient-ID | Klient-ID som är associerat med ditt [!DNL Square]-konto. |
| Klienthemlighet | Klienthemligheten som är associerad med ditt [!DNL Square]-konto. |
| Åtkomsttoken | Åtkomsttoken används för att autentisera ditt [!DNL Square]-konto med OAuth 2.0-autentisering. Åtkomsttoken kan hämtas från [!DNL Square]. |
| Uppdatera token | Uppdateringstoken används för att generera nya åtkomsttoken när din nuvarande åtkomsttoken upphör att gälla. Uppdateringstoken kan hämtas från [!DNL Square]. |

Mer information om dessa autentiseringsuppgifter och hur du hämtar dem finns i [[!DNL Square] dokumentationen om OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL Square]-konto till plattformen.

## Anslut ditt [!DNL Square]-konto

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Payments] väljer du **[!UICONTROL Square]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/square/catalog.png)

Sidan **[!UICONTROL Connect to Square]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Square]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/square/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och lämpliga värden för dina [!DNL Square]-inloggningsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![ny](../../../../images/tutorials/create/square/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du autentiserat och skapat en källanslutning mellan ditt [!DNL Square]-konto och din plattform. Du kan nu fortsätta till nästa självstudiekurs och [skapa ett dataflöde för att hämta betalningsdata till plattformen](../../dataflow/payments.md).
