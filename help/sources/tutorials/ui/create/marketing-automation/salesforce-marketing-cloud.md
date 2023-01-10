---
keywords: Experience Platform;hem;populära ämnen;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Skapa en Salesforce Marketing Cloud-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Salesforce Marketing Cloud-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Skapa en [!DNL Salesforce Marketing Cloud] källanslutning i användargränssnittet

>[!NOTE]
>
> The [!DNL Salesforce Marketing Cloud] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL Salesforce Marketing Cloud] källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL Salesforce Marketing Cloud] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Salesforce Marketing Cloud] på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Programmets värdserver. Detta är ofta din underdomän. **Obs!** När du anger `host` behöver du bara ange underdomänen och inte hela URL:en. Om din värd-URL till exempel är `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`behöver du bara ange `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` som värdvärde. |
| `clientId` | Klient-ID som är kopplat till din [!DNL Salesforce Marketing Cloud] program. |
| `clientSecret` | Klienthemligheten som är kopplad till din [!DNL Salesforce Marketing Cloud] program. |

Mer information om hur du kommer igång finns i [[!DNL Salesforce Marketing Cloud] dokument](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Koppla samman [!DNL Salesforce Marketing Cloud] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Salesforce Marketing Cloud] konto till plattform.

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet för att begränsa vilka kopplingar som visas.

Under [!UICONTROL Marketing automation] kategori, välj **[!UICONTROL Salesforce Marketing Cloud]** och sedan markera **[!UICONTROL Set up]**.

![katalog](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

The **[!UICONTROL Connect to Salesforce Marketing Cloud]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Salesforce Marketing Cloud] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Salesforce Marketing Cloud] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att få in data från automatiseringssystemet för marknadsföring i plattformen](../../dataflow/marketing-automation.md).
