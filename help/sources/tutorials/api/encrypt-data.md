---
title: Krypterad datainmatning
description: Med Adobe Experience Platform kan du importera krypterade filer via batchkällor i molnet.
hide: true
hidefromtoc: true
source-git-commit: 0457784b8aa97d55882b794077aecdbd2a9a612a
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 0%

---

# Krypterad dataöverföring

Med Adobe Experience Platform kan du importera krypterade filer via batchkällor i molnet. Med krypterad datainmatning kan ni utnyttja asymmetriska krypteringsmekanismer för att på ett säkert sätt överföra batchdata till Experience Platform. För närvarande stöds PGP och GPG för asymmetrisk kryptering.

Processen för krypterad datainmatning är följande:

1. [Skapa ett krypteringsnyckelpar med Experience Platform API:er](#create-encryption-key-pair). Krypteringsnyckelparet består av en privat nyckel och en offentlig nyckel. När du har skapat den kan du kopiera eller hämta den offentliga nyckeln tillsammans med motsvarande offentliga nyckel-ID och förfallotid. Under den här processen kommer den privata nyckeln att lagras av Experience Platform i ett säkert valv.
2. Använd den offentliga nyckeln för att kryptera datafilen som du vill importera.
3. Placera den krypterade filen i molnlagringen.
4. När den krypterade filen är klar [skapa en källanslutning och ett dataflöde för molnlagringskällan](#create-a-dataflow-for-encrypted-data). När du skapar flödet måste du ange en `encryption` och inkludera ditt offentliga nyckel-ID.
5. Experience Platform hämtar den privata nyckeln från det säkra valvet för att dekryptera data vid tidpunkten för inmatningen.

Det här dokumentet innehåller anvisningar om hur du genererar ett krypteringsnyckelpar för att kryptera dina data och importerar krypterade data till Experience Platform med hjälp av molnlagringskällor.

## Komma igång

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
   * [Lagringskällor i molnet](../api/collect/cloud-storage.md): Skapa ett dataflöde för att hämta batchdata från molnlagringskällan till Experience Platform.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Skapa krypteringsnyckelpar {#create-encryption-key-pair}

Det första steget när du ska hämta krypterade data till Experience Platform är att skapa ditt nyckelpar för kryptering genom att göra en begäran om POST till `/encryption/keys` slutpunkt för [!DNL Connectors] API.

**API-format**

```http
POST /data/foundation/connectors/encryption/keys
```

**Begäran**

Följande begäran genererar ett krypteringsnyckelpar med PGP-krypteringsalgoritmen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{PASSPHRASE}"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `encryptionAlgorithm` | Den typ av krypteringsalgoritm som du använder. Krypteringstyperna som stöds är `PGP` och `GPG`. |
| `params.passPhrase` | Lösenfrasen ger ytterligare ett lager av skydd för dina krypteringsnycklar. När lösenfrasen skapas lagrar Experience Platform den i ett annat säkert valv än den offentliga nyckeln. Du måste ange en sträng som inte är tom som lösenfras. |

**Svar**

Ett lyckat svar returnerar din offentliga nyckel, ditt offentliga nyckel-ID och nycklarnas förfallotid. Utgångsdatumet är automatiskt 180 dagar efter datumet för nyckelgenereringen. Förfallotid kan för närvarande inte konfigureras.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

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
>* [ID för offentlig nyckel](#create-encryption-key-pair)
>* [Källanslutnings-ID](../api/collect/cloud-storage.md#source)
>* [Målanslutnings-ID](../api/collect/cloud-storage.md#target)
>* [Mappnings-ID](../api/collect/cloud-storage.md#mapping)


Om du vill skapa ett dataflöde skickar du en POST till `/flows` slutpunkt för [!DNL Flow Service] API. Om du vill importera krypterade data måste du lägga till en `encryption` till `transformations` -egenskapen och inkludera `publicKeyId` som skapades i ett tidigare steg.

**API-format**

```http
POST /flows
```

**Begäran**

Följande begäran skapar ett dataflöde för att importera krypterade data för en molnlagringskälla.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Customer Data",
      "description: "ACME encrypted data ingestion",
      "flowSpec": {
          "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "26b53912-1005-49f0-b539-12100559f0e2"
      ],
      "targetConnectionIds": [
        "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                  "mappingVersion": 0
              }
          },
          {
              "name": "Encryption",
              "params": {
                  "publicKeyId": 512e686e-543e-4354-bcba-e1403ddcc532
          }
  }
      ],
      "scheduleParams": {
          "startTime": "1597784298",
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

**Svar**

Ett godkänt svar returnerar ID:t (`id`) av det nya dataflödet för dina krypterade data.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett krypteringsnyckelpar för dina molnlagringsdata och ett dataflöde som du kan använda för att hämta krypterade data med [!DNL Flow Service API]. Om du vill ha statusuppdateringar om dataflödets fullständighet, fel och mätvärden läser du i guiden på [övervaka ditt dataflöde med [!DNL Flow Service] API](./monitor.md).