---
title: Anslut ditt Salesforce-tjänstmolnkonto med användargränssnittet i Experience Platform
description: Lär dig hur du ansluter ditt Salesforce Service Cloud-konto och överför dina kundframgångsuppgifter till Experience Platform via användargränssnittet.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Koppla samman [!DNL Salesforce Service Cloud] konto till Experience Platform med användargränssnittet

Den här självstudiekursen innehåller steg för hur du ansluter [!DNL Salesforce Service Cloud] ta fram data om kundframgångar för Adobe Experience Platform via användargränssnittet i Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Salesforce Service Cloud] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde för kunden](../../dataflow/customer-success.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Salesforce Service Cloud] på Experience Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce Service Cloud] källinstans. |
| `username` | Användarnamnet för [!DNL Salesforce Service Cloud] användarkonto. |
| `password` | Lösenordet för [!DNL Salesforce Service Cloud] användarkonto. |
| `securityToken` | Säkerhetstoken för [!DNL Salesforce Service Cloud] användarkonto. |
| `apiVersion` | (Valfritt) REST API-versionen av [!DNL Salesforce Service Cloud] -instans som du använder. Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |

Mer information om autentisering finns i [this [!DNL Salesforce] autentiseringsguide](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

## Koppla samman [!DNL Salesforce Service Cloud] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Salesforce] konto till Experience Platform.

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt källarbetsytan. The *[!UICONTROL Catalog]* I visas en mängd olika källor som finns i katalogen med Experience Platform-källor.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också söka efter en viss källa med sökalternativet.

Välj **[!UICONTROL Customer success]** i listan över källkategorier och välj sedan **[!UICONTROL Add data]** från [!DNL Salesforce Service Cloud] kort.

![Källkatalogen i användargränssnittet i Experience Platform med källkortet i Salesforce Service Cloud markerat.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

The **[!UICONTROL Connect to Salesforce Service Cloud]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

>[!BEGINTABS]

>[!TAB Använd ett befintligt Salesforce Service Cloud-konto]

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och välj sedan det konto som du vill använda i listan som visas. När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

![En lista över autentiserade Salesforce-konton som redan finns i din organisation.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

>[!TAB Skapa ett nytt Salesforce Service Cloud-konto]

Om du vill använda ett nytt konto väljer du **[!UICONTROL New account]** och ange namn, beskrivning och [!DNL Salesforce Service Cloud] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och under några sekunder kan den nya anslutningen upprättas.

![Gränssnittet där du kan skapa ett nytt Salesforce-konto genom att ange lämpliga autentiseringsuppgifter.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL Salesforce Service Cloud] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från kundframgångar till Experience Platform](../../dataflow/customer-success.md).
