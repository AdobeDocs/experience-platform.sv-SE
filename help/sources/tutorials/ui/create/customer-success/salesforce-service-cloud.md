---
keywords: Experience Platform;hem;populära ämnen;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Skapa en Salesforce Service Cloud-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en Salesforce Service Cloud-källanslutning med Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Skapa en [!DNL Salesforce Service Cloud]-källanslutning i användargränssnittet

>[!NOTE]
>
>[!DNL Salesforce Service Cloud]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Salesforce Service Cloud]-källkoppling (kallas nedan SSC) med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig SSC-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/customer-success.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt SSC-konto på [!DNL Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `username` | Användarnamnet för användarkontot. |
| `password` | Lösenordet för användarkontot. |
| `securityToken` | Säkerhetstoken för användarkontot. |

Mer information om hur du kommer igång finns i [det här [!DNL Salesforce Service Cloud] dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Anslut ditt [!DNL Salesforce Service Cloud]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt SSC-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Salesforce Service Cloud]** under kategorin **[!UICONTROL Customer Success]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny SSC-koppling.

![katalog](../../../../images/tutorials/create/ssc/catalog.png)

Sidan **[!UICONTROL Connect to Salesforce Service Cloud]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina SSC-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/ssc/connect.png)

### Befintligt konto

Om du vill ansluta till ett befintligt konto väljer du det SSC-konto som du vill ansluta till och fortsätter sedan med **[!UICONTROL Next]**.

![befintlig](../../../../images/tutorials/create/ssc/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt SSC-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data om kundens framgång till [!DNL Platform]](../../dataflow/customer-success.md).