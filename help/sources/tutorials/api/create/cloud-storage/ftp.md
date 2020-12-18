---
keywords: Experience Platform;home;popular topics; File Transfer Protocol; file transfer protocol
solution: Experience Platform
title: Skapa en FTP-anslutning med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Experience Platform till en FTP-server (File Transfer Protocol).
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 1%

---


# Skapa en FTP-anslutning med hjälp av API:t [!DNL Flow Service]

>[!NOTE]
>
>FTP-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

I den här självstudien används API:t [!DNL Flow Service] för att vägleda dig genom stegen för att ansluta [!DNL Experience Platform] till en FTP-server (File Transfer Protocol).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en FTP-server med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till FTP måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är associerad med FTP-servern. |
| `username` | Användarnamnet med åtkomst till FTP-servern. |
| `password` | Lösenordet för FTP-servern. |

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](../../../../../tutorials/authentication.md) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per FTP-konto eftersom den kan användas för att skapa flera källanslutningar för att hämta olika data.

### Skapa en FTP-anslutning med grundläggande autentisering

Om du vill skapa en FTP-anslutning med grundläggande autentisering skickar du en POST till [!DNL Flow Service]-API:t och anger värden för anslutningens `host`, `userName` och `password`.

**API-format**

```http
POST /connections
```

**Begäran**

För att en FTP-anslutning ska kunna skapas måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikations-ID för FTP är `fb2e94c9-c031-467d-8103-6bd6e0a432f2`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nya anslutningen. Detta ID krävs för att utforska FTP-servern i nästa självstudiekurs.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en FTP-anslutning med hjälp av API:t [!DNL Flow Service] och har fått anslutningens unika ID-värde. Du kan använda det här anslutnings-ID:t för att [utforska molnlagring med API:t för Flow Service](../../explore/cloud-storage.md) eller [ingest parquet data med API:t för Flow Service](../../cloud-storage-parquet.md).
