---
title: Anslut Azure-databaser till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter Azure-databaser till Experience Platform med API:er.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 0c8ff1029beee3f58cbf536b11b40551b6f6c2ed
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Anslut [!DNL Azure Databricks] till Experience Platform med API:t [!DNL Flow Service]

>[!AVAILABILITY]
>
>* Källan [!DNL Azure Databricks] är tillgänglig i källkatalogen för användare som har köpt Real-Time CDP Ultimate.
>
>* Källan [!DNL Azure Databricks] är i betaversion. Läs [villkoren](../../../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Azure Databricks]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Läs guiden om [hur du kommer igång med Experience Platform API:er](../../../../../landing/api-guide.md) om du vill ha information om hur du kan anropa Experience Platform API:er.

### Konfigurera kravkonfiguration

Läs [[!DNL Databricks] översikten](../../../../connectors/databases/databricks.md) om du vill veta mer om de nödvändiga konfigurationer som måste slutföras innan du kan ansluta ditt konto till Experience Platform.

### Samla in nödvändiga inloggningsuppgifter

Ange värden för följande autentiseringsuppgifter för att ansluta [!DNL Databricks] till Experience Platform.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `domain` | URL-adressen till din [!DNL Databricks]-arbetsyta. Exempel: `https://adb-1234567890123456.7.azuredatabricks.net`. |
| `clusterId` | ID för ditt kluster i [!DNL Databricks]. Det här klustret måste redan vara ett befintligt kluster och bör vara ett interaktivt kluster. |
| `accessToken` | Åtkomsttoken som autentiserar ditt [!DNL Databricks]-konto. Du kan generera din åtkomsttoken med arbetsytan [!DNL Databricks]. |
| `database` | Namnet på databasen i deltasjön. |
| `connectionSpec.Id` | Anslutningens spec-ID returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningens spec-ID för [!DNL Databricks] är `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`. |

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger autentiseringsuppgifterna för ditt [!DNL Databricks]-konto.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för en [!DNL Databricks]-källa med åtkomsttokenautentisering.

+++Exempel på visningsbegäran

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.domain` | URL-adressen till din [!DNL Databricks]-arbetsyta. |
| `auth.params.clusterId` | ID för ditt kluster i [!DNL Databricks]. Klustret måste redan vara ett befintligt kluster och måste vara ett interaktivt kluster |
| `auth.params.accessToken` | Åtkomsttoken som autentiserar ditt [!DNL Databricks]-konto. |
| `auth.params.database` | Namnet på databasen i deltasjön. |
| `connectionSpec.id` | Anslutningens spec-ID [!DNL Databricks]. |

+++

**Svar**

Ett lyckat svar returnerar din nya anslutning, inklusive ditt grundläggande anslutnings-ID.

+++Visa svarsexempel

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en anslutning mellan ditt [!DNL Databricks]-konto och Experience Platform. Du kan använda ditt nyligen genererade basanslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
