---
title: Anslut Capillary till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter Capillary till Experience Platform med API:er.
hide: true
hidefromtoc: true
source-git-commit: 7119ca51e0a4db09c8adb68bcde41ab3837439d1
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# Anslut [!DNL Capillary Streaming Events] till Experience Platform med API:t [!DNL Flow Service]

Läs den här vägledningen när du vill lära dig hur du använder [!DNL Capillary Streaming Events] och [[!DNL Flow Service]  API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) för att strömma data från ditt [!DNL Capillary]-konto till Adobe Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Capillary Streaming Events] översikten](../../../../connectors/loyalty/capillary.md) om du vill ha information om autentisering.

### Använda Experience Platform API:er

Läs guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md) om du vill ha information om hur du kan anropa Experience Platform API:er.

>[!BEGINSHADEBOX]

## Checklista för utvecklarprocess

1. Skapa eller välj **XDM-schemat (Experience Data Model)** som mål med schemaregistret. Använd det här XDM-schemat för att **skapa en datauppsättning** i katalogtjänsten.
2. Skapa en **basanslutning** för att lagra dina [!DNL Capillary]-autentiseringsuppgifter.
3. Skapa en **källanslutning** som kan bindas till din `baseConnectionId`.
4. Skapa en **målanslutning** för att se till att dina data hamnar i datasjön.
5. Använd Data Prep för att skapa mappningar som mappar [!DNL Capillary]-källfälten till rätt XDM-fält.
6. Skapa ett dataflöde med din `sourceConnectionId`, `targetConnectionId` och `mappingID`
7. Testa med en enda exempelprofil-/transaktionshändelse för att verifiera dataflödet.

>[!ENDSHADEBOX]

## Skapa en basanslutning {#base-connection}

En basanslutning behåller autentiseringsuppgifter och anslutningsinformation. Om du vill skapa en basanslutning för [!DNL Capillary] gör du en POST-begäran till `/connections`-slutpunkten för [!DNL Flow Service] API:t och anger dina [!DNL Capillary]-autentiseringsuppgifter i begärandetexten.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Capillary]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**Svar**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Skapa en källanslutning

Om du vill skapa en källanslutning skickar du en POST-begäran till slutpunkten `/sourceConnections` samtidigt som du anger ditt grundläggande anslutnings-ID.

**API-format**

```http
POST /flowservice/sourceConnections
```

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med detaljerad information om den nyligen skapade källanslutningen, inklusive dess unika identifierare (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### Schemakonfigurationer

>[!BEGINTABS]

>[!TAB Inläsning av profil]

Profiler innehåller attribut för identitet och lojalitet. Visa följande nyttolast för ett exempel baserat på profilschemat [!DNL Capillary]. Du kan konfigurera och mappa det här schemat till en enskild XDM-profil.

**Begäran**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**Svar**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB Inmatning av transaktion]

Transaktioner fångar upp handelsaktiviteter. Visa följande nyttolast för ett exempel baserat på händelseschemat för [!DNL Capillary]. Du kan konfigurera och mappa det här schemat till en XDM Experience Event.

**Begäran**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**Svar**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

### Händelser som stöds

[!DNL Capillary]-källan stöder följande händelser:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`


### Historisk datamigrering

Ni kan föra in era historiska lojalitets- och transaktionsdata i Experience Platform. Exportera bara dina data som strukturerade CSV-filer från [!DNL Capillary], överför dem säkert med [!DNL SFTP] och importera dem till dina Experience Platform-datauppsättningar. Efter den inledande migreringen är dina data uppdaterade i realtid via den händelsestyrda anslutningen.

### Skapa ett mål-XDM-schema {#target-schema}

Ett XDM-schema (Experience Data Model) är ett standardiserat sätt att organisera och beskriva kundupplevelsedata i Experience Platform. Om du vill importera källdata till Experience Platform måste du först skapa ett mål-XDM-schema som definierar strukturen och datatyperna som du vill importera. Det här schemat fungerar som en plan för den Experience Platform-datauppsättning där dina inmatade data finns.

Ett mål-XDM-schema kan skapas genom att en POST-begäran till [schemats register-API ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) utförs. Mer information om hur du skapar ett XDM-målschema finns i följande guider:

* [Skapa ett schema med API:t ](../../../../../xdm/api/schemas.md).
* [Skapa ett schema med användargränssnittet](../../../../../xdm/tutorials/create-schema-ui.md).

När du har skapat målschemat `$id` kommer det att krävas senare för måldatauppsättningen och målmappningen.

## Skapa en måldatauppsättning {#target-dataset}

En datamängd är en lagrings- och hanteringskonstruktion för en datamängd som vanligtvis är strukturerad som en tabell med kolumner (schema) och rader (fält). Data som har importerats till Experience Platform lagras i datasjön som datauppsättningar. Under det här steget kan du antingen skapa en ny datauppsättning eller använda en befintlig.

Du kan skapa en måldatamängd genom att göra en POST-begäran till [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), samtidigt som du anger målschemats ID i nyttolasten. Detaljerade steg om hur du skapar en måldatauppsättning finns i guiden om att [skapa en datauppsättning med API:t](../../../../../catalog/api/create-dataset.md).


## Skapa en målanslutning {#target}

En målanslutning representerar anslutningen till målet där inkapslade data kommer in. Om du vill skapa en målanslutning måste du ange det fasta ID för anslutningsspecifikation som är associerat med datasjön. Detta anslutningsspecifikations-ID är: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API-format**

```http
POST /targetConnections
```

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### Skapa en mappning {#mapping}

Mappa sedan källdata till målschemat som måldatauppsättningen följer. Skapa en mappning genom att göra en POST-begäran till `mappingSets`-slutpunkten för [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Inkludera ditt mål-XDM-schema-ID och information om de mappningsuppsättningar som du vill skapa.

Mappa de kapillära fälten till motsvarande XDM-schemafält enligt följande:

| Source-schema | Målschema |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email` |
| `loyalty.points` | `xdm:loyaltyPoints` |
| `loyalty.tier` | `xdm:loyaltyTier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

### Skapa ett dataflöde {#flow}

När du har skapat källanslutningen, mappningen och målanslutningen kan du konfigurera ett dataflöde för att flytta data från [!DNL Capillary] till Experience Platform.

Vanliga dataflöden är:

* **Profildataflöde**: Infogar [!DNL Capillary] profildata i en enskild XDM-profildatauppsättning.
* **Transaktionsdataflöde**: Ingerar [!DNL Capillary] transaktionsdata till en XDM ExperienceEvent-datauppsättning.

**Begäran**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime` är i UNIX epooch sekunder.

**Svar**

Ett lyckat svar returnerar ditt dataflöde med dess motsvarande dataflödes-ID.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## Felhantering

Kopplingen innehåller robust felhantering för följande scenarier:

* **Autentiseringsfel**: Uppdaterar automatiskt Adobe-autentiseringsuppgifter när autentiseringen misslyckas.
* **Hastighetsbegränsningsfel**: Implementerar återförsök med exponentiell säkerhetskopiering när API-hastighetsgränserna nås.
* **Nätverksfel**: Loggar och försök igen misslyckades med nätverksbegäranden.
* **Dataverifieringsfel**: Loggar ogiltiga nyttolaster för manuell granskning och lösning.

Alla fel loggas med information som feltyp, tidsstämpel, nyttolast för begäran och Adobe API-svar för att underlätta felsökning och felsökning.

## Testa anslutningen

Följ stegen nedan för att lära dig hur du testar anslutningen:

* Gör en GET-begäran till `/connections/{BASE_CONNECTION_ID}` och ange ditt grundläggande anslutnings-ID för att verifiera att din basanslutning finns. Under det här steget kan du även verifiera att statusen för din basanslutning är inställd på `active`.
* Gör en GET-begäran till `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}` och ange ditt källanslutnings-ID för att verifiera din källanslutning.
* Använd din URL för direktuppspelningsslutpunkt för att skicka en exempelprofil-nyttolast (använd JSON för profilinmatning).
* Navigera till datauppsättningen i Experience Platform UI och kör en fråga på datauppsättningen för att bekräfta dina poster.
* Använd dataprep-loggarna för att kontrollera om det finns fel.
* Om du måste öppna en supportanmälan måste du ha följande:
   * Begär nyttolast
   * Svarstext
   * Request-id
   * tidsstämpel
   * Resurs-ID.

## Bilaga

Mer information om ytterligare åtgärder finns i följande dokumentation

* [Övervaka dataflöden](../../../../../dataflows/ui/monitor-sources.md)
* [Uppdatera dataflöden](../../../ui/update-dataflows.md)
* [Ta bort dataflöden](../../../ui/delete.md)
* [Uppdatera källkonto](../../../ui/update.md)
