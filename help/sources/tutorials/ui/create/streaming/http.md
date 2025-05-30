---
title: Skapa en HTTP API Streaming Connection med användargränssnittet
description: Den här gränssnittshandboken hjälper dig att skapa en direktuppspelningsanslutning med Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---


# Skapa en [!DNL HTTP API] direktuppspelningsanslutning med användargränssnittet

I den här självstudien beskrivs hur du skapar en direktuppspelad källanslutning med arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   - [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

## Skapa en direktuppspelningsanslutning

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

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
- **[!UICONTROL XDM compatible]:** Den här egenskapen anger om den här direktuppspelningsanslutningen kommer att skicka händelser som är kompatibla med XDM-scheman. Som standard är den här egenskapen inaktiverad.

När du är klar väljer du **[!UICONTROL Connect to source]** och sedan **[!UICONTROL Next]** för att fortsätta.

![nytt-konto](../../../../images/tutorials/create/http/new.png)

## Markera data

När du har skapat HTTP API-anslutningen visas steget **[!UICONTROL Select data]**, som ger dig ett gränssnitt för att överföra och förhandsgranska dina data.

Välj **[!UICONTROL Upload files]** om du vill överföra dina data. Du kan också dra och släppa data i [!UICONTROL Drag and drop files]-delen av gränssnittet.

![add-data](../../../../images/tutorials/create/http/add-data.png)

När dina data har överförts kan du använda den högra sidan av gränssnittet för att förhandsgranska din filhierarki. Välj **[!UICONTROL Next]** om du vill fortsätta.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappa datafält till ett XDM-schema

Steget [!UICONTROL Mapping] visas med ett gränssnitt för att mappa källdata till en Experience Platform-datauppsättning.

Källan [!DNL HTTP API] stöder inmatning av JSON-filer. JSON-filer behöver inte konfigureras manuellt om de är markerade som XDM-kompatibla. Om inte, måste du konfigurera mappningen explicit.

Välj en datauppsättning för inkommande data som ska importeras till. Du kan antingen använda en befintlig datauppsättning eller skapa en ny.

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning väljer du **[!UICONTROL New dataset]**. På formuläret som visas anger du namn, valfri beskrivning och målschema för datauppsättningen. Om du väljer ett [!DNL Profile]-aktiverat schema kan du välja om datauppsättningen också ska vara [!DNL Profile]-aktiverad.

![ny-datamängd](../../../../images/tutorials/create/http/new-dataset.png)

### Använd en befintlig datamängd

Om du vill använda en befintlig datauppsättning väljer du **[!UICONTROL Existing dataset]**. Markera den datauppsättning som du vill använda i formuläret som visas. När du har valt en datauppsättning kan du välja om datauppsättningen ska vara [!DNL Profile]-aktiverad.

![befintlig-datamängd](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappa standardfält

Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittshandboken för dataförinställningar](../../../../../data-prep/ui/mapping.md).

Välj **[!UICONTROL Add new mapping]** om du vill lägga till ett nytt källfält.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Ett nytt källfält och målfältskoppling visas. Om du vill lägga till ett nytt källfält väljer du pilikonen bredvid inmatningsfältet [!UICONTROL Select source field].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

På panelen [!UICONTROL Select attributes] kan du utforska din filhierarki och välja ett specifikt källfält att mappa till ett mål-XDM-fält. När du har valt det källfält som du vill mappa väljer du **[!UICONTROL Select]** för att fortsätta.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

När du har markerat ett källfält kan du nu identifiera rätt mål-XDM-fält att mappa till. Välj schemaikonen under målfältsavsnittet.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Fönstret [!UICONTROL Map source field to target field] visas, och du får ett gränssnitt för att utforska schemat för måldatauppsättningen. Välj det målfält som matchar källfältet och välj sedan **[!UICONTROL Select]** för att fortsätta.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

När alla källfält har mappats till rätt mål-XDM-fält väljer du **[!UICONTROL Next]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Dataflödesdetaljer

**[!UICONTROL Dataflow detail]**-steget visas. På den här sidan kan du ange information för det skapade dataflödet genom att ange ett namn och en valfri beskrivning.

Välj **[!UICONTROL Next]** när du har angett information för dataflödet.

![dataflödesdetalj](../../../../images/tutorials/create/http/dataflow-detail.png)

## Granska

Steget **[!UICONTROL Review]** visas så att du kan granska informationen om dataflödet innan det skapas. Informationen är grupperad i följande kategorier:

- **[!UICONTROL Connection]**: Visar kontonamnet, källplattformen och källnamnet.
- **[!UICONTROL Assign dataset and map fields]**: Visar måldatauppsättningen och det schema som datauppsättningen följer.

När du har bekräftat att informationen är korrekt väljer du **[!UICONTROL Finish]**.

![granskning](../../../../images/tutorials/create/http/review.png)

## Hämta URL för direktuppspelningsslutpunkt

När anslutningen har skapats visas informationssidan för källor. På den här sidan visas information om din nya anslutning, inklusive tidigare körda dataflöden, ID och URL för direktuppspelningsslutpunkt.

![slutpunkt](../../../../images/tutorials/create/http/endpoint.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en HTTP-direktuppspelningsanslutning, vilket gör att du kan använda direktuppspelningsslutpunkten för att få tillgång till olika [!DNL Data Ingestion] API:er. Instruktioner om hur du skapar en direktuppspelningsanslutning i API:t finns i [skapa en självstudiekurs för direktuppspelningsanslutning](../../../api/create/streaming/http.md).

Om du vill lära dig att strömma data till Experience Platform kan du läsa antingen självstudiekursen [om strömning av tidsseriedata](../../../../../ingestion/tutorials/streaming-time-series-data.md) eller självstudiekursen om [strömning av postdata](../../../../../ingestion/tutorials/streaming-record-data.md).
