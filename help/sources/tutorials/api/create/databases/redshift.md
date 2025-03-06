---
title: Anslut AWS Redshift till Experience Platform med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till AWS Redshift med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: dd9aee1ac887637d4761188d6dbcf55ad5bde407
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Anslut [!DNL AWS Redshift] till Experience Platform med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>Källan [!DNL AWS Redshift] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs den här vägledningen när du vill veta hur du kan ansluta ditt [!DNL AWS Redshift]-källkonto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Anslut [!DNL AWS Redshift] till Experience Platform på Azure {#azure}

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL AWS Redshift]-källa till Experience Platform på Azure.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL AWS Redshift] måste du ange följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| `server` | Servernamnet för [!DNL AWS Redshift] -instansen. |
| `port` | Den TCP-port som en [!DNL AWS Redshift] -server använder för att avlyssna klientanslutningar. |
| `username` | Användarnamnet som är associerat med ditt [!DNL AWS Redshift] -konto. |
| `password` | Lösenordet som motsvarar användarkontot. |
| `database` | Den [!DNL AWS Redshift] -databas från vilken data ska hämtas. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL AWS Redshift] är `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Mer information om hur du kommer igång finns i det här [[!DNL AWS Redshift] dokumentet](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Skapa en basanslutning för [!DNL AWS Redshift] på Experience Platform på Azure [#azure-base ]

>[!NOTE]
>
>Standardkodningsstandarden för [!DNL Redshift] är Unicode. Detta kan inte ändras.

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL AWS Redshift]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

+++Markera för att visa exempel

Följande begäran skapar en basanslutning för [!DNL AWS Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.server` | Servernamnet för din [!DNL AWS Redshift]-instans. |
| `auth.params.port` | TCP-porten som en [!DNL AWS Redshift]-server använder för att avlyssna klientanslutningar. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL AWS Redshift]-konto. |
| `auth.params.password` | Lösenordet som motsvarar användarkontot. |
| `auth.params.database` | Databasen [!DNL AWS Redshift] från vilken data ska hämtas. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL AWS Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Svar**

+++Markera för att visa exempel

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## Anslut [!DNL AWS Redshift] till Experience Platform på AWS webbtjänster (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på AWS Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL AWS Redshift]-källa till Experience Platform på AWS.

### Skapa en basanslutning för [!DNL AWS Redshift] på Experience Platform på AWS {#aws-base}

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL AWS Redshift]:

+++Markera för att visa exempel

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.server` | Servernamnet för din [!DNL AWS Redshift]-instans. |
| `auth.params.port` | TCP-porten som en [!DNL AWS Redshift]-server använder för att avlyssna klientanslutningar. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL AWS Redshift]-konto. |
| `auth.params.password` | Lösenordet som motsvarar användarkontot. |
| `auth.params.database` | Databasen [!DNL AWS Redshift] från vilken data ska hämtas. |
| `auth.params.schema` | Namnet på schemat som är associerat med din [!DNL AWS Redshift]-databas. Du måste se till att användaren som du vill ge databasåtkomst till också har åtkomst till det här schemat. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL AWS Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska ditt lagringsutrymme i nästa självstudiekurs.

+++Markera för att visa exempel

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL AWS Redshift]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/database-nosql.md)
