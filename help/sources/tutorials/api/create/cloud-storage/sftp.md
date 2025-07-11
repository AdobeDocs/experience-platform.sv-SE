---
title: Skapa en SFTP-basanslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till en SFTP-server (Secure File Transfer Protocol) med API:t för Flow Service.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Skapa en SFTP-basanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL SFTP] (Secure File Transfer Protocol) med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

>[!IMPORTANT]
>
>Du bör undvika radmatningar och radmatningar när du importerar JSON-objekt med en [!DNL SFTP]-källanslutning. Du kan undvika begränsningarna genom att använda ett enda JSON-objekt per rad och flera rader för att skapa filer.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till en [!DNL SFTP]-server med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL SFTP] autentiseringsguiden](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) om du vill ha mer information om hur du hämtar autentiseringsuppgifter.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

>[!TIP]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL SFTP]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Källan [!DNL SFTP] stöder både grundläggande autentisering och autentisering via den offentliga nyckeln för SSH. Under det här steget kan du även ange sökvägen till den undermapp som du vill ge åtkomst till.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL SFTP]-autentiseringsuppgifter som en del av parametrarna för begäran.

>[!IMPORTANT]
>
>[!DNL SFTP]-kopplingen stöder `ed25519`, `RSA` eller `DSA` OpenSSH-nyckel. Kontrollera att nyckelfilsinnehållet börjar med `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` och slutar med `"-----END [RSA/DSA] PRIVATE KEY-----"`. Om den privata nyckelfilen är en PPK-formatfil använder du PuTTY-verktyget för att konvertera från PPK till OpenSSH-format.

**API-format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

+++Begäran

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
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.port` | Porten för SFTP-servern. Det här heltalsvärdet är som standard 22. |
| `auth.params.username` | Användarnamnet som är associerat med SFTP-servern. |
| `auth.params.password` | Lösenordet som är kopplat till SFTP-servern. |
| `auth.params.maxConcurrentConnections` | Det maximala antalet samtidiga anslutningar som anges vid anslutning av Experience Platform till SFTP. När det här värdet är aktiverat måste det vara minst 1. |
| `auth.params.folderPath` | Sökvägen till mappen som du vill ge åtkomst till. |
| `auth.params.disableChunking` | Ett booleskt värde som används för att avgöra om SFTP-servern stöder chunking eller inte. |
| `connectionSpec.id` | SFTP-serveranslutningsspecifikation-ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++svar

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade anslutningen. Detta ID krävs för att utforska din SFTP-server i nästa självstudiekurs.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB SSH-autentisering med offentlig nyckel]

+++Begäran

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
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.host` | Värdnamnet för [!DNL SFTP]-servern. |
| `auth.params.port` | Porten för SFTP-servern. Det här heltalsvärdet är som standard 22. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL SFTP]-server. |
| `auth.params.privateKeyContent` | Base64-kodad privat nyckel för SSH. De OpenSSH-nyckeltyper som stöds är `ed25519`, `RSA` och `DSA`. |
| `auth.params.passPhrase` | Lösenordsfrasen eller lösenordet för att dekryptera den privata nyckeln om nyckelfilen eller nyckelinnehållet skyddas av en lösenordsfras. Om PrivateKeyContent är lösenordsskyddat måste den här parametern användas med PrivateKeyContent-innehållets lösenfras som värde. |
| `auth.params.maxConcurrentConnections` | Det maximala antalet samtidiga anslutningar som anges vid anslutning av Experience Platform till SFTP. När det här värdet är aktiverat måste det vara minst 1. |
| `auth.params.folderPath` | Sökvägen till mappen som du vill ge åtkomst till. |
| `auth.params.disableChunking` | Ett booleskt värde som används för att avgöra om SFTP-servern stöder chunking eller inte. |
| `connectionSpec.id` | ID för serveranslutningsspecifikationen [!DNL SFTP]: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++svar

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyligen skapade anslutningen. Detta ID krävs för att utforska din SFTP-server i nästa självstudiekurs.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL SFTP]-anslutning med API:t [!DNL Flow Service] och fått anslutningens unika ID-värde. Du kan använda det här anslutnings-ID:t för att [utforska molnlagring med API:t för Flow Service ](../../explore/cloud-storage.md).
