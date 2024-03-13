---
title: Anslut ditt Salesforce-konto med användargränssnittet i Experience Platform
description: Lär dig hur du ansluter ditt Salesforce-konto och överför dina CRM-data till Experience Platform med användargränssnittet.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: a5ecd4ab1c543805870b846cfe0fccc5474333d4
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Koppla samman [!DNL Salesforce] konto till Experience Platform med användargränssnittet

Den här självstudiekursen innehåller steg för hur du ansluter [!DNL Salesforce] ta med dina CRM-data till Adobe Experience Platform via användargränssnittet i Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en autentiserad [!DNL Salesforce] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde för CRM-data](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter {#gather-required-credentials}

För att autentisera [!DNL Salesforce] måste du ange värden som motsvarar följande [!DNL Salesforce] autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce] källinstans. |
| `username` | Användarnamnet för [!DNL Salesforce] användarkonto. |
| `password` | Lösenordet för [!DNL Salesforce] användarkonto. |
| `securityToken` | Säkerhetstoken för [!DNL Salesforce] användarkonto. |
| `apiVersion` | (Valfritt) REST API-versionen av [!DNL Salesforce] -instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52`måste du ange värdet som `52.0` Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |

Mer information om autentisering finns i [this [!DNL Salesforce] autentiseringsguide](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att ansluta [!DNL Salesforce] konto till Experience Platform.

## Koppla samman [!DNL Salesforce] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt källarbetsytan. The *[!UICONTROL Catalog]* På skärmen visas en mängd olika källor som finns i katalogen med Experience Platform-källor.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också söka efter en viss källa med sökalternativet.

Välj **[!UICONTROL CRM]** i listan över källkategorier och välj sedan **[!UICONTROL Add data]** från [!DNL Salesforce] kort.

![Källkatalogen i användargränssnittet i Experience Platform med Salesforce-källkortet markerat.](../../../../images/tutorials/create/salesforce/catalog.png)

The **[!UICONTROL Connect to Salesforce]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

>[!BEGINTABS]

>[!TAB Använd ett befintligt Salesforce-konto]

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och välj sedan det konto som du vill använda i listan som visas. När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

![En lista över autentiserade Salesforce-konton som redan finns i din organisation.](../../../../images/tutorials/create/salesforce/existing.png)

>[!TAB Skapa ett nytt Salesforce-konto]

Om du vill använda ett nytt konto väljer du **[!UICONTROL New account]** och ange namn, beskrivning och [!DNL Salesforce] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och under några sekunder kan den nya anslutningen upprättas.

![Gränssnittet där du kan skapa ett nytt Salesforce-konto genom att ange lämpliga autentiseringsuppgifter.](../../../../images/tutorials/create/salesforce/new.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL Salesforce] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/crm.md).
