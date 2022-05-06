---
keywords: Experience Platform;hem;populära ämnen;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Skapa en SFTP-basanslutning med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till en SFTP-server (Secure File Transfer Protocol) med API:t för Flow Service.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---

# Skapa en SFTP-basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL SFTP] (Secure File Transfer Protocol) med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

>[!IMPORTANT]
>
>Du bör undvika radmatningar och radmatningar när du importerar JSON-objekt med en [!DNL SFTP] källanslutning. Du kan undvika begränsningarna genom att använda ett enda JSON-objekt per rad och flera rader för att skapa filer.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en [!DNL SFTP] servern som använder [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att ansluta till [!DNL SFTP]måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är kopplad till din [!DNL SFTP] server. |
| `port` | Den SFTP-serverport som du ansluter till. Om det inte anges används standardvärdet `22`. |
| `username` | Användarnamnet med åtkomst till [!DNL SFTP] server. |
| `password` | Lösenordet för [!DNL SFTP] server. |
| `privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. Typen av OpenSSH-nyckel måste klassificeras som antingen RSA eller DSA. |
| `passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om `privateKeyContent` är lösenordsskyddad, måste den här parametern användas med den privata nyckelinnehållets lösenfras som värde. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL SFTP] är: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL SFTP] autentiseringsuppgifter som en del av parametrarna för begäran.

### Skapa en [!DNL SFTP] basanslutning med grundläggande autentisering

Skapa en [!DNL SFTP] basanslutning med grundläggande autentisering, gör en POST-förfrågan till [!DNL Flow Service] API när du anger värden för anslutningen `host`, `userName`och `password`.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL SFTP] med grundläggande autentisering:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.host` | Värdnamnet för SFTP-servern. |
| `auth.params.username` | Användarnamnet som är associerat med SFTP-servern. |
| `auth.params.password` | Lösenordet som är kopplat till SFTP-servern. |
| `connectionSpec.id` | SFTP-serveranslutningsspecifikation-ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nya anslutningen. Detta ID krävs för att utforska din SFTP-server i nästa självstudiekurs.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Skapa en [!DNL SFTP] basanslutning med autentisering med SSH offentlig nyckel

Skapa en [!DNL SFTP] basanslutning med SSH-autentisering med offentlig nyckel, gör en POST till [!DNL Flow Service] API när du anger värden för anslutningen `host`, `userName`, `privateKeyContent`och `passPhrase`.

>[!IMPORTANT]
>
>The [!DNL SFTP] -anslutningen stöder en RSA- eller DSA-typ av OpenSSH-nyckel. Se till att nyckelfilens innehåll börjar med `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` och slutar med `"-----END [RSA/DSA] PRIVATE KEY-----"`. Om den privata nyckelfilen är en PPK-formatfil använder du PuTTY-verktyget för att konvertera från PPK till OpenSSH-format.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL SFTP] med SSH-autentisering med offentlig nyckel:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.host` | Värdnamnet för din [!DNL SFTP] server. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL SFTP] server. |
| `auth.params.privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. Typen av OpenSSH-nyckel måste klassificeras som antingen RSA eller DSA. |
| `auth.params.passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |
| `connectionSpec.id` | The [!DNL SFTP] serveranslutningsspecifikation-ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Svar**

Ett godkänt svar returnerar den unika identifieraren (`id`) för den nya anslutningen. Detta ID krävs för att du ska kunna utforska [!DNL SFTP] i nästa självstudiekurs.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL SFTP] anslutning med [!DNL Flow Service] API, och har fått anslutningens unika ID-värde. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för Flow Service](../../explore/cloud-storage.md).
