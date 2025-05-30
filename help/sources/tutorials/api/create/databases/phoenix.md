---
title: Skapa en Phoenix-basanslutning med API:t för Flow Service
description: Lär dig hur du ansluter en Phoenix-databas till Adobe Experience Platform med API:t för Flow Service.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Skapa en [!DNL Phoenix]-basanslutning med API:t [!DNL Flow Service]

>[!WARNING]
>
>[!DNL Phoenix]-källan kommer att bli inaktuell i slutet av juni 2025.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen beskrivs hur du skapar en basanslutning och ansluter ditt [!DNL Phoenix]-konto till Adobe Experience Platform med API:t för [!DNL Flow Service].

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Phoenix] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande autentiseringsuppgifter för att kunna ansluta ditt [!DNL Phoenix]-konto till Experience Platform.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för servern [!DNL Phoenix]. |
| `username` | Användarnamnet som du använder för att komma åt servern [!DNL Phoenix]. |
| `password` | Lösenordet som motsvarar användaren. |
| `port` | TCP-porten som servern [!DNL Phoenix] använder för att avlyssna klientanslutningar. Om du ansluter till [!DNL Azure HDInsights] anger du porten som 443. Om den här parametern inte anges används standardvärdet 8765. |
| `httpPath` | Den partiella URL som motsvarar servern [!DNL Phoenix]. Ange /hbasephoenix0 om du använder [!DNL Azure] HDInsights-kluster. |
| `enableSsl` | Ett booleskt värde. Anger om anslutningar till servern krypteras med SSL. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Phoenix] är: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Mer information om hur du kommer igång finns i [det här Phoenix-dokumentet](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa en basanslutning skickar du en POST-begäran till slutpunkten `/connections` och anger dina [!DNL Phoenix] autentiseringsuppgifter i begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Phoenix]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.host` | Värden för servern [!DNL Phoenix]. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Phoenix]-anslutning. |
| `auth.params.password` | Lösenordet som är kopplat till din [!DNL Phoenix]-anslutning. |
| `auth.params.port` | TCP-porten för din [!DNL Phoenix]-anslutning. |
| `auth.params.httpPath` | Den partiella http-sökvägen för din [!DNL Phoenix]-anslutning. |
| `auth.params.enableSsl` | Det booleska värdet som anger om anslutningarna till servern är krypterade med SSL. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Phoenix]: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Phoenix]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
