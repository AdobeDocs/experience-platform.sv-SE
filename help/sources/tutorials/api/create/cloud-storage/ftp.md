---
keywords: Experience Platform;hem;populära ämnen; filöverföringsprotokoll; filöverföringsprotokoll
solution: Experience Platform
title: Skapa en FTP-basanslutning med API:t för Flow Service
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till en FTP-server (File Transfer Protocol) med API:t för Flow Service.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# Skapa en FTP-basanslutning med [!DNL Flow Service] API

>[!NOTE]
>
>FTP-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL FTP] (File Transfer Protocol) med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en [!DNL FTP] servern som använder [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att ansluta till [!DNL FTP]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är kopplad till din [!DNL FTP] server. |
| `username` | Användarnamnet med åtkomst till dina [!DNL FTP] server. |
| `password` | Lösenordet för [!DNL FTP] server. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL FTP] är: `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL FTP] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.host` | FTP-serverns värdnamn. |
| `auth.params.username` | Användarnamnet som är associerat med FTP-servern. |
| `auth.params.password` | Lösenordet som är kopplat till FTP-servern. |
| `connectionSpec.id` | Anslutningsspecifikation-ID för FTP-server: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nya anslutningen. Detta ID krävs för att utforska FTP-servern i nästa självstudie.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en FTP-anslutning med [!DNL Flow Service] API, och har fått anslutningens unika ID-värde. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för Flow Service](../../explore/cloud-storage.md).
