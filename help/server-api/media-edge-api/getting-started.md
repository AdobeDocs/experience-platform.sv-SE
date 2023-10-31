---
solution: Experience Platform
title: Komma igång med API:er för Media Edge
description: Komma igång med API:er för Media Edge
exl-id: 76022dea-408b-4d8e-abd4-1a6de81beceb
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 1%

---

# Komma igång med API för Media Edge

Den här handboken innehåller anvisningar om hur du utför framgångsrika initiala interaktioner med Media Edge API-tjänsten. Detta inkluderar att starta en mediesession och sedan spåra händelser som skickats till en Adobe Experience Platform-lösning som Customer Journey Analytics (CJA). Media Edge API-tjänsten initieras med sessionens startslutpunkt. När sessionen har startats kan en eller flera av följande händelser spåras:

* `play`
* `ping`
* `bitrateChange`
* `bufferStart`
* `pauseStart`
* `adBreakStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakComplete`
* `chapterStart`
* `chapterComplete`
* `chapterSkip`
* `error`
* `sessionEnd`
* `sessionComplete`
* `statesUpdate`

Varje händelse har en egen slutpunkt. Alla Media Edge API-slutpunkter är POST-metoder med JSON-begärandeinstanser för händelsedata. Mer information om Media Edge API-slutpunkter, parametrar och exempel finns i [Media Edge Swagger-fil](swagger.md).

Den här guiden visar hur du spårar följande händelser efter att du har startat sessionen:

* [Buffertstart](#buffer-start-event-request)
* [Spela upp](#play-event-request)
* [Sessionen slutförd](#session-complete-event-request)

## Implementera API {#implement-api}

Förutom smärre skillnader i anropad modell och sökväg har Media Edge API samma implementering som [Media Collection API](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en). Implementeringsinformationen för Media Collection gäller även fortsättningsvis för Media Edge API, vilket beskrivs i följande dokumentation:

* [Ställa in HTTP-begärantypen i spelaren](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Skicka ping-händelser](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Timeoutvillkor](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [Styra händelseordningen](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Behörighet {#authorization}

Media Edge API:er kräver för närvarande inte auktoriseringshuvuden i sina begäranden.


## Startar sessionen {#start-session}

Om du vill starta mediesessionen på servern använder du slutpunkten för sessionsstart. Ett lyckat svar innehåller `sessionId`, som är en obligatorisk parameter för efterföljande händelsebegäranden.

Innan du gör sessionsstartbegäran behöver du följande:

* The `datastreamId`—en obligatorisk parameter för POSTENS sessionsstartbegäran. Så här hämtar du `datastreamId`, se [Konfigurera ett datastream](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en).

* Ett JSON-objekt för den begärda nyttolasten som innehåller de minsta data som krävs (som visas i exempelbegäran nedan).

När du har fått den här informationen ska du ange `datastreamId` i följande anrop:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Exempelbegäran

I följande exempel visas en cURL-begäran för sessionsstart:

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

I exempelbegäran ovan är `eventType` värdet innehåller prefixet `media.` enligt [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv) för att ange domäner.

Datatypsmappning för `eventType` i exemplet ovan är följande:

| eventType | datatyper |
| -------- | ------ |
| media.SessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): Array[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): Array[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| alla | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Exempel på svar

I följande exempel visas ett lyckat svar för sessionsstartbegäran:

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

I exempelsvaret ovan är `sessionId` visas som `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. Du kommer att använda detta ID i efterföljande händelsebegäranden som en obligatorisk parameter.

Mer information om parametrar och exempel för sessionens startslutpunkt finns i [Media Edge Swagger](swagger.md) -fil.

Mer information om XDM-mediedataparametrar finns i [Informationsschema för mediainformation](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Buffertstarthändelsebegäran {#buffer-start}

Buffertens starthändelse signalerar när buffringen startar i mediespelaren. Buffertåterupptagning är inte en händelse i API-tjänsten, utan kan härledas när en uppspelningshändelse skickas efter Buffertstart. Om du vill göra en begäran om en Buffer Start-händelse använder du `sessionId` i nyttolasten för ett anrop till följande slutpunkt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Exempelbegäran

I följande exempel visas en Buffer Start cURL-begäran:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

I exempelbegäran ovan är det samma `sessionId` som returneras i det föregående anropet används som obligatorisk parameter i Buffer Start-begäran.

Svaret är 200 och innehåller inget innehåll.

Mer information om parametrar och exempel för Buffer Start-slutpunkten finns i [Media Edge Swagger](swagger.md) -fil.


## Spela upp händelsebegäran {#play-event}

Play-händelsen skickas när mediespelaren ändrar sitt läge till&quot;spela upp&quot; från ett annat läge, till exempel&quot;buffring&quot;,&quot;pausad&quot; eller&quot;fel&quot;. Om du vill göra en begäran om uppspelningshändelse använder du `sessionId` i nyttolasten för ett anrop till följande slutpunkt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Exempelbegäran

I följande exempel visas en Play cURL-begäran:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

Svaret är 200 och innehåller inget innehåll.

Mer information om parametrar och exempel för Play-slutpunkter finns i [Media Edge Swagger](swagger.md) -fil.

## Sessionens slutförda händelsebegäran {#session-complete}

Händelsen Slutför session skickas när slutet av huvudinnehållet nås. Om du vill göra en begäran om att slutföra en session använder du `sessionId` i nyttolasten för ett anrop till följande slutpunkt:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Exempelbegäran

I följande exempel visas en fullständig cURL-begäran för session:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

Svaret är 200 och innehåller inget innehåll.

Mer information om parametrar och exempel för slutpunkten för sessionens slut finns i [Media Edge Swagger](swagger.md) -fil.

## Svarskoder

I följande tabell visas möjliga svarskoder från API-begäranden för Media Edge:

| Status | Beskrivning |
| ---------- | --------- |
| 200 | Sessionen har skapats |
| 207 | Problem med en av tjänsterna som ansluter till Edge Network (se mer i [felsökningsguide](troubleshooting.md)) |
| 400-nivå | Felaktig begäran |
| 500-nivå | Serverfel |

## Mer hjälp om funktionen

* [Felsökningsguide för Media Edge](troubleshooting.md)
* [Översikt över API för Media Edge](overview.md)
