---
keywords: Experience Platform;hem;populära ämnen;direktuppspelningsanslutning;skapa direktuppspelningsanslutning;ui guide;självstudiekurs;skapa en direktuppspelningsanslutning;direktuppspelningsproblem;intag;
solution: Experience Platform
title: Skapa en direktuppspelningsanslutning med användargränssnittet
topic: tutorial
type: Tutorial
description: Den här gränssnittshandboken hjälper dig att skapa en direktuppspelningsanslutning med Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
translation-type: tm+mt
source-git-commit: 3b71f1399a770e097cf75827e626d6d4e289ab77
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Skapa en direktuppspelningsanslutning med användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en direktuppspelad källanslutning med arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Skapa en direktuppspelningsanslutning

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] innehåller en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin **[!UICONTROL Streaming]** väljer du **[!UICONTROL HTTP API]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/http/catalog.png)

Sidan **[!UICONTROL Connect HTTP API account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det HTTP API-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintligt konto](../../../../images/tutorials/create/http/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]**. Ange ett kontonamn och en valfri beskrivning på indataformuläret som visas. Du får också möjlighet att ange följande konfigurationsegenskaper:

- **[!UICONTROL Authentication]:** Den här egenskapen avgör om direktuppspelningsanslutningen kräver autentisering eller inte. Autentisering säkerställer att data samlas in från betrodda källor. Om du har att göra med personligt identifierbar information (PII) ska den här egenskapen aktiveras. Som standard är den här egenskapen inaktiverad.
- **[!UICONTROL XDM compatible]:** Den här egenskapen anger om den här direktuppspelningsanslutningen ska skicka händelser som är kompatibla med XDM-scheman. Som standard är den här egenskapen inaktiverad.

När du är klar väljer du **[!UICONTROL Connect to source]** och sedan **[!UICONTROL Next]** för att fortsätta.

![nytt konto](../../../../images/tutorials/create/http/new.png)

## Markera data

När du har skapat HTTP API-anslutningen visas **[!UICONTROL Select data]**-steget, som ger dig ett gränssnitt för att överföra och förhandsgranska dina data.

Välj **[!UICONTROL Upload files]** om du vill överföra dina data. Du kan också dra och släppa data i [!UICONTROL Drag and drop files]-delen av gränssnittet.

![tilläggsdata](../../../../images/tutorials/create/http/add-data.png)

När dina data har överförts kan du använda den högra sidan av gränssnittet för att förhandsgranska din filhierarki. Välj **[!UICONTROL Next]** för att fortsätta.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappa datafält till ett XDM-schema

Steget [!UICONTROL Mapping] visas med ett gränssnitt för att mappa källdata till en plattformsdatauppsättning.

Parquet-filer måste vara XDM-kompatibla och kräver inte att du konfigurerar mappningen manuellt, medan CSV-filer kräver att du uttryckligen konfigurerar mappningen, men tillåter dig att välja vilka källdatafält som ska mappas. Om JSON-filer markeras som XDM-klagomål behöver du inte konfigurera manuellt. Om den inte är markerad som XDM-kompatibel måste du explicit konfigurera mappningen.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning väljer du **[!UICONTROL New dataset]**. På formuläret som visas anger du namn, valfri beskrivning och målschema för datauppsättningen. Om du väljer ett [!DNL Profile]-aktiverat schema kan du välja om datauppsättningen också ska vara [!DNL Profile]-aktiverad.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Använd en befintlig datauppsättning

Om du vill använda en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]**. Markera den datauppsättning som du vill använda i formuläret som visas. När du har valt en datauppsättning kan du välja om datauppsättningen ska vara [!DNL Profile]-aktiverad.

![befintlig datamängd](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappa standardfält

Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om datamappning och mappningsfunktioner finns i självstudiekursen om [mappning av CSV-data till XDM-schemafält](../../../../../ingestion/tutorials/map-a-csv-file.md).

Om du vill lägga till ett nytt källfält väljer du **[!UICONTROL Add new mapping]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Ett nytt källfält och målfältskoppling visas. Om du vill lägga till ett nytt källfält väljer du pilikonen bredvid [!UICONTROL Select source field]-inmatningsfältet.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

På panelen [!UICONTROL Select attributes] kan du utforska din filhierarki och välja ett specifikt källfält att mappa till ett mål-XDM-fält. När du har valt det källfält som du vill mappa väljer du **[!UICONTROL Select]** för att fortsätta.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

När du har markerat ett källfält kan du nu identifiera rätt mål-XDM-fält att mappa till. Välj schemaikonen under målfältsavsnittet.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Fönstret [!UICONTROL Map source field to target field] visas, vilket ger dig ett gränssnitt för att utforska schemat för måldatauppsättningen. Välj det målfält som matchar källfältet och välj sedan **[!UICONTROL Select]** för att fortsätta.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

När alla källfält har mappats till rätt mål-XDM-fält väljer du **[!UICONTROL Next]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Dataflödesdetaljer

**[!UICONTROL Dataflow detail]**-steget visas. På den här sidan kan du ange information för det skapade dataflödet genom att ange ett namn och en valfri beskrivning.

När du har angett information för dataflödet väljer du **[!UICONTROL Next]**.

![dataflöde-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Granska

**[!UICONTROL Review]**-steget visas, så att du kan granska informationen om dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

- **[!UICONTROL Connection]**: Visar kontonamnet, källplattformen och källnamnet.
- **[!UICONTROL Assign dataset and map fields]**: Visar måldatauppsättningen och det schema som datauppsättningen följer.

När du har bekräftat att informationen är korrekt väljer du **[!UICONTROL Finish]**.

![recension](../../../../images/tutorials/create/http/review.png)

## Hämta URL för direktuppspelningsslutpunkt

När anslutningen har skapats visas informationssidan för källor. På den här sidan visas information om din nya anslutning, inklusive tidigare körda dataflöden, ID och URL för direktuppspelningsslutpunkt.

![slutpunkt](../../../../images/tutorials/create/http/endpoint.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en direktuppspelad HTTP-anslutning, vilket gör att du kan använda direktuppspelningsslutpunkten för att få åtkomst till en mängd olika API:er för [!DNL Data Ingestion]. Instruktioner om hur du skapar en direktuppspelningsanslutning i API:t finns i [självstudiekursen om att skapa en direktuppspelningsanslutning](../../../api/create/streaming/http.md).

Om du vill lära dig att strömma data till plattformen kan du läsa självstudiekursen om [data från tidsserierna för direktuppspelning](../../../../../ingestion/tutorials/streaming-time-series-data.md) eller självstudiekursen om [data för direktuppspelningsposter](../../../../../ingestion/tutorials/streaming-record-data.md).
