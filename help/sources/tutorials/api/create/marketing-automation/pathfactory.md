---
title: Skapa en PathFactory-basanslutning med API:t för Flow-tjänsten
description: Lär dig hur du autentiserar ditt PathFactory-konto mot Experience Platform med API:t för Flow Service.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Skapa en [!DNL PathFactory] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

Läs det här dokumentet om du vill veta mer om hur du skapar en basanslutning för [!DNL PathFactory] med [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL PathFactory] med [!DNL Flow Service] API.

### Samla in nödvändiga autentiseringsuppgifter {#gather-credentials}

För att få åtkomst till ditt PathFactory-konto på plattformen måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Användarnamn | Dina [!DNL PathFactory] användarnamn för konto. Detta är nödvändigt för att identifiera ditt konto i systemet. |
| Lösenord | Lösenordet som är kopplat till [!DNL PathFactory] konto. Säkerställ att detta skyddas för att förhindra obehörig åtkomst. |
| Domän | Domänen som är kopplad till din [!DNL PathFactory] konto. Detta avser vanligtvis den unika identifieraren i [!DNL PathFactory] URL. |
| Åtkomsttoken | En unik token som används för API-autentisering för att säkerställa säker kommunikation mellan dina system och [!DNL PathFactory]. |
| API-slutpunkter | Särskilda API-slutpunkter för dataåtkomst: Besökare, sessioner och sidvyer. Varje slutpunkt motsvarar olika datauppsättningar som du kan hämta. **Obs!** Dessa är fördefinierade av [!DNL PathFactory] och är specifika för de data som du avser att få tillgång till: <ul><li>**Slutpunkt för besökare**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Slutpunkt för sessioner**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Slutpunkt för sidvisning**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Mer information om hur du skyddar och använder dina inloggningsuppgifter och hur du hämtar och uppdaterar din åtkomsttoken finns på [[!DNL PathFactory] Support Center](https://support.pathfactory.com/categories/adobe/). Den här resursen innehåller omfattande guider om hur du hanterar dina inloggningsuppgifter och säkerställer effektiv och säker API-integrering.

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL PathFactory] autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL PathFactory]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.clientId` | Klient-ID som är kopplat till din [!DNL PathFactory] program. |
| `auth.params.clientSecret` | Klienthemligheten som är kopplad till din [!DNL PathFactory] program. |
| `connectionSpec.id` | The [!DNL PathFactory] anslutningsspecifikation-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Svar**

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL PathFactory] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att ta fram data för automatiserad marknadsföring till plattformen med [!DNL Flow Service] API](../../collect/marketing-automation.md)
