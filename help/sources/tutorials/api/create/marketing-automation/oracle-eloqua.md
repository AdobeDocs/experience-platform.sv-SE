---
title: Skapa en Oracle Eloqua-basanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till Oracle Eloqua med API:t för Flow Service.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Skapa en [!DNL Oracle Eloqua]-basanslutning med API:t [!DNL Flow Service]

>[!WARNING]
>
>[!DNL Oracle Eloqua]-källan kommer att bli inaktuell i januari 2026. En ny källa kommer att släppas senare i år som ett alternativ. När den nya källan har släppts måste du planera migreringen till den nya källan genom att skapa nya kontoanslutningar och dataflöden före utgången av januari 2026.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Oracle Eloqua] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Oracle Eloqua] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Oracle Eloqua] måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `endpoint` | Slutpunkten för [!DNL Oracle Eloqua]. |
| `username` | Användarnamnet för ditt [!DNL Oracle Eloqua]-konto. Användarnamnet måste vara formaterat som `siteName + \\ + username`, där `siteName` är det företagsnamn som du använde för att logga in på [!DNL Oracle Eloqua] och `username` är ditt användarnamn. Ditt inloggningsnamn kan till exempel vara: `adobe\\emily`. |
| `password` | Lösenordet som motsvarar ditt [!DNL Oracle Eloqua]-användarnamn. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Värdet för anslutningsspecifikations-ID:t för källan [!DNL Oracle Eloqua] är fast som: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Mer information om autentiseringsuppgifter för [!DNL Oracle Eloqua] finns i [[!DNL Oracle Eloqua] handboken om autentisering](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Oracle Eloqua]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på din [!DNL Oracle Eloqua]-basanslutning. Du bör ange ett beskrivande namn eftersom du kan använda det här värdet för att leta upp din basanslutning. |
| `description` | (Valfritt) En egenskap som du kan ta med för att ge ytterligare information om din basanslutning. |
| `auth.specName` | Autentiseringstypen som används för anslutningen. |
| `auth.params.endpoint` | Slutpunkten för [!DNL Oracle Eloqua]-servern. |
| `auth.params.username` | Den sammanfogade autentiseringsuppgiften som innehåller platsnamnet och användarnamnet som motsvarar ditt [!DNL Oracle Eloqua]-konto. |
| `auth.params.password` | Lösenordet som motsvarar ditt [!DNL Oracle Eloqua]-konto. |
| `connectionSpec.id` | Värdet för anslutningsspecifikations-ID:t för källan [!DNL Oracle Eloqua] är fast som: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Oracle Eloqua]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att överföra automatiserade marknadsföringsdata till Experience Platform med  [!DNL Flow Service] API](../../collect/marketing-automation.md)
