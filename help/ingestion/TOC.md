---
audience: user
user-guide-title: Hjälp med datainmatning i Adobe Experience Platform
breadcrumb-title: Användarhandbok om datainmatning
user-guide-description: Samla data i Experience Platform via batch- eller strömningsinmatning.
feature: Data Ingestion
role: Developer
source-git-commit: 1070c34bcd4577fcc5f0ac160196450db3aab9b0
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 17%

---


# Adobe Experience Platform datainmatning {#ingestion}

- [Översikt över datainmatning](home.md)
- Direktuppspelningsuppläsning {#streaming}
   - [Översikt](streaming-ingestion/overview.md)
   - [Kafka-kontakt](streaming-ingestion/kafka.md)
   - [Felsökning](streaming-ingestion/troubleshooting.md)
- Gruppinmatning {#batch}
   - [Komma igång med API:er för gruppinmatning](batch-ingestion/getting-started.md)
   - [API-översikt](batch-ingestion/overview.md)
   - [Utvecklarhandbok för API](batch-ingestion/api-overview.md)
   - [Partiellt batchintag](batch-ingestion/partial.md)
   - [Felsökning](batch-ingestion/troubleshooting.md)
- Tutorials {#tutorials}
   - Mappa en CSV-fil till XDM {#map-csv}
      - [Översikt](./tutorials/map-csv/overview.md)
      - [Mappa en CSV-fil till ett befintligt schema](./tutorials/map-csv/existing-schema.md)
      - [Mappa en CSV-fil med AI-genererade rekommendationer](./tutorials/map-csv/recommendations.md)
   - [Infoga batchdata med användargränssnittet](tutorials/ingest-batch-data.md)
   - [Skapa en autentiserad direktuppspelningsanslutning](tutorials/create-authenticated-streaming-connection.md)
   - [Skapa en direktuppspelningsanslutning (API)](tutorials/create-streaming-connection.md)
   - [Skapa en direktuppspelningsanslutning (UI)](tutorials/create-streaming-connection-ui.md)
   - [Direktuppspelning av postdata](tutorials/streaming-record-data.md)
   - [Strömmande tidsseriedata](tutorials/streaming-time-series-data.md)
   - [Direktuppspelning av flera meddelanden](tutorials/streaming-multiple-messages.md)
- Datakvalitet och övervakning {#quality}
   - [Översikt](quality/overview.md)
   - [Övervaka datainmatning](quality/monitor-data-ingestion.md)
   - [Hämta feldiagnostik](quality/error-diagnostics.md)
   - [Hämta misslyckade batchar](quality/retrieve-failed-batches.md)
   - [Direktinmatningsvalidering](quality/streaming-validation.md)
- [Skyddsritningar för dataöverföring](guardrails.md)
- [Source-anslutningar](source-connectors.md)
- [API-referens för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [API-referens för direktuppspelad inmatning](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Versionsinformation för plattform](https://experienceleague.adobe.com/en/docs/experience-platform/release-notes/latest)
