---
title: Krypterad datainmatning
description: Lär dig hur du importerar krypterade filer via molnlagringsbatchkällor med API:t.
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: adb48b898c85561efb2d96b714ed98a0e3e4ea9b
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 0%

---

# Krypterad dataöverföring

Du kan importera krypterade datafiler till Adobe Experience Platform med hjälp av batchkällor i molnet. Med krypterad datainmatning kan ni utnyttja asymmetriska krypteringsmekanismer för att på ett säkert sätt överföra batchdata till Experience Platform. För närvarande stöds PGP och GPG för asymmetrisk kryptering.

Processen för krypterad datainmatning är följande:

1. [Skapa ett krypteringsnyckelpar med Experience Platform API:er](#create-encryption-key-pair). Krypteringsnyckelparet består av en privat nyckel och en offentlig nyckel. När du har skapat den kan du kopiera eller hämta den offentliga nyckeln, tillsammans med motsvarande offentliga nyckel-ID och förfallotid. Under den här processen kommer den privata nyckeln att lagras av Experience Platform i ett säkert valv. **OBS!** Den offentliga nyckeln i svaret är Base64-kodad och måste dekrypteras innan den används.
2. Använd den offentliga nyckeln för att kryptera den datafil som du vill importera.
3. Placera den krypterade filen i molnlagringen.
4. När den krypterade filen är klar [skapa en källanslutning och ett dataflöde för molnlagringskällan](#create-a-dataflow-for-encrypted-data). När du skapar flödet måste du ange en `encryption` och inkludera ditt offentliga nyckel-ID.
5. Experience Platform hämtar den privata nyckeln från det säkra valvet för att dekryptera data vid tidpunkten för inmatningen.

>[!IMPORTANT]
>
>Den största tillåtna storleken för en krypterad fil är 1 GB. Du kan till exempel importera 2 GB data i en enda dataflödeskörning, men en enskild fil i dessa data får inte överstiga 1 GB.

Det här dokumentet innehåller anvisningar om hur du genererar ett krypteringsnyckelpar för att kryptera dina data och importerar krypterade data till Experience Platform med hjälp av molnlagringskällor.

## Kom igång {#get-started}

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
   * [Lagringskällor i molnet](../api/collect/cloud-storage.md): Skapa ett dataflöde för att hämta batchdata från molnlagringskällan till Experience Platform.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

### Filtillägg som stöds för krypterade filer {#supported-file-extensions-for-encrypted-files}

Listan över filtillägg som stöds för krypterade filer är:

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>Krypterad filinmatning i Adobe Experience Platform Sources stöder openPGP och inte någon specifik egen version av PGP.

## Skapa krypteringsnyckelpar {#create-encryption-key-pair}

Det första steget när du ska hämta krypterade data till Experience Platform är att skapa ditt nyckelpar för kryptering genom att göra en begäran om POST till `/encryption/keys` slutpunkt för [!DNL Connectors] API.

**API-format**

```http
POST /data/foundation/connectors/encryption/keys
```

**Begäran**

+++Visa exempelbegäran

Följande begäran genererar ett krypteringsnyckelpar med PGP-krypteringsalgoritmen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `encryptionAlgorithm` | Den typ av krypteringsalgoritm som du använder. Krypteringstyperna som stöds är `PGP` och `GPG`. |
| `params.passPhrase` | Lösenfrasen ger ytterligare ett lager av skydd för dina krypteringsnycklar. När lösenordet skapas lagrar Experience Platform den i ett annat säkert valv än den offentliga nyckeln. Du måste ange en sträng som inte är tom som lösenfras. |

+++

**Svar**

+++Visa exempelsvar

Ett lyckat svar returnerar din Base64-kodade offentliga nyckel, ditt offentliga nyckel-ID och nycklarnas förfallotid. Utgångsdatumet är automatiskt 180 dagar efter datumet för nyckelgenereringen. Förfallotid kan för närvarande inte konfigureras.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `publicKey` | Den offentliga nyckeln används för att kryptera data i ditt molnlagringsutrymme. Den här nyckeln motsvarar den privata nyckel som skapades under det här steget. Men den privata nyckeln går omedelbart till Experience Platform. |
| `publicKeyId` | Det offentliga nyckel-ID:t används för att skapa ett dataflöde och importera dina krypterade molnlagringsdata till Experience Platform. |
| `expiryTime` | Utgångsdatumet anger förfallodatumet för ditt krypteringsnyckelpar. Det här datumet anges automatiskt till 180 dagar efter datumet för nyckelgenereringen och visas i ett enhetligt tidsstämpelformat. |

+++

### Hämta krypteringsnycklar {#retrieve-encryption-keys}

Om du vill hämta alla krypteringsnycklar i organisationen skickar du en GET-förfrågan till `/encryption/keys` endpoit=not.

**API-format**

```http
GET /data/foundation/connectors/encryption/keys
```

**Begäran**

+++Visa exempelbegäran

Följande begäran hämtar alla krypteringsnycklar i organisationen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Svar**

+++Visa exempelsvar

Ett lyckat svar returnerar krypteringsalgoritmen, den offentliga nyckeln, ID:t för den offentliga nyckeln och motsvarande förfallotid för nycklarna.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Hämta krypteringsnycklar med ID {#retrieve-encryption-keys-by-id}

Om du vill hämta en viss uppsättning krypteringsnycklar skickar du en GET-förfrågan till `/encryption/keys` slutpunkt och ange ditt offentliga nyckel-ID som rubrikparameter.

**API-format**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Begäran**

+++Visa exempelbegäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Svar**

+++Visa exempelsvar

Ett lyckat svar returnerar krypteringsalgoritmen, den offentliga nyckeln, ID:t för den offentliga nyckeln och motsvarande förfallotid för nycklarna.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Skapa kundstyrt nyckelpar {#create-customer-managed-key-pair}

Du kan också skapa ett nyckelpar för signaturverifiering för att signera och importera dina krypterade data.

Under den här fasen måste du generera en egen kombination av privat nyckel och offentlig nyckel och sedan använda din privata nyckel för att signera dina krypterade data. Därefter måste du koda din offentliga nyckel i Base64 och sedan dela den till Experience Platform för att Platform ska kunna verifiera din signatur.

### Dela din offentliga nyckel med Experience Platform

Om du vill dela din offentliga nyckel skickar du en POST till `/customer-keys` -slutpunkten när du anger din krypteringsalgoritm och den Base64-kodade offentliga nyckeln.

**API-format**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Begäran**

+++Visa exempelbegäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}}
    }'
```

| Parameter | Beskrivning |
| --- | --- |
| `encryptionAlgorithm` | Den typ av krypteringsalgoritm som du använder. Krypteringstyperna som stöds är `PGP` och `GPG`. |
| `publicKey` | Den offentliga nyckel som motsvarar dina kundhanterade nycklar som används för att signera din krypterade nyckel. Nyckeln måste vara Base64-kodad. |

+++

**Svar**

+++Visa exempelsvar

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Egenskap | Beskrivning |
| --- | --- |
| `publicKeyId` | Detta offentliga nyckel-ID returneras som svar på att din kundhanterade nyckel delats med Experience Platform. Du kan ange detta ID för den offentliga nyckeln som ID för signeringsverifieringsnyckel när du skapar ett dataflöde för signerade och krypterade data. |

+++

## Anslut molnlagringskällan till Experience Platform med [!DNL Flow Service] API

När du har hämtat ditt krypteringsnyckelpar kan du nu fortsätta och skapa en källanslutning för din molnlagringskälla och överföra dina krypterade data till plattformen.

Först måste du skapa en basanslutning för att autentisera källan mot plattformen. Om du vill skapa en basanslutning och autentisera källan väljer du den källa du vill använda i listan nedan:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure-fillagring](../api/create/cloud-storage/azure-file-storage.md)
* [Datallandningszon](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud-lagring](../api/create/cloud-storage/google.md)
* [Oracle Object Storage](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

När du har skapat en basanslutning måste du sedan följa de steg som beskrivs i självstudiekursen för [skapa en källanslutning för en molnlagringskälla](../api/collect/cloud-storage.md) för att skapa en källanslutning, en målanslutning och en mappning.

## Skapa ett dataflöde för krypterade data {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Du måste ha följande för att kunna skapa ett dataflöde för krypterad datainmatning:
>
>* [ID för offentlig nyckel](#create-encryption-key-pair)
>* [Källanslutnings-ID](../api/collect/cloud-storage.md#source)
>* [Målanslutnings-ID](../api/collect/cloud-storage.md#target)
>* [Mappnings-ID](../api/collect/cloud-storage.md#mapping)

Om du vill skapa ett dataflöde skickar du en POST till `/flows` slutpunkt för [!DNL Flow Service] API. Om du vill importera krypterade data måste du lägga till en `encryption` till `transformations` -egenskapen och inkludera `publicKeyId` som skapades i ett tidigare steg.

**API-format**

```http
POST /flows
```

>[!BEGINTABS]

>[!TAB Skapa ett dataflöde för krypterad datainmatning]

**Begäran**

+++Visa exempelbegäran

Följande begäran skapar ett dataflöde för att importera krypterade data för en molnlagringskälla.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `flowSpec.id` | Flödesspecifikation-ID som motsvarar molnlagringskällor. |
| `sourceConnectionIds` | Källanslutnings-ID. Detta ID representerar överföringen av data från källan till plattformen. |
| `targetConnectionIds` | Målanslutnings-ID. Detta ID representerar var data kommer att sparas när de väl kommer till plattformen. |
| `transformations[x].params.mappingId` | Mappnings-ID. |
| `transformations.name` | När du importerar krypterade filer måste du ange `Encryption` som en extra omvandlingsparameter för dataflödet. |
| `transformations[x].params.publicKeyId` | Det offentliga nyckel-ID som du skapade. Detta ID är hälften av krypteringsnyckelparet som används för att kryptera molnlagringsdata. |
| `scheduleParams.startTime` | Starttiden för dataflödet i epok-tid. |
| `scheduleParams.frequency` | Frekvensen med vilken dataflödet samlar in data. Godtagbara värden är: `once`, `minute`, `hour`, `day`, eller `week`. |
| `scheduleParams.interval` | Intervallet anger perioden mellan två på varandra följande flödeskörningar. Intervallets värde ska vara ett heltal som inte är noll. Intervall krävs inte när frekvens har angetts som `once` och ska vara större än eller lika med `15` för andra frekvensvärden. |

+++

**Svar**

+++Visa exempelsvar

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet för dina krypterade data.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB Skapa ett dataflöde för att importera krypterade och signerade data]

**Begäran**

+++Visa exempelbegäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `params.signVerificationKeyId` | Signeringsverifieringsnyckelns ID är samma som det offentliga nyckel-ID som hämtades efter att din Base64-kodade offentliga nyckel delats med Experience Platform. |

+++

**Svar**

+++Visa exempelsvar

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet för dina krypterade data.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### Ta bort krypteringsnycklar {#delete-encryption-keys}

Om du vill ta bort dina krypteringsnycklar skickar du en DELETE-begäran till `/encryption/keys` slutpunkt och ange ditt offentliga nyckel-ID som rubrikparameter.

**API-format**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Begäran**

+++Visa exempelbegäran

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

### Validera krypteringsnycklar {#validate-encryption-keys}

Gör en GET-förfrågan till `/encryption/keys/validate/` slutpunkt och ange det offentliga nyckel-ID som du vill validera som en rubrikparameter.

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**Begäran**

+++Visa exempelbegäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Svar**

Ett godkänt svar returnerar antingen en bekräftelse på att dina ID:n är giltiga eller ogiltiga.

>[!BEGINTABS]

>[!TAB Giltig]

Ett giltigt ID för offentlig nyckel returnerar statusen `Active` tillsammans med ditt offentliga nyckel-ID.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB Ogiltig]

Ett ogiltigt ID för offentlig nyckel returnerar statusen `Expired` tillsammans med ditt offentliga nyckel-ID.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## Begränsningar för återkommande intag {#restrictions-on-recurring-ingestion}

Krypterad datainmatning stöder inte inmatning av återkommande mappar eller mappar på flera nivåer i källor. Alla krypterade filer måste finnas i en enda mapp. Jokertecken med flera mappar i en enda källsökväg stöds inte heller.

Följande är ett exempel på en mappstruktur som stöds, där källsökvägen är `/ACME-customers/*.csv.gpg`.

I det här scenariot kapslas filerna i fet stil in i Experience Platform.

* ACME-kunder
   * **File1.csv.gpg**
   * File2.json.gpg
   * **File3.csv.gpg**
   * File4.json
   * **File5.csv.gpg**

Följande är ett exempel på en mappstruktur som inte stöds där källsökvägen är `/ACME-customers/*`.

I det här scenariot misslyckas flödeskörningen och returnerar ett felmeddelande som anger att data inte kan kopieras från källan.

* ACME-kunder
   * File1.csv.gpg
   * File2.json.gpg
   * Undermapp1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* ACME-lojalitet
   * File6.csv.gpg


## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett krypteringsnyckelpar för dina molnlagringsdata och ett dataflöde som du kan använda för att hämta krypterade data med [!DNL Flow Service API]. Om du vill ha statusuppdateringar om dataflödets fullständighet, fel och mätvärden läser du i guiden på [övervaka ditt dataflöde med [!DNL Flow Service] API](./monitor.md).