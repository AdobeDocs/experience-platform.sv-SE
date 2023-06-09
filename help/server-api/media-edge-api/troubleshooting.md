---
keywords: Experience Platform;mediekant;populära ämnen;datumintervall
solution: Experience Platform
title: Komma igång med API:er för Media Edge
description: Felsökningsguide för Media Edge API:er
exl-id: null
source-git-commit: f040ba6d1403da4212fe279e32316bac995905b2
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---


# Felsökningsguide för Media Edge API

Den här guiden innehåller felsökningsanvisningar för hur du hanterar fel och får ett lyckat svar.

## Använda felsvarshjälpmedel

Felen åtföljs av ett svarstext som innehåller ett felobjekt för att underlätta felsökningen. I det här fallet innehåller svarstexten information om problem, som definieras av [RFC 7807 Probleminformation för HTTP-API:er](https://datatracker.ietf.org/doc/html/rfc7807). För att förbättra API-användarupplevelsen är probleminformationen beskrivande (informationen om matrisnycklarna visas med JsonPath till det saknade eller ogiltiga fältet). De är också kumulativa (alla ogiltiga fält rapporteras i samma begäran).


## Valideringssessionen startar

De flesta problem med att skapa sessionsstartbegäranden resulterar i ett 207 Multi-Status-svar.
Nyttolasten liknar de icke-allvarliga felen i Experience Edge Network Server API. Alla Media Analytics-fel har följande typ:  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. Siffrorna som visas i svaret motsvarar felstatusen.

I följande exempel visas en svarstext för en sessionsstartbegäran som båda saknar ett obligatoriskt fält och har ett ogiltigt.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

I exemplet ovan beskrivs båda problemen i `name` och `reason` under `details`: den första orsaken visas `missing required field` och den andra beskriver bristande överensstämmelse med ISO 8601-standarden.


>[!NOTE]
>
> För fel som orsakas direkt från Media Analytics rekommenderar Adobe att du fortsätter att bearbeta den genererade mediesessionen.

## Validera händelser

De flesta ogiltiga händelseförfrågningar resulterar i ett 400 felaktigt svar på begäran. I dessa fall liknar nyttolasten allvarliga fel i Experience Edge Network Server API.

För händelseförfrågningar innehåller Media Edge API-tjänsten ytterligare kontroller som inte fångas in i själva XDM-modellen. Detta inkluderar en kontroll av att sökvägen `eventType` matchar nyttolasten för begäran `eventType`.


I följande exempel visas en `eventType` matchar inte med `adBreakStart` nyttolast skickad till `ee/va/v1/chapterStart`:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

I följande exempel visas ytterligare en Media Edge API-kontroll som söker efter en `chapterStart` ring saknas `chapterDetails` info:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## Hantera fel på 400- och 500-nivå

Följande tabell innehåller anvisningar för hur du hanterar statussvarsfel:


| Felkod | Beskrivning |
| ---------- | --------- |
| 4xx - felaktig begäran | De flesta 4xx-fel (t.ex. 400, 403, 404) bör inte provas igen av användaren. Om du försöker igen kommer det inte att gå att svara. Användaren bör åtgärda felet innan han eller hon försöker utföra begäran igen. Händelser som resulterar i 4xx-statuskoder spåras inte, vilket kan påverka exaktheten för data i sessioner som har tagit emot 4xx-svar. |
| 410 borta | Anger att sessionen som är avsedd för spårning inte längre beräknas på serversidan. Den vanligaste orsaken till detta är att sessionen är längre än 24 timmar. När du har fått 410 försöker du starta en ny session och spåra den. |
| 429 För många begäranden | Den här svarskoden anger att servern hastighetsbegränsar förfrågningarna. Följ **Försök igen efter** instruktionerna i svarshuvudet noggrant. Alla svar som returneras måste innehålla HTTP-svarskoden med en domänspecifik felkod. |
| 500 Internt serverfel | 500 fel är generiska fel som fångar upp alla. 500 fel får inte provas igen, förutom 502, 503 och 504. |
| 502 Ogiltig gateway | Den här felkoden anger att servern, när den fungerar som en gateway, fick ett ogiltigt svar från överordnade servrar. Detta kan inträffa på grund av nätverksproblem mellan servrar. Det temporära nätverksproblemet kan lösa sig så att du kan försöka lösa problemet genom att försöka igen. |
| Tjänsten är inte tillgänglig | Felkoden anger att tjänsten inte är tillgänglig för tillfället. Detta kan inträffa under underhållsperioder. Mottagare med 503 fel kan försöka utföra begäran igen, men bör även följa **Försök igen efter** rubrikinstruktioner. |


Köa händelser när sessionssvaren är långsamma

När en mediaspårningssession har startats kan mediespelaren utlösas innan svaret för sessionsstart returneras (med parametern för sessions-ID) från serverdelen. Om detta inträffar måste programmet placera eventuella spårningshändelser i kö som kommer mellan sessionsbegäran och dess svar. När sessionssvaret kommer, bör du först bearbeta händelser som står i kö och sedan börja bearbeta live-händelser.

För bästa resultat bör du kontrollera referensspelaren i distributionen för att få anvisningar om hur du hanterar händelser innan du får ett sessions-ID.

I följande exempel visas en metod för att bearbeta händelser innan ett sessions-ID tas emot:


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


