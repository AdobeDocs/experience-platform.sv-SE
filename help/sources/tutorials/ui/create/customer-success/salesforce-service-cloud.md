---
title: Anslut ditt Salesforce Service Cloud-konto med Experience Platform användargränssnitt
description: Lär dig hur du ansluter ditt Salesforce Service Cloud-konto och överför dina kunddata till Experience Platform via användargränssnittet.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# Anslut ditt [!DNL Salesforce Service Cloud]-konto till Experience Platform med användargränssnittet

I den här självstudiekursen beskrivs hur du ansluter ditt [!DNL Salesforce Service Cloud]-konto och överför dina kunddata till Adobe Experience Platform via Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Salesforce Service Cloud]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde för att kunden ska lyckas](../../dataflow/customer-success.md)

### Samla in nödvändiga inloggningsuppgifter

Källan [!DNL Salesforce Service Cloud] stöder grundläggande autentisering och autentiseringsuppgifter för OAuth2-klient.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta ditt [!DNL Salesforce Service Cloud]-konto med grundläggande autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Miljö-URL | URL:en för [!DNL Salesforce Service Cloud]-källinstansen. |
| Användarnamn | Användarnamnet för användarkontot [!DNL Salesforce Service Cloud]. |
| Lösenord | Lösenordet för användarkontot [!DNL Salesforce Service Cloud]. |
| Säkerhetstoken | Säkerhetstoken för användarkontot [!DNL Salesforce Service Cloud]. |
| API-version | (Valfritt) REST API-versionen för den [!DNL Salesforce Service Cloud]-instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52` måste du ange värdet som `52.0`. Om fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |

Mer information om autentisering finns i [den här [!DNL Salesforce Service Cloud] autentiseringsguiden](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB Autentiseringsuppgifter för OAuth2-klient]

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta ditt [!DNL Salesforce Service Cloud]-konto med hjälp av OAuth2-klientautentiseringsuppgifter.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Miljö-URL | URL:en för [!DNL Salesforce Service Cloud]-källinstansen. |
| Klient-ID | Klient-ID används tillsammans med klienthemligheten som en del av OAuth2-autentisering. Tillsammans gör klient-ID och klienthemlighet att ditt program kan fungera för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce Service Cloud]. |
| Klienthemlighet | Klienthemligheten används tillsammans med klient-ID som en del av OAuth2-autentiseringen. Tillsammans gör klient-ID och klienthemlighet att ditt program kan fungera för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce Service Cloud]. |
| API-version | REST API-versionen för den [!DNL Salesforce Service Cloud]-instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52` måste du ange värdet som `52.0`. Om fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |

Mer information om hur du använder OAuth för [!DNL Salesforce Service Cloud] finns i [[!DNL Salesforce Service Cloud] handboken om OAuth-auktoriseringsflöden](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att ansluta ditt [!DNL Salesforce Service Cloud]-konto till Experience Platform.

## Anslut ditt [!DNL Salesforce Service Cloud]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!DNL Salesforce Service Cloud]** under kategorin *[!UICONTROL Customer success]* och välj sedan **[!UICONTROL Add data]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen i Experience Platform-gränssnittet med källkortet för Salesforce Service Cloud markerat.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

Sidan **[!UICONTROL Connect to Salesforce Service Cloud]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Använd ett befintligt konto

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och väljer sedan önskat konto i listan som visas. När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

![En lista över autentiserade Salesforce Service Cloud-konton som redan finns i din organisation.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Skapa ett nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger ett namn och en beskrivning för det nya [!DNL Salesforce Service Cloud]-kontot.

![Gränssnittet där du kan skapa ett nytt Salesforce Service Cloud-konto genom att ange lämpliga autentiseringsuppgifter.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Välj sedan den autentiseringstyp som du vill använda för ditt nya konto.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Välj **[!UICONTROL Basic authentication]** för grundläggande autentisering och ange sedan värden för följande autentiseringsuppgifter:

* Miljö-URL
* Användarnamn
* Lösenord
* API-version (valfritt)

När du är klar väljer du **[!UICONTROL Connect to source]**.

![Det grundläggande autentiseringsgränssnittet för att skapa Salesforce-konton.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB Autentiseringsuppgifter för OAuth2-klient]

För autentiseringsuppgifter för OAuth 2-klient väljer du **[!UICONTROL OAuth2 Client Credential]** och anger sedan värden för följande autentiseringsuppgifter:

* Miljö-URL
* Klient-ID
* Klienthemlighet
* API-version

När du är klar väljer du **[!UICONTROL Connect to source]**.

![OAuth-gränssnittet för att skapa Salesforce-konton.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Salesforce Service Cloud]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta Customer Success-data till Experience Platform](../../dataflow/customer-success.md).
