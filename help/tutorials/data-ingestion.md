---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Självstudiekurser om dataöverföring
topic: tutorial
type: Tutorial
description: Inmatning av data inkluderar batchinmatning, direktuppspelning och förtäring med hjälp av källanslutningar.
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Infoga data i [!DNL Experience Platform]

Adobe Experience Platform sammanför data från olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe [!DNL Experience Platform Data Ingestion] representerar de flera metoder som [!DNL Platform] använder för att importera data från dessa källor, samt hur data bevaras i datasjön för användning av nedströms [!DNL Platform services]. [!DNL Data Ingestion] omfattar batchförbrukning, direktuppspelning och förtäring med hjälp av källanslutningar. Läs översikten [Datainmatning](../ingestion/home.md) om du vill veta mer eller fortsätt direkt till [källdokumentationen](../sources/home.md).

## Skapa en källanslutning i gränssnittet och API:t

Med källkopplingar kan du importera data från flera källor, där de sedan kan märkas, struktureras och förbättras med [!DNL Platform services]. Om du vill börja skapa en källkoppling läser du i översikten [källor](../sources/home.md).

## Importera batchdata

Med Adobe Experience Platform kan du enkelt importera data till [!DNL Platform] som gruppfiler. Exempel på data som ska importeras kan vara profildata från en platt fil i ett CRM-system (till exempel en Parquet-fil) eller data som överensstämmer med ett känt [!DNL Experience Data Model]-schema (XDM) i schemaregistret. Du kommer igång genom att gå till självstudiekursen [Input data into Platform](../ingestion/tutorials/ingest-batch-data.md).

## Mappa en CSV-fil till ett XDM-schema

För att kunna importera CSV-data till Adobe Experience Platform måste data mappas till ett [!DNL Experience Data Model]-schema (XDM). Följ självstudiekursen [mappa en CSV-fil till ett XDM-schema för steg som visar hur du mappar en CSV-fil till ett XDM-schema med ](../ingestion/tutorials/map-a-csv-file.md)-användargränssnittet.[!DNL Experience Platform]

## Skapa en direktuppspelningsanslutning

För att kunna starta direktuppspelning av data till [!DNL Experience Platform] måste du först begära en HTTP-slutpunkt. Du kan konfigurera den här slutpunkten för att framtvinga autentiserat beteende. Detta kan göras med hjälp av användargränssnittet [!DNL Platform] eller [!DNL Experience Platform] API:er. Om du vill veta mer kan du följa självstudiekurserna för [att skapa en direktuppspelningsanslutning med gränssnittet](../ingestion/tutorials/create-streaming-connection-ui.md) eller [skapa en direktuppspelningsanslutning med API:er](../ingestion/tutorials/create-streaming-connection.md).

## Skapa en autentiserad direktuppspelningsanslutning

Autentiserad datainsamling gör att Adobe Experience Platform-tjänster, som [!DNL Real-time Customer Profile] och [!DNL Identity], kan skilja mellan poster som kommer från betrodda källor och otillförlitliga källor. Kom igång genom att följa självstudiekursen för [att skapa en autentiserad direktuppspelningsanslutning](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Strömma post- och tidsseriedata

Med en datamängd och strömmande anslutningar på plats kan du strömma data från post- eller tidsserier till [!DNL Platform]. För att börja direktuppspela postdata följer du [dataströmmen till postdata i självstudiekursen för plattformen](../ingestion/tutorials/streaming-record-data.md). För att börja strömma tidsseriedata följer du [strömmens tidsseriedata till Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Strömma flera meddelanden i en enda HTTP-begäran

När du direktuppspelar data till Adobe Experience Platform kan det vara dyrt att ringa ett antal HTTP-anrop. I stället för att skapa 200 HTTP-begäranden med 1 kB-nyttolaster är det till exempel mycket effektivare att skapa 1 HTTP-begäran med 200 meddelanden på 1 kB vardera, med en enda nyttolast på 200 kB. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera data som skickas till [!DNL Experience Platform]. Om du vill lära dig hur du skickar flera meddelanden till [!DNL Experience Platform] inom en enskild HTTP-begäran med direktuppspelningsinmatning följer du självstudiekursen [Skicka flera meddelanden](../ingestion/tutorials/streaming-multiple-messages.md).



