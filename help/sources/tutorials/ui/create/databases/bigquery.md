---
title: Skapa en Google Big Query Source Connection i användargränssnittet
description: Lär dig hur du skapar en Google Big Query-källanslutning med Adobe Experience Platform-gränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 55aaaa39659566de81bb161d704b6f8212e29a8b
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Skapa en [!DNL Google BigQuery]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL Google BigQuery] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

I den här självstudiekursen får du lära dig hur du ansluter ditt [!DNL Google BigQuery]-konto till Adobe Experience Platform med användargränssnittet.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Google BigQuery]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Google BigQuery] autentiseringsguiden](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) om du vill ha mer information om hur du samlar in dina nödvändiga inloggningsuppgifter.

## Anslut ditt Google BigQuery-konto

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Databases] väljer du **[!UICONTROL Google BigQuery]** och sedan **[!UICONTROL Add data]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Google BigQuery har valts.](../../../../images/tutorials/create/google-big-query/catalog.png)

Sidan **[!UICONTROL Connect to Google Big Query]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Google BigQuery]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Den befintliga kontosidan där en lista över befintliga konton visas.](../../../../images/tutorials/create/google-big-query/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en valfri beskrivning för det nya [!DNL Google BigQuery]-kontot.

![Det nya kontogränssnittet i källarbetsflödet.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB Använd grundläggande autentisering]

Om du vill använda grundläggande autentisering markerar du **[!UICONTROL Basic Authentication]** och anger värden för ditt [projekt, klient-ID, klienthemlighet, uppdateringstoken och (valfritt) datamängd-ID för stora resultat ](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

![Det nya kontogränssnittet där grundläggande autentisering väljs.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB Använd tjänstautentisering]

Om du vill använda tjänstautentisering markerar du **[!UICONTROL Service Authentication]** och anger värden för ditt [projekt-ID, nyckelfilsinnehåll och (valfritt) stort resultatdatauppsättnings-ID](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials). När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

![Det nya kontogränssnittet där tjänstautentisering väljs.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Google BigQuery]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).
