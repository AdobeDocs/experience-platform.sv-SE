---
keywords: Experience Platform;hem;populära ämnen;hämta misslyckade batchar;misslyckade batchar;batchöverföring;Batchhämtning;Misslyckade batchar;Hämta misslyckade batchar;hämta misslyckade batchar;Hämtning misslyckades batchar;hämta misslyckade batchar;
solution: Experience Platform
title: Hämtning av misslyckade batchar med API:t för dataåtkomst
topic: tutorial
type: Tutorial
description: I den här självstudiekursen beskrivs steg för hur du hämtar information om en misslyckad batch med hjälp av API:er för datainmatning.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Hämtning av misslyckade batchar med API:t för dataåtkomst

Adobe Experience Platform har två metoder för att överföra och importera data. Du kan antingen använda batchinmatning, som gör att du kan infoga deras data med olika filtyper (t.ex. CSV-filer), eller direktuppspelning, vilket gör att du kan infoga deras data i [!DNL Platform] med direktuppspelningsslutpunkter i realtid.

I den här självstudiekursen beskrivs steg för att hämta information om en misslyckad batch med hjälp av [!DNL Data Ingestion] API:er.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
- [[!DNL Data Ingestion]](../home.md): Metoderna som data kan skickas till  [!DNL Experience Platform].

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Schema Registry], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: `application/json`

### Samplingen misslyckades

I den här självstudien används exempeldata med en felaktigt formaterad tidsstämpel som anger att månadens värde ska vara **00**, vilket visas nedan:

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

Nyttolasten ovan valideras inte korrekt mot XDM-schemat på grund av den felaktiga tidsstämpeln.

## Hämta den misslyckade batchen

**API-format**

```http
GET /batches/{BATCH_ID}/failed
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID:t för gruppen som du letar upp. |

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
```

**Svar**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Med svaret ovan ser du vilka delar av gruppen som har slutförts och misslyckats. Från det här svaret ser du att filen `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` innehåller den misslyckade batchen.

## Hämta den misslyckade batchen

När du vet vilken fil i gruppen som misslyckades kan du hämta den misslyckade filen och se vad felmeddelandet är.

**API-format**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID för den batch som innehåller den misslyckade filen. |
| `{FAILED_FILE}` | Namnet på filen som har den felaktiga formateringen. |

**Begäran**

Följande begäran gör att du kan hämta filen som hade fel i inläsningen.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Eftersom den tidigare importerade batchen hade ett ogiltigt datum/tid visas följande valideringsfel.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## Nästa steg

Efter att ha läst den här självstudiekursen har du lärt dig hur du hämtar fel från misslyckade batchar. Mer information om batchförbrukning finns i [Utvecklarhandbok för batchimport](../batch-ingestion/overview.md). Mer information om direktuppspelning finns i [självstudiekursen om att skapa en direktuppspelningsanslutning](../tutorials/create-streaming-connection.md).

## Bilaga

Det här avsnittet innehåller information om andra typer av fel som kan uppstå vid förtäring.

### Felaktigt formaterad XDM

Precis som tidsstämpelfelet i det föregående exempelflödet beror dessa fel på felaktigt formaterad XDM. Felmeddelandena varierar beroende på vad problemet är. Därför kan inget specifikt felexempel visas.

### IMS-organisations-ID saknas eller är ogiltigt

Det här felet visas om IMS-organisations-ID:t saknas i nyttolasten och är ogiltigt.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### XDM-schema saknas

Det här felet visas om `schemaRef` för `xdmMeta` saknas.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Källnamn saknas

Det här felet visas om `source` i huvudet saknar `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### XDM-entitet saknas

Det här felet visas om det inte finns någon `xdmEntity`.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
