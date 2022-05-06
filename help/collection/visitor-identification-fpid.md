---
title: Besökaridentifiering via FPID
description: Lär dig att konsekvent identifiera besökare via server-API med hjälp av FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: gränsnätverk;gateway;api;besökare;identifiering;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Besökaridentifiering via FPID

## Översikt

[!DNL First-party IDs] (`FPIDs`) är enhets-ID:n som genereras, hanteras och lagras av kunder. Detta ger kunderna kontroll över att identifiera användarenheter. Genom att skicka `FPIDs`, genererar Edge Network inte något helt nytt `ECID` för en begäran som inte innehåller någon.

The `FPID` kan inkluderas i API-begärandetexten som en del av `identityMap` eller skickas som en cookie.

An `FPID` kan vara deterministiskt översatt till en `ECID` av Edge Network, så `FPID` identiteter är helt kompatibla med lösningar från Experience Cloud. Få en `ECID` från en specifik `FPID` ger alltid samma resultat, så användarna får en enhetlig upplevelse.

The `ECID` som hämtas på det här sättet kan hämtas via en `identity.fetch` fråga:

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

För förfrågningar som innehåller både `FPID` och `ECID`, `ECID` som redan finns i begäran har högre prioritet än den som kan genereras från `FPID`. Edge Network kommer därför att använda `ECID` redan tillhandahållen och kommer inte att beräkna en från angiven `FPID`.

När det gäller enhets-ID:n `server` datastreams ska använda `FPID` som enhets-ID. Andra identiteter (dvs. `EMAIL`) kan också anges i begärandetexten, men Edge Network kräver att en primär identitet anges explicit. Primär identitet är den grundläggande identitet som profildata ska lagras i.

>[!NOTE]
>
>Begäranden som inte har någon identitet, respektive ingen primär identitet som uttryckligen angetts i begärandetexten, kommer att misslyckas.

Följande `identityMap` fältgruppen har formaterats korrekt för en `server` datastream-begäran:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Följande `identityMap` fältgruppen kommer att resultera i ett felsvar när den anges på en `server` datastream-begäran:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

Det felsvar som returneras av Edge Network i det här fallet liknar följande:

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## Besökaridentifiering med `FPID`

Identifiera användare via `FPID`, se till att `FPID` cookie har skickats innan någon begäran skickas till Edge Network. The `FPID` kan skickas i en cookie eller som en del av `identityMap` i själva förfrågningen.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/ee/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
                    },
                    "webReferrer": {
                        "URL": ""
                    }
                },
                "device": {
                    "screenHeight": 1440,
                    "screenWidth": 3440,
                    "screenOrientation": "landscape"
                },
                "environment": {
                    "type": "browser",
                    "browserDetails": {
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## Begär med `FPID` skickas som `identityMap` fält

Exemplet nedan skickar [!DNL FPID] som `identityMap` parameter.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
