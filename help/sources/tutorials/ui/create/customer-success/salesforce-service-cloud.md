---
keywords: Experience Platform;hem;populära ämnen;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Skapa en Salesforce Service Cloud-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Salesforce Service Cloud-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Skapa en [!DNL Salesforce Service Cloud] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL Salesforce Service Cloud] (nedan kallad SSC)-källkontakt med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig SSC-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen på [konfigurera ett dataflöde](../../dataflow/customer-success.md)

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt SSC-konto på [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `username` | Användarnamnet för användarkontot. |
| `password` | Lösenordet för användarkontot. |
| `securityToken` | Säkerhetstoken för användarkontot. |

Mer information om hur du kommer igång finns i [this [!DNL Salesforce Service Cloud] dokument](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Koppla samman [!DNL Salesforce Service Cloud] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt SSC-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Customer Success]** kategori, välj **[!UICONTROL Salesforce Service Cloud]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny SSC-anslutning.

![katalog](../../../../images/tutorials/create/ssc/catalog.png)

The **[!UICONTROL Connect to Salesforce Service Cloud]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina SSC-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/ssc/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det SSC-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ssc/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt SSC-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta Customer Success-data till [!DNL Platform]](../../dataflow/customer-success.md).
