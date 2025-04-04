---
title: Skapa en PathFactory-basanslutning med API:t för Flow-tjänsten
description: Lär dig hur du autentiserar ditt PathFactory-konto mot Experience Platform med API:t för Flow Service.
badge: Beta
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---

# Skapa en [!DNL PathFactory]-basanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

Läs det här dokumentet om du vill veta mer om hur du skapar en basanslutning för [!DNL PathFactory] med [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL PathFactory] med API:t [!DNL Flow Service].

### Samla in nödvändiga autentiseringsuppgifter {#gather-credentials}

För att få åtkomst till ditt PathFactory-konto på Experience Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Användarnamn | Användarnamn för ditt [!DNL PathFactory]-konto. Detta är nödvändigt för att identifiera ditt konto i systemet. |
| Lösenord | Lösenordet som är kopplat till ditt [!DNL PathFactory]-konto. Säkerställ att detta skyddas för att förhindra obehörig åtkomst. |
| Domän | Domänen som är associerad med ditt [!DNL PathFactory]-konto. Detta refererar vanligtvis till den unika identifieraren i din [!DNL PathFactory]-URL. |
| Åtkomsttoken | En unik token som används för API-autentisering för att säkerställa säker kommunikation mellan dina system och [!DNL PathFactory]. |
| API-slutpunkter | Särskilda API-slutpunkter för dataåtkomst: Besökare, sessioner och sidvyer. Varje slutpunkt motsvarar olika datauppsättningar som du kan hämta. **Obs!** Dessa är fördefinierade av [!DNL PathFactory] och är specifika för de data som du vill komma åt: <ul><li>**Slutpunkt för besökare**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Sessionsslutpunkt**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Slutpunkt för sidvyer**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Mer information om hur du skyddar och använder dina autentiseringsuppgifter, och om hur du hämtar och uppdaterar din åtkomsttoken finns på [[!DNL PathFactory] supportcentret](https://support.pathfactory.com/categories/adobe/). Den här resursen innehåller omfattande guider om hur du hanterar dina inloggningsuppgifter och säkerställer effektiv och säker API-integrering.

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skapar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL PathFactory]-autentiseringsuppgifter som en del av begärandetexten.

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
| `auth.params.clientId` | Klient-ID som är associerat med ditt [!DNL PathFactory]-program. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med ditt [!DNL PathFactory]-program. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL PathFactory]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL PathFactory]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att överföra automatiserade marknadsföringsdata till Experience Platform med  [!DNL Flow Service] API](../../collect/marketing-automation.md)
