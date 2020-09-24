---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser om dataöverföring
topic: tutorial
type: Tutorial
description: Inmatning av data inkluderar batchinmatning, direktuppspelning och förtäring med hjälp av källanslutningar.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Infoga data i [!DNL Experience Platform]

Adobe Experience Platform sammanför data från olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe [!DNL Experience Platform Data Ingestion] representerar de olika metoder som används för att [!DNL Platform] importera data från dessa källor, samt hur dessa data bevaras i datasjön för användning i senare led [!DNL Platform services]. [!DNL Data Ingestion] omfattar batchförbrukning, direktuppspelning och förtäring med hjälp av källanslutningar. Om du vill veta mer kan du läsa översikten över [](../ingestion/home.md) datainmatning eller gå direkt till [källdokumentationen](../sources/home.md).

## Skapa en källanslutning i gränssnittet och API:t

Med källkopplingar kan du importera data från flera källor, där de sedan kan märkas, struktureras och förbättras med [!DNL Platform services]. Information om hur du börjar skapa en källkoppling finns i [Källöversikt](../sources/home.md).

## Importera batchdata

Med Adobe Experience Platform kan du enkelt importera data till [!DNL Platform] som gruppfiler. Exempel på data som ska importeras kan vara profildata från en platt fil i ett CRM-system (till exempel en parquet-fil) eller data som överensstämmer med ett känt [!DNL Experience Data Model] (XDM) schema i schemaregistret. Kom igång genom att gå till [självstudiekursen](../ingestion/tutorials/ingest-batch-data.md)om att få tillgång till information om intag i plattformen.

## Mappa en CSV-fil till ett XDM-schema

För att kunna importera CSV-data till Adobe Experience Platform måste data mappas till ett [!DNL Experience Data Model] (XDM) schema. Om du vill se steg som visar hur du mappar en CSV-fil till ett XDM-schema med [!DNL Experience Platform] användargränssnittet följer du [mappningen av en CSV-fil till en självstudiekurs](../ingestion/tutorials/map-a-csv-file.md)för XDM-schema.

## Skapa en direktuppspelningsanslutning

För att kunna starta direktuppspelning av data till [!DNL Experience Platform]måste du först begära en HTTP-slutpunkt. Du kan konfigurera den här slutpunkten för att framtvinga autentiserat beteende. Detta kan göras med [!DNL Platform] användargränssnittet eller API: [!DNL Experience Platform] er. Om du vill veta mer kan du följa självstudiekurserna för att [skapa en direktuppspelningsanslutning med användargränssnittet](../ingestion/tutorials/create-streaming-connection-ui.md) eller [skapa en direktuppspelningsanslutning med API:er](../ingestion/tutorials/create-streaming-connection.md).

## Skapa en autentiserad direktuppspelningsanslutning

Autentiserad datainsamling gör det möjligt för Adobe Experience Platform-tjänster, som [!DNL Real-time Customer Profile] och [!DNL Identity], att skilja mellan poster som kommer från betrodda källor och otillförlitliga källor. Kom igång genom att följa självstudiekursen för att [skapa en autentiserad direktuppspelningsanslutning](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Strömma post- och tidsseriedata

Med en datamängd och strömmande anslutningar på plats kan du strömma data från post- eller tidsserier till [!DNL Platform]. Följ [dataströmmens postdata i självstudiekursen](../ingestion/tutorials/streaming-record-data.md)om du vill börja direktuppspela postdata. För att börja strömma tidsseriedata följer du [strömmens tidsseriedata till Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Strömma flera meddelanden i en enda HTTP-begäran

När du direktuppspelar data till Adobe Experience Platform kan det vara dyrt att ringa ett antal HTTP-anrop. I stället för att skapa 200 HTTP-begäranden med 1 kB-nyttolaster är det till exempel mycket effektivare att skapa 1 HTTP-begäran med 200 meddelanden på 1 kB vardera, med en enda nyttolast på 200 kB. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera data som skickas till [!DNL Experience Platform]. Om du vill lära dig hur du skickar flera meddelanden till [!DNL Experience Platform] en enda HTTP-begäran med direktuppspelning, ska du följa självstudiekursen [om att](../ingestion/tutorials/streaming-multiple-messages.md)skicka flera meddelanden.



