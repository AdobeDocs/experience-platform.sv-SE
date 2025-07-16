---
title: API-slutpunkt för externa målgrupper
description: Lär dig hur du använder API:t för externa målgrupper för att skapa, uppdatera, aktivera och ta bort externa målgrupper från Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '2312'
ht-degree: 1%

---


# Extern målgruppsslutpunkt

Med externa målgrupper kan du överföra profildata från externa källor till Adobe Experience Platform. Du kan använda slutpunkten `/external-audience` i segmenteringstjänstens API för att importera en extern målgrupp till Experience Platform, visa information och uppdatera externa målgrupper samt ta bort externa målgrupper.

## Komma igång

>[!IMPORTANT]
>
>Slutpunkterna i den här guiden har prefixet `/core/ais` i motsats till `/core/ups`.

För att du ska kunna använda Experience Platform API:er måste du ha slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Experience Platform API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver ett huvud som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådor](../../sandboxes/home.md).

## Skapa externa målgrupper {#create-audience}

Du kan skapa en extern målgrupp genom att göra en POST-begäran till slutpunkten `/external-audience/`.

**API-format**

```http
POST /external-audience/
```

**Begäran**

+++ Ett exempel på en förfrågan om att skapa en extern publik.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `name` | Sträng | Namnet på den externa publiken. |
| `description` | Sträng | En valfri beskrivning för den externa målgruppen. |
| `customAudienceId` | Sträng | En valfri identifierare för den externa målgruppen. |
| `fields` | Array med objekt | Listan med fält och deras datatyper. När du skapar fältlistan kan du lägga till följande objekt: <ul><li>`name`: **Obligatoriskt** Namnet på fältet som är en del av den externa målgruppsspecifikationen.</li><li>`type`: **Obligatoriskt** Den typ av data som placeras i fältet. Värden som stöds är `string`, `number`, `long`, `integer`, `date` (`2025-05-13`), `datetime` (`2025-05-23T20:19:00+00:00`) och `boolean`.</li>`identityNs`: **Krävs för identitetsfält** Det namnutrymme som används av identitetsfältet. Värden som stöds innehåller alla giltiga namnutrymmen, till exempel `ECID` eller `email`.li><li>`labels`: *Valfritt* En array med åtkomstkontrolletiketter för fältet. Mer information om tillgängliga etiketter för åtkomstkontroll finns i [etikettordlistan för dataanvändning](/help/data-governance/labels/reference.md). </li></ul> |
| `sourceSpec` | Objekt | Ett objekt som innehåller information om var den externa målgruppen finns. När du använder det här objektet **måste** innehålla följande information: <ul><li>`path`: **Obligatoriskt**: Platsen för den externa målgruppen eller mappen som innehåller den externa målgruppen i källan.</li><li>`type`: **Obligatoriskt** Den typ av objekt som du hämtar från källan. Värdet kan vara `file` eller `folder`.</li><li>`sourceType`: *Valfritt* Den typ av källa som du hämtar från. För närvarande är det enda värdet som stöds `Cloud Storage`.</li><li>`cloudType`: *Valfritt* Typen av molnlagring, baserat på källtypen. Värden som stöds är `S3`, `DLZ`, `GCS` och `SFTP`.</li><li>`baseConnectionId`: ID:t för basanslutningen och tillhandahålls av din källleverantör. Det här värdet är **obligatoriskt** om `cloudType`-värdet `S3`, `GCS` eller `SFTP` används. Mer information finns i översikten över [källanslutningar](../../sources/home.md)li></ul> |
| `ttlInDays` | Heltal | Datan upphör att gälla för den externa målgruppen, i dagar. Värdet kan anges från 1 till 90. Som standard är utgångsdatumet för data inställt på 30 dagar. |
| `audienceType` | Sträng | Målgruppstypen för den externa målgruppen. För närvarande stöds bara `people`. |
| `originName` | Sträng | **Obligatorisk** Målgruppens ursprung. Det är här som publiken kommer ifrån. För externa målgrupper bör du använda `CUSTOM_UPLOAD`. |
| `namespace` | Sträng | Namnutrymmet för målgruppen. Som standard är det här värdet inställt på `CustomerAudienceUpload`. |
| `labels` | Array med strängar | De etiketter för åtkomstkontroll som gäller för den externa målgruppen. Mer information om tillgängliga etiketter för åtkomstkontroll finns i [etikettordlistan för dataanvändning](/help/data-governance/labels/reference.md). |
| `tags` | Array med strängar | De taggar som du vill använda för den externa målgruppen. Mer information om taggar finns i [handboken för hantering av taggar](/help/administrative-tags/ui/managing-tags.md). |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 202 med information om din nya externa målgrupp.

+++ Ett exempelsvar när du skapar en extern publik.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `operationId` | Sträng | Åtgärdens ID. Du kan sedan använda det här ID:t för att hämta status för hur målgruppen har skapats. |
| `operationDetails` | Objekt | Ett objekt som innehåller information om den begäran du skickade för att skapa den externa målgruppen. |
| `name` | Sträng | Namnet på den externa publiken. |
| `description` | Sträng | Beskrivningen för den externa målgruppen. |
| `fields` | Array med objekt | Listan med fält och deras datatyper. Den här arrayen avgör vilka fält du behöver i den externa publiken. |
| `sourceSpec` | Objekt | Ett objekt som innehåller information om var den externa målgruppen finns. |
| `ttlInDays` | Heltal | Datan upphör att gälla för den externa målgruppen, i dagar. Värdet kan anges från 1 till 90. Som standard är utgångsdatumet för data inställt på 30 dagar. |
| `audienceType` | Sträng | Målgruppstypen för den externa målgruppen. |
| `originName` | Sträng | **Obligatorisk** Målgruppens ursprung. Det är här som publiken kommer ifrån. |
| `namespace` | Sträng | Namnutrymmet för målgruppen. |
| `labels` | Array med strängar | De etiketter för åtkomstkontroll som gäller för den externa målgruppen. Mer information om tillgängliga etiketter för åtkomstkontroll finns i [etikettordlistan för dataanvändning](/help/data-governance/labels/reference.md). |


+++

## Hämta status för målgruppsskapande {#retrieve-status}

Du kan hämta status för din externa målgruppssändning genom att göra en GET-begäran till `/external-audiences/operations`-slutpunkten och ange ID:t för åtgärden som du fick från det skapade externa målgruppssvaret.

**API-format**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{OPERATION_ID}` | Värdet `id` för åtgärden som du vill hämta. |

**Begäran**

+++ Ett exempel på en begäran om att hämta en extern målgrupps åtgärdsstatus.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den externa målgruppens aktivitetsstatus.

+++ Ett exempelsvar när du hämtar en extern målgrupps aktivitetsstatus.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `operationId` | Sträng | ID:t för åtgärden som du hämtar. |
| `status` | Sträng | Åtgärdens status. Detta kan vara något av följande värden: `SUCCESS`, `FAILED`, `PROCESSING`. |
| `operationDetails` | Objekt | Ett objekt som innehåller information om målgruppen. |
| `audienceId` | Sträng | ID för den externa målgrupp som skickas av åtgärden. |
| `createdBy` | Sträng | ID för den användare som skapade den externa målgruppen. |
| `createdAt` | Lång epok-tidsstämpel | Tidsstämpeln, i sekunder, när begäran om att skapa den externa målgruppen skickades. |
| `updatedBy` | Sträng | ID för den användare som senast uppdaterade målgruppen. |
| `updatedAt` | Lång epok-tidsstämpel | Tidsstämpeln, i sekunder, när målgruppen senast uppdaterades. |

+++

## Uppdatera en extern målgrupp {#update-audience}

>[!NOTE]
>
>Om du vill använda följande slutpunkt måste du ha `audienceId` för din externa målgrupp. Du kan hämta `audienceId` från ett lyckat anrop till slutpunkten `GET /external-audiences/operations/{OPERATION_ID}`.

Du kan uppdatera fält för din externa målgrupp genom att göra en PATCH-begäran till slutpunkten `/external-audience` och ange målgruppens ID i sökvägen för begäran.

När du använder den här slutpunkten kan du uppdatera följande fält:

- Målgruppsbeskrivning
- Åtkomstkontrolletiketter på fältnivå
- Etiketter för åtkomstkontroll på målgruppsnivå

Om du uppdaterar fältet med den här slutpunkten **ersätts** innehållet i det fält som du har begärt.

**API-format**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**Begäran**

+++ Ett exempel på en begäran om att uppdatera den externa målgruppens beskrivning.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `description` | Sträng | Den uppdaterade beskrivningen för den externa målgruppen. |

Dessutom kan du uppdatera följande parametrar:

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `labels` | Array | En array som innehåller den uppdaterade listan med åtkomstetiketter för målgruppen. Mer information om tillgängliga etiketter för åtkomstkontroll finns i [etikettordlistan för dataanvändning](/help/data-governance/labels/reference.md). |
| `fields` | Array med objekt | En array som innehåller fälten och tillhörande etiketter för den externa målgruppen. Endast de fält som anges i PATCH-begäran kommer att uppdateras. Mer information om tillgängliga etiketter för åtkomstkontroll finns i [etikettordlistan för dataanvändning](/help/data-governance/labels/reference.md). |
| `ttlInDays` | Heltal | Datan upphör att gälla för den externa målgruppen, i dagar. Värdet kan anges från 1 till 90. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade externa målgruppen.

+++ Ett exempelsvar när den externa målgruppens beskrivning uppdateras.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## Starta målgruppsintag {#start-audience-ingestion}

>[!IMPORTANT]
>
>Du kan **inte** starta ett nytt intag för den externa målgruppen om ett tidigare målgruppsintag redan pågår.

>[!NOTE]
>
>Om du vill använda följande slutpunkt måste du ha `audienceId` för din externa målgrupp. Du kan hämta `audienceId` från ett lyckat anrop till slutpunkten `GET /external-audiences/operations/{OPERATION_ID}`.

Du kan påbörja en målgruppsinmatning genom att göra en POST-begäran till följande slutpunkt och samtidigt ange målar-ID.

**API-format**

```http
POST /external-audience/{AUDIENCE_ID}/run
```

**Begäran**

Följande begäran utlöser en ingressning för den externa målgruppen.

+++ Ett exempel på en förfrågan om att starta ett målgruppsintag.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/run \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Epoch-tidsstämpel | **Obligatoriskt** Intervallet som anger den starttid som flödet ska köras för att välja vilka filer som ska bearbetas. |
| `dataFilterEndTime` | Epoch-tidsstämpel | Det intervall som anger sluttiden som flödet ska köras för att välja vilka filer som ska bearbetas. |
| `differentialIngestion` | Boolean | Ett fält som avgör om intaget är ett partiellt intag baserat på skillnaden sedan det senaste intaget eller ett fullständigt målgruppsintag. Standardvärdet är `true`. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om importen.

+++ Ett exempelsvar när målgruppsintaget startas.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `audienceName` | Sträng | Namnet på målgruppen som du påbörjar ett förtäringsförsök för. |
| `audienceId` | Sträng | Målgruppens ID. |
| `runId` | Sträng | ID:t för det intag du påbörjade. |
| `differentialIngestion` | Boolean | Ett fält som avgör om intaget är ett partiellt intag baserat på skillnaden sedan det senaste intaget eller ett fullständigt målgruppsintag. |
| `dataFilterStartTime` | Epoch-tidsstämpel | Det intervall som anger den starttid som flödet körs för att välja vilka filer som bearbetades. |
| `dataFilterEndTime` | Epoch-tidsstämpel | Det intervall som anger sluttiden som flödet körs för att välja vilka filer som bearbetades. |
| `createdAt` | Lång epok-tidsstämpel | Tidsstämpeln, i sekunder, när begäran om att skapa den externa målgruppen skickades. |
| `createdBy` | Sträng | ID för den användare som skapade den externa målgruppen. |

+++

## Hämta specifik status för målgruppsinmatning {#retrieve-ingestion-status}

Du kan hämta status för ett målgruppsintag genom att göra en GET-begäran till följande slutpunkt samtidigt som du anger både målgrupps- och kör-ID:n.

**API-format**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**Begäran**

Följande begäran hämtar den externa målgruppens inmatningsstatus.

+++ Ett exempel på en begäran om att hämta den externa målgruppens inmatningsstatus.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den externa målgruppens inmatning.

+++ Ett exempelsvar när den externa målgruppens förtäring hämtas.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `audienceName` | Sträng | Namnet på publiken. |
| `audienceId` | Sträng | Målgruppens ID. |
| `runId` | Sträng | ID:t för importen. |
| `status` | Sträng | Status för importen. Möjliga statusar är `SUCCESS` och `FAILED`. |
| `differentialIngestion` | Boolean | Ett fält som avgör om intaget är ett partiellt intag baserat på skillnaden sedan det senaste intaget eller ett fullständigt målgruppsintag. |
| `dataFilterStartTime` | Epoch-tidsstämpel | Det intervall som anger den starttid som flödet körs för att välja vilka filer som bearbetades. |
| `dataFilterEndTime` | Epoch-tidsstämpel | Det intervall som anger sluttiden som flödet körs för att välja vilka filer som bearbetades. |
| `createdAt` | Lång epok-tidsstämpel | Tidsstämpeln, i sekunder, när begäran om att skapa den externa målgruppen skickades. |
| `createdBy` | Sträng | ID för den användare som skapade den externa målgruppen. |
| `details` | Array med objekt | Ett objekt som innehåller information om importen. <ul><li>`stage`: Inledningsfasen. Detta kan antingen vara `DATASET_INGEST` eller `PROFILE_STORE_INGEST`, som representerar inmatningen av data i sjön och intaget av profilen.</li><li>`status`: Status för intaget på scenen. Möjliga statusar är `SUCCESS` och `FAILED`.</li><li>`flowRunId`: ID:t för scenens inmatningsflöde.</li></ul> |

+++

## Visa målgruppsintendationsstatus {#list-ingestion-statuses}

Du kan hämta alla inmatningsstatusar för den valda externa målgruppen genom att göra en GET-begäran till följande slutpunkt och samtidigt ange målar-ID. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

**API-format**

Följande slutpunkt har stöd för flera frågeparametrar som hjälper dig att filtrera dina resultat. Dessa parametrar är valfria, men vi rekommenderar starkt att de används för att hjälpa dig att fokusera dina resultat.

```http
GET /external-audience/{AUDIENCE_ID}/runs
GET /external-audience/{AUDIENCE_ID}/runs?{QUERY_PARAMETERS}
```

**Frågeparametrar**

+++ En lista med tillgängliga frågeparametrar.

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `limit` | Det maximala antalet objekt som returneras i svaret. Värdet kan ligga mellan 1 och 40. Som standard är gränsen 20. | `limit=30` |
| `sortBy` | Den ordning som returnerade artiklar sorteras i. Du kan sortera efter antingen `name` eller `ingestionTime`. Dessutom kan du lägga till ett `-`-tecken för att sortera efter **fallande** i stället för **stigande** ordning. Som standard sorteras objekten efter `ingestionTime` i fallande ordning. | `sortBy=name` |
| `property` | Ett filter för att avgöra vilka målgruppsinmatningar som visas. Du kan filtrera följande egenskaper: <ul><li>`name`: Du kan filtrera efter målgruppens namn. Om du använder den här egenskapen kan du jämföra med `=`, `!=`, `=contains` eller `!=contains`. </li><li>`ingestionTime`: Du kan filtrera efter användningstiden. Om du använder den här egenskapen kan du jämföra med `>=` eller `<=`.</li><li>`status`: Gör att du kan filtrera efter körningens status. Om du använder den här egenskapen kan du jämföra med `=`, `!=`, `=contains` eller `!=contains`. </li></ul> | `property=ingestionTime<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++

**Begäran**

Följande begäran hämtar alla inmatningsstatusar för den externa målgruppen.

+++ Ett exempel på en begäran om att få en lista över status för målgruppsinmatning.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över intagsstatus för den angivna externa målgruppen.

+++ Ett exempelsvar när du hämtar en lista över målgruppsintagningsstatus.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        }
    ],
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
}
```

| Egenskap | Typ | Beskrivning |
| -------- | ---- | ----------- |
| `runs` | Objekt | Ett objekt som innehåller listan med förtäring körs som tillhör målgruppen. Mer information om det här objektet finns i avsnittet [Hämta inmatningsstatus](#retrieve-ingestion-status). |
| `_page` | Objekt | Ett objekt som innehåller sidnumreringsinformation om resultatlistan. |

+++

## Ta bort en extern målgrupp {#delete-audience}

Du kan ta bort en extern målgrupp genom att göra en DELETE-förfrågan till följande slutpunkt och samtidigt ange målar-ID.

**API-format**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**Begäran**

Följande begäran tar bort den angivna externa målgruppen.

+++ En exempelbegäran om att ta bort den externa målgruppen.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 204 med en tom svarstext.

## Nästa steg {#next-steps}

När du har läst den här guiden får du nu en bättre förståelse för hur du skapar, hanterar och tar bort externa målgrupper med Experience Platform API:er. Om du vill lära dig hur du använder externa målgrupper med Experience Platform-gränssnittet läser du dokumentationen för [målportalen](../ui/audience-portal.md).

## Bilaga {#appendix}

I följande avsnitt visas de tillgängliga felkoderna när du använder det externa målgrupps-API:t.

| Felkod för plattform | Statuskod | Meddelande | Beskrivning |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | En felaktig begäran har inträffat på grund av ett fel som uppstod när begäran validerades. |
| 100911-400 | 400 | `BAD_REQUEST` | En ogiltig token har angetts. |
| 100920-401 | 401 | `UNAUTHORIZED` | Ett huvud saknas. |
| 100921-401 | 401 | `UNAUTHORIZED` | En ogiltig `imsOrgId` har angetts. |
| 100922-401 | 401 | `UNAUTHORIZED` | Du har inte behörighet att använda externa målgrupps-API:er. |
| 100940-404 | 404 | `NOT_FOUND` | Det gick inte att hitta den begärda målgruppen. |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | Publiken finns redan. |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | Begärandestrukturen är giltig, men den kan inte behandlas på grund av logiska eller semantiska fel. |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | Ett problem uppstod när begäran bearbetades i systemet. |
| 100970-502 | 502 | `BAD_GATEWAY` | Det finns beroendeproblem i senare led. |
