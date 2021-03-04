---
keywords: Experience Platform;hem;populära ämnen;direktuppspelningsanslutning;skapa direktuppspelningsanslutning;api guide;självstudiekurs;skapa en direktuppspelningsanslutning;direktuppspelningsproblem;intag;
solution: Experience Platform
title: Skapa en direktuppspelningsanslutning med API:t
topic: självstudiekurs
type: Självstudiekurs
description: Den här självstudiekursen hjälper dig att börja använda API:er för direktuppspelning, som ingår i API:erna för Adobe Experience Platform datainmatningstjänst.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 1%

---


# Skapa en direktuppspelningsanslutning med API:t

Flow Service används för att samla in och centralisera kunddata från olika källor inom Adobe Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som alla källor som stöds kan anslutas från.

I den här självstudien används API:t [!DNL Flow Service] för att vägleda dig genom stegen för att skapa en direktuppspelningsanslutning med API:t för Flow Service.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Det standardiserade ramverk som  [!DNL Platform] organiserar upplevelsedata.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:er för direktuppspelning.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../../../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Skapa en anslutning

En anslutning anger källan och innehåller den information som krävs för att göra flödet kompatibelt med API:er för direktuppspelning. När du skapar en anslutning kan du skapa en icke-autentiserad och autentiserad anslutning.

### Icke-autentiserad anslutning

Icke-autentiserade anslutningar är den standarddirektuppspelningsanslutning som du kan skapa när du vill strömma data till plattformen.

**API-format**

```http
POST /flowservice/connections
```

**Begäran**

För att kunna skapa en direktuppspelningsanslutning måste leverantörs-ID och anslutningsspecifikations-ID anges som en del av POSTEN. Leverantörs-ID är `521eee4d-8cbe-4906-bb48-fb6bd4450033` och anslutningsspecifikations-ID är `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.sourceId` | ID:t för den direktuppspelningsanslutning som du vill skapa. |
| `auth.params.dataType` | Datatypen för direktuppspelningsanslutningen. Värdet måste vara `xdm`. |
| `auth.params.name` | Namnet på den direktuppspelningsanslutning som du vill skapa. |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för direktuppspelningsanslutningar. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om den nya anslutningen, inklusive dess unika identifierare (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | `id` för den nya anslutningen. Detta kallas `{CONNECTION_ID}`. |
| `etag` | En identifierare som tilldelats anslutningen och som anger ändringen av anslutningen. |

### Autentiserad anslutning

Autentiserade anslutningar bör användas när du behöver skilja mellan poster som kommer från betrodda och ej betrodda källor. Användare som vill skicka information med personligt identifierbar information (PII) bör skapa en autentiserad anslutning vid direktuppspelning av information till plattformen.

**API-format**

```http
POST /flowservice/connections
```

**Begäran**

För att kunna skapa en direktuppspelningsanslutning måste leverantörs-ID och anslutningsspecifikations-ID anges som en del av POSTEN. Leverantörs-ID är `521eee4d-8cbe-4906-bb48-fb6bd4450033` och anslutningsspecifikations-ID är `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.sourceId` | ID:t för den direktuppspelningsanslutning som du vill skapa. |
| `auth.params.dataType` | Datatypen för direktuppspelningsanslutningen. Värdet måste vara `xdm`. |
| `auth.params.name` | Namnet på den direktuppspelningsanslutning som du vill skapa. |
| `auth.params.authenticationRequired` | Parametern som anger att den skapade direktuppspelningsanslutningen |
| `connectionSpec.id` | Anslutningsspecifikationen `id` för direktuppspelningsanslutningar. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om den nya anslutningen, inklusive dess unika identifierare (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | `id` för den nya anslutningen. Detta kallas `{CONNECTION_ID}`. |
| `etag` | En identifierare som tilldelats anslutningen och som anger ändringen av anslutningen. |

## Hämta URL för direktuppspelningsslutpunkt

När anslutningen har skapats kan du nu hämta din URL för direktuppspelningsslutpunkt.

**API-format**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | `id`-värdet för anslutningen som du skapade tidigare. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den begärda anslutningen. URL:en för direktuppspelningsslutpunkten skapas automatiskt med anslutningen och kan hämtas med `inletUrl`-värdet.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en HTTP-direktuppspelningsanslutning, vilket gör att du kan använda direktuppspelningsslutpunkten för att importera data till plattformen. Instruktioner om hur du skapar en direktuppspelningsanslutning i användargränssnittet finns i [självstudiekursen ](../../../ui/create/streaming/http.md) om hur du skapar en direktuppspelningsanslutning.

Om du vill lära dig att strömma data till plattformen kan du läsa självstudiekursen om [data från tidsserierna för direktuppspelning](../../../../../ingestion/tutorials/streaming-time-series-data.md) eller självstudiekursen om [data för direktuppspelningsposter](../../../../../ingestion/tutorials/streaming-record-data.md).

## Bilaga

I det här avsnittet finns ytterligare information om hur du skapar direktuppspelningsanslutningar med API:t.

### Skicka meddelanden till en autentiserad direktuppspelningsanslutning

Om en direktuppspelningsanslutning har autentisering aktiverat måste klienten lägga till `Authorization`-huvudet i sin begäran.

Om rubriken `Authorization` inte finns, eller om en åtkomsttoken som är ogiltig/utgången skickas, returneras ett otillåtet HTTP 401-svar med ett liknande svar som nedan:

**Svar**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
