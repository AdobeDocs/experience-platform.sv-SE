---
title: Google BigQuery Source Connector - översikt
description: Lär dig hur du ansluter Google BigQuery till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# [!DNL Google BigQuery]-källa

>[!IMPORTANT]
>
>Källan [!DNL Google BigQuery] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs det här dokumentet för nödvändiga steg som du måste slutföra för att kunna ansluta ditt [!DNL Google BigQuery]-konto till Adobe Experience Platform på antingen Azure eller Amazon Web Services (AWS).

## Förhandskrav {#prerequisites}

I följande avsnitt finns information om den nödvändiga konfiguration som du måste slutföra innan du kan ansluta ditt [!DNL Google BigQuery]-konto till Experience Platform.

### IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform på antingen Azure eller Amazon Web Services (AWS). Mer information finns i guiden [tillåtslista IP-adresser för att ansluta till Experience Platform på Azure och AWS](../../ip-address-allow-list.md).

### Autentisera till Experience Platform på Azure {#azure}

Du måste ange följande autentiseringsuppgifter för att ansluta ditt [!DNL Google BigQuery]-konto till Experience Platform på Azure.

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

### Autentisera till Experience Platform på AWS {#aws}

Du måste ange följande autentiseringsuppgifter för att kunna ansluta ditt [!DNL Google BigQuery]-konto till Experience Platform på AWS.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `projectId` | ID:t för [!DNL Google BigQuery] som du vill fråga mot. |
| `keyFileContent` | Nyckelfilen som används för att autentisera tjänstkontot. Du kan hämta det här värdet från [[!DNL Google Cloud service accounts] instrumentpanelen](https://console.cloud.google.com). Nyckelfilens innehåll är i JSON-format. Du måste koda detta i [!DNL Base64] när du autentiserar till Experience Platform. |
| `datasetId` | Datauppsättnings-ID:t [!DNL Google BigQuery]. Detta ID representerar var datatabellerna finns. |

## Anslut [!DNL Google BigQuery] till Experience Platform

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google BigQuery] till Experience Platform med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google BigQuery-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/bigquery.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

### Använda gränssnittet

- [Skapa en Google BigQuery-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/bigquery.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
