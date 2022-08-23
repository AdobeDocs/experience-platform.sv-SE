---
title: Versionsinformation om Adobe Experience Platform, augusti 2022
description: Versionsinformation från augusti 2022 för Adobe Experience Platform.
source-git-commit: b8513fa214ea74eec6809796cc194466e05cbb21
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 24 augusti 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Dataprep](#data-prep)
- [Källor](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för inmatning av poster med varningar | Dataprep lokaliserar nu varningar (icke-kritiska fel) till fälten och tillåter att resten av raden importeras. Alla mappningsomformningsfel rapporteras nu som varningar och rader som är delvis inkapslade betraktas som lyckade, med en varning.  Övervakning stöds även för poster med varningar och diagnostikinformation. Det går för närvarande bara att få del av poster med varningar att strömma data. Läs dokumentationen om [importera poster med varningar](../../sources/tutorials/ui/monitor-streaming.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om [!DNL Data Prep], se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för självbetjäningskällor (batch-SDK) | Utveckla, testa och integrera REST API-baserade datakällor för att importera batchdata till Experience Platform med hjälp av lättkonfigurerade källspecifikationer. Med Sources SDK kan du: <ul><li>Konfigurera en ny källa till Experience Platform-katalogen.</li><li>Definiera specifikationer för källan, inklusive information om vilka autentiseringstyper som stöds, schemaläggning och hur resursdata hämtas.</li><li>Skapa användarinriktad dokumentation för den nya källan.</li></ul> Mer information finns i dokumentationen om [Självbetjänade källor (batch-SDK)](../../sources/sources-sdk/overview.md). |
| Allmän tillgänglighet för [!DNL Google BigQuery] källa | Använd [!DNL Google BigQuery] källa att importera data från [!DNL Google BigQuery] data warehouse till Experience Platform. Mer information finns i dokumentationen för [[!DNL Google BigQuery] källa](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] källa (beta) | Använd [!DNL Teradata Vantage] källa till import av data från hybridmiljöer med flera moln till Experience Platform. Mer information finns i dokumentationen för [[!DNL Teradata Vantage] källa](../../sources/connectors/databases/teradata-vantage.md). |
| Stöd för olika regioner för Adobe Analytics | Du kan nu importera rapportsviter från valfri region (USA, Storbritannien eller Singapore). Rapportsviterna måste mappas till samma organisation som den Experience Platform Sandbox-instans i vilken källanslutningen skapas. Mer information finns i guiden [skapa en Adobe Analytics-källanslutning i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| API-stöd för on-demand-inmatning | Använd on-demand-inmatning för att skapa ad hoc-flöden för ett givet dataflöde med [!DNL Flow Service] API. Skapade flödeskörningar måste anges som engångsintag. Mer information finns i guiden [skapa en flödeskörning för on-demand-inmatning med API](../../sources/tutorials/api/on-demand-ingestion.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om källor finns i [källöversikt](../../sources/home.md).
