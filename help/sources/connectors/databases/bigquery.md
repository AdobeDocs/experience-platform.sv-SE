---
title: Google BigQuery Source Connector - översikt
description: Lär dig hur du ansluter Google BigQuery till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# [!DNL Google BigQuery]-källa

>[!IMPORTANT]
>
>Källan [!DNL Google BigQuery] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Läs det här dokumentet om du behöver utföra nödvändiga steg för att kunna ansluta ditt [!DNL Google BigQuery]-konto till Experience Platform.

## Förhandskrav {#prerequisites}

I följande avsnitt finns mer information om nödvändiga inställningar som krävs innan du kan skapa en [!DNL Google BigQuery]-källanslutning.

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

### Generera dina [!DNL Google BigQuery]-autentiseringsuppgifter {#credentials}

Om du vill ansluta [!DNL Google BigQuery] till Experience Platform måste du generera värden för följande autentiseringsuppgifter:

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Ange lämpliga värden för följande autentiseringsuppgifter för att autentisera med en kombination av OAuth 2.0 och grundläggande autentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `project` | Projektet är organisationsenhet på basnivå för dina [!DNL Google Cloud]-resurser, inklusive [!DNL Google BigQuery]. |
| `clientID` | Klient-ID är hälften av dina [!DNL Google BigQuery] OAuth 2.0-autentiseringsuppgifter. |
| `clientSecret` | Klienthemligheten är den andra halvan av dina [!DNL Google BigQuery] OAuth 2.0-autentiseringsuppgifter. |
| `refreshToken` | Med uppdateringstoken kan du hämta nya åtkomsttoken för ditt API. Åtkomsttoken har begränsad livslängd och kan förfalla under projektets gång. Du kan använda uppdateringstoken för att autentisera och begära efterföljande åtkomsttoken för ditt projekt vid behov. |
| `largeResultsDataSetId` | (Valfritt) Det förskapade [!DNL Google BigQuery]-datauppsättnings-ID som krävs för att aktivera stöd för stora resultatuppsättningar. |

Detaljerade instruktioner om hur du genererar OAuth 2.0-autentiseringsuppgifter för [!DNL Google] API:er finns i följande [[!DNL Google] autentiseringsguide för OAuth 2.0](https://developers.google.com/identity/protocols/oauth2).

>[!TAB Tjänstautentisering]

Om du vill autentisera med tjänstautentisering anger du lämpliga värden för följande autentiseringsuppgifter.

**Obs!**: Ditt tjänstkonto måste ha tillräcklig behörighet, till exempel: **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** och **[!DNL BigQuery Data Owner]** för att autentiseras med tjänstautentisering.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `projectId` | ID:t för [!DNL Google BigQuery] som du vill fråga mot. |
| `keyFileContent` | Nyckelfilen som används för att autentisera tjänstkontot. Du kan hämta det här värdet från [[!DNL Google Cloud service accounts] instrumentpanelen](https://console.cloud.google.com). Nyckelfilens innehåll är i JSON-format. Du måste koda detta i [!DNL Base64] när du autentiserar till Experience Platform. |
| `largeResultsDataSetId` | (Valfritt) Det förskapade [!DNL Google BigQuery]-datauppsättnings-ID som krävs för att aktivera stöd för stora resultatuppsättningar. |

Mer information om hur du använder tjänstkonton i [!DNL Google BigQuery] finns i handboken [Använda tjänstkonton i  [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts).

>[!ENDTABS]

## Anslut [!DNL Google BigQuery] till plattformen

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google BigQuery] till plattformen med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google BigQuery-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

### Använda gränssnittet

- [Skapa en Google BigQuery-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/bigquery.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
