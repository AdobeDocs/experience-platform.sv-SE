---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Självstudiekurser om dataöverföring
topic: tutorial
translation-type: tm+mt
source-git-commit: 2020f4b88f81f2d4fe3cfbd91cd18119ae580f4f

---


# Importera data till Experience Platform

Adobe Experience Platform samlar data från flera olika källor för att hjälpa marknadsförarna att bättre förstå kundernas beteende. Adobe Experience Platforms datainmatning representerar de olika metoder som Platform använder för att hämta data från dessa källor samt hur dessa data lagras i Data Lake för användning av plattformstjänster längre fram i kedjan. Inmatning av data inkluderar batchinmatning, direktuppspelning och förtäring med hjälp av källanslutningar. Om du vill veta mer kan du läsa översikten över [](../ingestion/home.md) datainmatning eller gå direkt till [källdokumentationen](../source-connectors/home.md).

## Skapa en källanslutning i gränssnittet och API:t

Med källkopplingar kan du importera data från flera källor, där de sedan kan märkas, struktureras och förbättras med hjälp av plattformstjänster. Om du vill börja skapa en koppling med hjälp av användargränssnittet går du till [Skapa en källkoppling i översikten](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/sources-ui-tutorial.md)för användargränssnittet. Om du vill skapa källanslutningar med API:t går du till [Skapa en källanslutning med API-översikten](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)för Flow Service.

## Importera batchdata

Med Adobe Experience Platform kan ni enkelt importera data till plattformen som gruppfiler. Exempel på data som ska importeras kan vara profildata från en platt fil i ett CRM-system (t.ex. en parquet-fil) eller data som överensstämmer med ett känt XDM-schema (Experience Data Model) i schemaregistret. Kom igång genom att gå till [självstudiekursen](../ingestion/tutorials/ingest-batch-data.md)om att få tillgång till information om intag.

## Mappa en CSV-fil till ett XDM-schema

För att kunna importera CSV-data till Adobe Experience Platform måste data mappas till ett XDM-schema (Experience Data Model). Om du vill se steg som visar hur du mappar en CSV-fil till ett XDM-schema med användargränssnittet i Experience Platform följer du [mappningen av en CSV-fil till en självstudiekurs](../ingestion/tutorials/map-a-csv-file.md)för XDM-schemat.

## Skapa en direktuppspelningsanslutning

För att kunna starta direktuppspelning av data på Experience Platform måste du först skapa en direktuppspelad HTTP-anslutning. När du skapar en direktuppspelningsanslutning måste du ange nyckeldetaljer som till exempel källan för direktuppspelningsdata och om du tänker skicka data från en tillförlitlig (autentiserad) eller en otillförlitlig (ej autentiserad) källa eller inte. Detta kan göras med hjälp av användargränssnittet för plattformen eller API:erna för Experience Platform. Om du vill veta mer kan du följa självstudiekurserna för att [skapa en direktuppspelningsanslutning med användargränssnittet](../ingestion/tutorials/create-streaming-connection-ui.md) eller [skapa en direktuppspelningsanslutning med API:er](../ingestion/tutorials/create-streaming-connection.md).

## Skapa en autentiserad direktuppspelningsanslutning

Autentiserad datainsamling gör att Adobe Experience Platform-tjänster, som kundprofil och identitet i realtid, kan skilja mellan poster som kommer från betrodda källor och icke-betrodda källor. Kom igång genom att följa självstudiekursen för att [skapa en autentiserad direktuppspelningsanslutning](../ingestion/tutorials/create-authenticated-streaming-connection.md).

## Strömma post- och tidsseriedata

Med en datamängd och strömmande anslutningar på plats kan du strömma data från post- eller tidsserier till plattformen. Följ [dataströmmens postdata i självstudiekursen](../ingestion/tutorials/streaming-record-data.md)om du vill börja direktuppspela postdata. För att börja strömma tidsseriedata följer du [strömmens tidsseriedata till Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Strömma flera meddelanden i en enda HTTP-begäran

När du direktuppspelar data på Adobe Experience Platform kan det vara dyrt att göra ett antal HTTP-anrop. I stället för att skapa 200 HTTP-begäranden med 1 kB-nyttolaster är det till exempel mycket effektivare att skapa 1 HTTP-begäran med 200 meddelanden på 1 kB vardera, med en enda nyttolast på 200 kB. När det används på rätt sätt är gruppering av flera meddelanden i en enda begäran ett utmärkt sätt att optimera data som skickas till Experience Platform. Om du vill lära dig hur du skickar flera meddelanden till Experience Platform inom en enda HTTP-begäran med direktuppspelningsuppläsning följer du självstudiekursen [om att](../ingestion/tutorials/streaming-multiple-messages.md)skicka flera meddelanden.



