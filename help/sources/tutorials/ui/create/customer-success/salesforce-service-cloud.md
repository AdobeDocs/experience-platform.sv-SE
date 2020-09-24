---
keywords: Experience Platform;home;popular topics;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Skapa en Salesforce Service Cloud-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en Salesforce Service Cloud-källkoppling (nedan kallad SSC) med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Skapa en [!DNL Salesforce Service Cloud] källanslutning i användargränssnittet

>[!NOTE]
>
>Kopplingen [!DNL Salesforce Service Cloud] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Salesforce Service Cloud] (nedan kallad SSC) källkoppling med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig SSC-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/customer-success.md)

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt SSC-konto [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `username` | Användarnamnet för användarkontot. |
| `password` | Lösenordet för användarkontot. |
| `securityToken` | Säkerhetstoken för användarkontot. |

Mer information om hur du kommer igång finns i [ [!DNL Salesforce Service Cloud] det här dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Anslut ditt [!DNL Salesforce Service Cloud] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt SSC-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under **[!UICONTROL Customer Success]** kategorin **[!UICONTROL Salesforce Service Cloud]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny SSC-anslutning.

![katalog](../../../../images/tutorials/create/ssc/catalog.png)

Sidan visas **[!UICONTROL Connect to Salesforce Service Cloud]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina SSC-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/ssc/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det SSC-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/ssc/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt SSC-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från [!DNL Platform]](../../dataflow/customer-success.md)kundens framgång.