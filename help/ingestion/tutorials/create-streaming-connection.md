---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en direktuppspelningsanslutning med API:t
topic: tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---


# Skapa en direktuppspelningsanslutning med API:t

Den här självstudiekursen hjälper dig att börja använda API:er för direktuppspelning, som ingår i Adobe Experience Platform Data API: [!DNL Ingestion Service] er.

## Komma igång

Registrering av direktuppspelningsanslutning krävs för att starta direktuppspelning av data till Adobe Experience Platform. När du registrerar en direktuppspelningsanslutning måste du ange viss nyckelinformation, som källan för direktuppspelningsdata.

När du har registrerat en direktuppspelningsanslutning får du som DataProducer en unik URL som kan användas för att strömma data till Platform.

Den här självstudiekursen kräver också kunskaper om olika Adobe Experience Platform-tjänster. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar upplevelsedata.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:er för direktuppspelning.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Skapa en anslutning

En anslutning anger källan och innehåller den information som krävs för att göra flödet kompatibelt med API:er för direktuppspelning.

**API-format**

```http
POST /flowservice/connections
```

**Begäran**

>[!NOTE]
>
>Värdena för de listade `providerId` och de `connectionSpec` måste **** användas enligt exemplet, eftersom de är vad som anger för API:t att du skapar en direktuppspelningsanslutning för direktuppspelningsinmatning.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
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

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om den nya anslutningen.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Den nya `id` anslutningens namn. Detta kommer att kallas `{CONNECTION_ID}`. |
| `etag` | En identifierare som tilldelats anslutningen och som anger ändringen av anslutningen. |

## Hämta URL för datainsamling

När anslutningen har skapats kan du nu hämta din URL för datainsamling.

**API-format**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Värdet `id` för anslutningen som du skapade tidigare. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den begärda anslutningen. URL:en för datainsamling skapas automatiskt med anslutningen och kan hämtas med `inletUrl` värdet.

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

Nu när du har skapat en direktuppspelningsanslutning kan du direktuppspela antingen tidsserier eller spela in data, så att du kan importera data i [!DNL Platform]. Om du vill lära dig hur du direktuppspelar tidsseriedata [!DNL Platform]går du till självstudiekursen [om data för](./streaming-time-series-data.md)direktuppspelningstidsserier. Om du vill lära dig hur du direktuppspelar postdata [!DNL Platform]går du till självstudiekursen [om](./streaming-record-data.md)direktuppspelningspostdata.

## Bilaga

I det här avsnittet finns ytterligare information om hur du skapar direktuppspelningsanslutningar med API:t.

### Autentiserade direktuppspelningsanslutningar

Autentiserad datainsamling gör det möjligt för Adobe Experience Platform-tjänster, som [!DNL Real-time Customer Profile] och [!DNL Identity], att skilja mellan poster som kommer från betrodda källor och otillförlitliga källor. Klienter som vill skicka personligt identifierbar information (PII) kan göra det genom att skicka IMS Access-token som en del av POSTEN - om IMS-token är giltig markeras posterna som insamlade från betrodda källor.

Mer information om hur du skapar en autentiserad direktuppspelningsanslutning finns i självstudiekursen [Skapa en autentiserad direktuppspelningsanslutning](create-authenticated-streaming-connection.md).