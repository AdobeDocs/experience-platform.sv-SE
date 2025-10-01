---
title: Strömma data från Snowflake-databasen till Experience Platform med användargränssnittet
description: Lär dig hur du direktuppspelar data från en Synwoflake-databas till Experience Platform
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: 0d646136da2c508fe7ce99a15787ee15c5921a6c
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# Strömma data från din [!DNL Snowflake]-databas till Experience Platform med användargränssnittet

Läs den här vägledningen när du vill lära dig hur du direktuppspelar data från din [!DNL Snowflake]-databas till Experience Platform med hjälp av källarbetsytan i användargränssnittet.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Autentisering

Läs guiden om [nödvändig konfiguration för [!DNL Snowflake] direktuppspelningsdata](../../../../connectors/databases/snowflake-streaming.md) om du vill ha information om hur du måste slutföra innan du kan importera direktuppspelningsdata från [!DNL Snowflake] till Experience Platform.

## Använd [!DNL Snowflake Streaming]-källan för att strömma [!DNL Snowflake]-data till Experience Platform

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Databaser* väljer du **[!DNL Snowflake Streaming]** och sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor som inte har något autentiserat konto i källkatalogen visar alternativet **[!UICONTROL Set up]**. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen i Experience Platform-gränssnittet med källkortet för Snowflake Streaming markerat.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

Sidan **[!UICONTROL Connect Snowflake Streaming account]** visas. På den här sidan kan du antingen använda nya eller befintliga autentiseringsuppgifter.

### Skapa ett nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger ett namn och en valfri beskrivning för ditt konto.

![Det nya gränssnittet för att skapa konton i källarbetsflödet.](../../../../images/tutorials/create/snowflake-streaming/new.png)

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill använda [!UICONTROL Basic authentication] väljer du **[!UICONTROL Basic Authentication for Snowflake]** och anger autentiseringsuppgifter för ditt [!DNL Snowflake]-konto. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

Läs översikten [!DNL Snowflake Streaming] om du vill ha mer information om [hur du samlar in nödvändiga inloggningsuppgifter](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials).

![Det nya kontogränssnittet i källarbetsflödet med grundläggande autentisering markerat.](../../../../images/tutorials/create/snowflake-streaming/basic-auth.png)

>[!TAB KeyPair-autentisering]

Om du vill använda [!UICONTROL KeyPair authentication] väljer du **[!UICONTROL KeyPair Authentication for Snowflake]** och anger autentiseringsuppgifter för ditt [!DNL Snowflake]-konto. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

Läs översikten [!DNL Snowflake Streaming] om du vill ha mer information om [hur du samlar in nödvändiga inloggningsuppgifter](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials).

![Det nya kontogränssnittet i källarbetsflödet, autentisering med nyckelpar har valts](../../../../images/tutorials/create/snowflake-streaming/key-pair.png)

>[!ENDTABS]

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]**, markerar ditt konto i listan och väljer **[!UICONTROL Next]**.

## Markera data {#select-data}

>[!IMPORTANT]
>
>* Det måste finnas en tidsstämpelkolumn i källtabellen för att ett direktuppspelat dataflöde ska kunna skapas. Tidsstämpeln krävs för att Experience Platform ska veta när data kommer att importeras och när inkrementella data kommer att direktuppspelas. Du kan lägga till en tidsstämpelkolumn retroaktivt för en befintlig anslutning och skapa ett nytt dataflöde.
>
>* Se till att datafälten i exempelkälldatafilen är i enlighet med [!DNL Snowflake]s riktlinjer för fallupplösning för identifierare. Mer information finns i [[!DNL Snowflake] dokumentet om ID-casing](https://docs.snowflake.com/en/sql-reference/identifiers-syntax#label-identifier-casing).

[!UICONTROL Select data]-steget visas. I det här steget måste du markera de data som du vill importera till Experience Platform, konfigurera tidsstämplar och tidszoner och tillhandahålla en exempelkälldatafil för inmatning av rådata.

Använd databaskatalogen till vänster på skärmen och markera den tabell som du vill importera till Experience Platform.

Välj sedan kolumntypen för tidsstämpling för tabellen. Du kan välja mellan två typer av tidsstämpelkolumner: `TIMESTAMP_NTZ` eller `TIMESTAMP_LTZ`. Om du väljer kolumntypen `TIMESTAMP_NTZ` måste du också ange en tidszon. Kolumnerna ska ha en begränsning som inte är null. Mer information finns i avsnittet [Begränsningar och vanliga frågor](../../../../connectors/databases/snowflake-streaming.md#limitations-and-frequently-asked-questions).

Du kan också konfigurera inställningar för bakgrundsfyllning under det här steget. Backfill avgör vilka data som hämtas från början. Om bakåtfyllning är aktiverad, kommer alla aktuella filer i den angivna sökvägen att importeras under det första schemalagda intaget. Om så inte är fallet importeras endast de filer som läses in mellan den första importkörningen och starttiden. Filer som lästs in före starttiden importeras inte.

Markera växlingsknappen **[!UICONTROL Backfill]** om du vill aktivera bakåtfyllning.

![Konfigurationsstegen för tidsstämpel, tidszon och bakgrundsfyllning.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Välj slutligen **[!UICONTROL Choose file]** om du vill överföra exempelkälldata för att skapa mappningsuppsättningen, som används i ett senare steg för att mappa originaldata till Experience Data Model (XDM).

När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

![Förhandsgranskningen av källans exempeldata.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Ange information om datauppsättning och dataflöde {#provide-dataset-and-dataflow-details}

Därefter måste du ange information om datauppsättningen och dataflödet.

### Information om datauppsättning {#dataset-details}

En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Data som har inhämtats till Experience Platform lagras i datasjön som datauppsättningar. Under det här steget kan du skapa en ny datauppsättning eller använda en befintlig datauppsättning.

Om du har en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]** och använder sedan alternativet **[!UICONTROL Advanced search]** för att visa ett fönster med alla datauppsättningar i organisationen, inklusive deras respektive information, t.ex. om de har aktiverats för inmatning i kundprofilen i realtid.

![Det befintliga gränssnittet för val av datauppsättning.](../../../../images/tutorials/create/snowflake-streaming/dataset.png)

Om du vill använda en ny datauppsättning väljer du **[!UICONTROL New dataset]** och anger sedan ett namn och en valfri beskrivning för datauppsättningen. Du måste också välja ett XDM-schema (Experience Data Model) som datauppsättningen följer.

| Ny datauppsättningsinformation | Beskrivning |
| --- | --- |
| Namn på utdatauppsättning | Namnet på den nya datauppsättningen. |
| Beskrivning | (Valfritt) En kort översikt över den nya datauppsättningen. |
| Schema | En listruta med scheman som finns i organisationen. Du kan också skapa ett eget schema före källkonfigurationsprocessen. Mer information finns i guiden om att [skapa ett XDM-schema i användargränssnittet](../../../../../xdm/tutorials/create-schema-ui.md). |

### Information om dataflöde {#dataflow-details}

När datauppsättningen har konfigurerats måste du ange information om dataflödet, inklusive ett namn, en valfri beskrivning och aviseringskonfigurationer.

![Konfigurationssteget för dataflödesinformation.](../../../../images/tutorials/create/snowflake-streaming/dataflow-detail.png)

| Dataflödeskonfigurationer | Beskrivning |
| --- | --- |
| Dataflödesnamn | Dataflödets namn.  Som standard används namnet på filen som importeras. |
| Beskrivning | (Valfritt) En kort beskrivning av dataflödet. |
| Aviseringar | Experience Platform kan skapa händelsebaserade aviseringar som användare kan prenumerera på. Dessa alternativ kräver ett öppet dataflöde för att utlösa dem. Mer information finns i [varningsöversikten](../../alerts.md) <ul><li>**Källdataflödeskörning Start**: Välj den här aviseringen för att få ett meddelande när dataflödeskörningen börjar.</li><li>**Källdataflödet har körts**: Välj den här aviseringen om du vill få ett meddelande om dataflödet slutar utan fel.</li><li>**Körningsfel för källdataflöde**: Välj den här aviseringen för att få ett meddelande om dataflödet avslutas med fel.</li></ul> |

När du är klar väljer du **[!UICONTROL Next]** för att fortsätta.

## Mappa fält till ett XDM-schema {#mapping}

[!UICONTROL Mapping]-steget visas. Använd mappningsgränssnittet för att mappa källdata till rätt schemafält innan du importerar dessa data till Experience Platform och välj sedan **[!UICONTROL Next]**. En utförlig guide om hur du använder mappningsgränssnittet finns i [Användargränssnittshandboken för dataförberedelser](../../../../../data-prep/ui/mapping.md) för mer information.

![Mappningsgränssnittet för källarbetsflödet.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Granska ditt dataflöde {#review}

Det sista steget i processen för att skapa dataflöde är att granska dataflödet innan det körs. Använd steget **[!UICONTROL Review]** om du vill granska informationen om det nya dataflödet innan det körs. Detaljerna är grupperade i följande kategorier:

* **Anslutning**: Visar källtypen, den relevanta sökvägen för den valda källfilen och antalet kolumner i källfilen.
* **Tilldela datauppsättnings- och mappningsfält**: Visar vilka datauppsättningar som källdata importeras till, inklusive det schema som datauppsättningen följer.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och tillåt en tid innan dataflödet skapas.

![Granskningssteget för källarbetsflödet.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för direktuppspelning för [!DNL Snowflake] data. Mer information finns i dokumentationen nedan.

### Övervaka dataflödet

När dataflödet har skapats kan du övervaka de data som hämtas genom det för att visa information om hur mycket data som har importerats, hur bra de är och vilka fel som har uppstått. Mer information om hur du övervakar direktuppspelade dataflöden finns i självstudiekursen [Övervaka direktuppspelade dataflöden i användargränssnittet](../../monitor-streaming.md).

### Uppdatera ditt dataflöde

Om du vill uppdatera konfigurationer för schemaläggning, mappning och allmän information för dina dataflöden går du till självstudiekursen [Uppdatera källornas dataflöden i användargränssnittet](../../update-dataflows.md).

### Ta bort ditt dataflöde

Du kan ta bort dataflöden som inte längre är nödvändiga eller som har skapats felaktigt med funktionen **[!UICONTROL Delete]** som finns på arbetsytan i **[!UICONTROL Dataflows]**. Mer information om hur du tar bort dataflöden finns i självstudiekursen [Ta bort dataflöden i användargränssnittet](../../delete.md).
