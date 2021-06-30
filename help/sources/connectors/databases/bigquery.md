---
keywords: Experience Platform;hem;populära ämnen;BigQuery;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Google BigQuery Source Connector - översikt
topic-legacy: overview
description: Lär dig hur du ansluter Google BigQuery till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# (Beta) [!DNL Google BigQuery]-koppling

>[!NOTE]
>
>[!DNL Google BigQuery] är i betaversion. Se [Källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsdatabas. Plattformen kan ansluta till olika typer av databaser, till exempel relational, NoSQL eller data warehouse. Stöd för databasproviders är [!DNL Google BigQuery].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Förutsättningar

I följande avsnitt finns mer information om nödvändiga inställningar som krävs innan du kan skapa en [!DNL Google BigQuery]-källanslutning.

### Generera dina [!DNL Google BigQuery]-autentiseringsuppgifter

Om du vill ansluta [!DNL Google BigQuery] till plattformen måste du generera värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `project` | Projektet är en organiseringsenhet på basnivå för dina [!DNL Google Cloud]-resurser, inklusive [!DNL Google BigQuery]. |
| `clientID` | Klient-ID:t är hälften av dina [!DNL Google BigQuery] OAuth 2.0-autentiseringsuppgifter. |
| `clientSecret` | Klienthemligheten är den andra halvan av dina [!DNL Google BigQuery] OAuth 2.0-autentiseringsuppgifter. |
| `refreshToken` | Med uppdateringstoken kan du hämta nya åtkomsttoken för ditt API. Åtkomsttoken har begränsad livslängd och kan förfalla under projektets gång. Du kan använda uppdateringstoken för att autentisera och begära efterföljande åtkomsttoken för ditt projekt vid behov. |

Detaljerade instruktioner om hur du skapar OAuth 2.0-autentiseringsuppgifter för [!DNL Google] API:er finns i följande [[!DNL Google] autentiseringsguide för OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

## Anslut [!DNL Google BigQuery] till plattformen

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google BigQuery] till plattformen med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google BigQuery-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Utforska datastrukturen och innehållet i en databaskälla med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

### Använda gränssnittet

- [Skapa en Google BigQuery-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/bigquery.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
