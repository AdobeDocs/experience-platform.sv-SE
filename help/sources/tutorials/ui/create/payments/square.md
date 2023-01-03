---
keywords: Experience Platform;hem;populära ämnen;Fyrkant;Fyrkant
title: Skapa en anslutning med kvadratiska källor i användargränssnittet
description: Lär dig hur du skapar en fast källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# Skapa en [!DNL Square] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Square] källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Square] account Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | URL:en för [!DNL Square] -instans. |
| Klient-ID | Klient-ID som är kopplat till din [!DNL Square] konto. |
| Klienthemlighet | Klienthemligheten som är kopplad till din [!DNL Square] konto. |
| Åtkomsttoken | Åtkomsttoken används för att autentisera din [!DNL Square] konto med OAuth 2.0-autentisering. Åtkomsttoken kan hämtas från [!DNL Square]. |
| Uppdatera token | Uppdateringstoken används för att generera nya åtkomsttoken när din nuvarande åtkomsttoken upphör att gälla. Uppdateringstoken kan hämtas från [!DNL Square]. |

Mer information om dessa autentiseringsuppgifter och hur du hämtar dem finns i [[!DNL Square] dokumentation om OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Square] konto till plattform.

## Koppla samman [!DNL Square] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Payments] kategori, välj **[!UICONTROL Square]** och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/square/catalog.png)

The **[!UICONTROL Connect to Square]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL Square] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/square/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och lämpliga värden för [!DNL Square] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/square/new.png)

## Nästa steg

I den här självstudiekursen har du autentiserat och skapat en källanslutning mellan [!DNL Square] konto och plattform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att överföra betalningsdata till plattformen](../../dataflow/payments.md).
