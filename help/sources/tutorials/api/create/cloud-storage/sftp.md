---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: Skapa en SFTP-anslutning med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Experience Platform till en SFTP-server (Secure File Transfer Protocol).
translation-type: tm+mt
source-git-commit: 71653681a0f4b31319bd352202bf55fb3947a455
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---


# Skapa en SFTP-anslutning med [!DNL Flow Service] API

>[!NOTE]
>
>SFTP-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudiekursen används API:t för att vägleda dig genom stegen för att ansluta [!DNL Flow Service] [!DNL Experience Platform] till en SFTP-server (Secure File Transfer Protocol).

Om du föredrar att använda användargränssnittet i [!DNL Experience Platform]innehåller [självstudiekursen](../../../ui/create/cloud-storage/ftp-sftp.md) stegvisa instruktioner för hur du utför liknande åtgärder.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en SFTP-server med hjälp av [!DNL Flow Service] API:t.

### Samla in nödvändiga inloggningsuppgifter

För [!DNL Flow Service] att kunna ansluta till SFTP måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är associerad med SFTP-servern. |
| `username` | Användarnamnet som ger åtkomst till din SFTP-server. |
| `password` | Lösenordet för SFTP-servern. |
| `privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. SSH-filens OpenSSH-format (RSA/DSA). |
| `passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../../../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per SFTP-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

### Skapa en SFTP-anslutning med grundläggande autentisering

Om du vill skapa en SFTP-anslutning med grundläggande autentisering skickar du en POST till [!DNL Flow Service] API:t och anger värden för anslutningens `host`, `userName`och `password`.

**API-format**

```http
POST /connections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nya anslutningen. Detta ID krävs för att utforska din SFTP-server i nästa självstudiekurs.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Skapa en SFTP-anslutning med autentisering med SSH-offentlig nyckel

Om du vill skapa en SFTP-anslutning med SSH-autentisering med offentlig nyckel, skickar du en POST till [!DNL Flow Service] API:t samtidigt som du anger värden för anslutningens `host`, `userName``privateKeyContent`och `passPhrase`.

**API-format**

```http
POST /connections
```

**Begäran**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.host` | Värdnamnet för SFTP-servern. |
| `auth.params.username` | Användarnamnet som är associerat med SFTP-servern. |
| `auth.params.privateKeyContent` | Base64-kodat innehåll för privat SSH-nyckel. SSH-filens OpenSSH-format (RSA/DSA). |
| `auth.params.passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |
| `connectionSpec.id` | SFTP-serveranslutningsspecifikation-ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nya anslutningen. Detta ID krävs för att utforska din SFTP-server i nästa självstudiekurs.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en SFTP-anslutning med API:t och fått anslutningens unika ID-värde. [!DNL Flow Service] Du kan använda det här anslutnings-ID:t för att [utforska molnlagring med API:t](../../explore/cloud-storage.md) för Flow Service eller [inmatningsdata med API:t](../../cloud-storage-parquet.md)för Flow Service.
