---
keywords: Experience Platform;hem;populära ämnen;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Skapa en Salesforce Marketing Cloud-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en Salesforce Marketing Cloud-källanslutning med Adobe Experience Platform-gränssnittet.
source-git-commit: f196da32f67578ad1d73f3200f6050a7ddab0d88
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# Skapa en [!DNL Salesforce Marketing Cloud]-källanslutning i användargränssnittet

>[!NOTE]
>
> Källan [!DNL Salesforce Marketing Cloud] är i betaversion. Mer information om hur du använder betatecknade källor finns i [källöversikten](../../../../home.md#terms-and-conditions).

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Salesforce Marketing Cloud]-källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL Salesforce Marketing Cloud]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Salesforce Marketing Cloud]-konto på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Programmets värdserver. Detta är ofta din underdomän. |
| `clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce Marketing Cloud]-program. |

Mer information om hur du kommer igång finns i det här [[!DNL Salesforce Marketing Cloud] dokumentet](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Anslut ditt [!DNL Salesforce Marketing Cloud]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Salesforce Marketing Cloud]-konto till Platform.

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet för att begränsa vilka kopplingar som visas.

Under kategorin [!UICONTROL Marketing automation] väljer du **[!UICONTROL Salesforce Marketing Cloud]** och sedan **[!UICONTROL Set up]**.

![katalog](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Sidan **[!UICONTROL Connect to Salesforce Marketing Cloud]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL Salesforce Marketing Cloud] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Salesforce Marketing Cloud]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Salesforce Marketing Cloud]-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att få in data från automatiseringssystemet för marknadsföring i plattformen](../../dataflow/marketing-automation.md).
