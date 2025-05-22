---
title: Hybrid-personalisering med Web SDK och Edge Network API
description: I den här artikeln visas hur du kan använda Web SDK tillsammans med Edge Network API för att distribuera hybridanpassning på dina webbegenskaper.
keywords: personalisering, hybrid, server-api, server-side, hybridimplementering,
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 7b91f4f486db67d4673877477a6be8287693533a
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# Hybrid-personalisering med Web SDK och Edge Network API

## Översikt {#overview}

Hybridanpassning beskriver processen att hämta innehåll på serversidan för personalisering med [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/) och återge den på klientsidan med [Web SDK](../home.md).

Du kan använda hybridpersonalisering med personaliseringslösningar som Adobe Target, Adobe Journey Optimizer eller Offer Decisioning. Skillnaden är innehållet i [!UICONTROL Edge Network API]-nyttolasten.

## Förhandskrav {#prerequisites}

Innan du implementerar hybridanpassning på dina webbegenskaper måste du se till att du uppfyller följande villkor:

* Ni har bestämt vilken personaliseringslösning ni vill använda. Detta påverkar innehållet i nyttolasten [!UICONTROL Edge Network API].
* Du har åtkomst till en programserver som du kan använda för att ringa [!UICONTROL Edge Network API]-anropen.
* Du har åtkomst till [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/).
* Du har [konfigurerat](/help/web-sdk/commands/configure/overview.md) korrekt och distribuerat Web SDK på de sidor som du vill anpassa.

## Flödesdiagram {#flow-diagram}

Flödesdiagrammet nedan beskriver ordningen för de steg som vidtas för att leverera hybridpersonalisering.

![Visuellt flödesdiagram som visar ordningen för de steg som har vidtagits för att leverera hybridanpassning.](assets/hybrid-personalization-diagram.png)

1. Alla befintliga cookies som tidigare lagrats av webbläsaren, med prefixet `kndctr_`, ingår i webbläsarbegäran.
1. Klientens webbläsare begär webbsidan från programservern.
1. När programservern tar emot sidbegäran görs en `POST`-begäran till [Edge Network API interactive data collection endpoint](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) för att hämta personaliseringsinnehåll. `POST`-begäran innehåller en `event` och en `query`. Cookies från föregående steg, om de är tillgängliga, ingår i `meta>state>entries`-arrayen.
1. Edge Network API returnerar personaliseringsinnehållet till programservern.
1. Programservern returnerar ett HTML-svar till klientwebbläsaren som innehåller [identitets- och klustercookies](#cookies).
1. På klientsidan anropas kommandot [!DNL Web SDK] `applyResponse` som skickar sidhuvuden och brödtexten i [!UICONTROL Edge Network API]-svaret från föregående steg.
1. [!DNL Web SDK] återger mål [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)-erbjudanden och Journey Optimizer Web Channel-objekt automatiskt, eftersom flaggan `renderDecisions` är inställd på `true`.
1. Målformulärbaserade [!DNL HTML]/[!DNL JSON]-erbjudanden och kodbaserade Journey Optimizer-upplevelser tillämpas manuellt med metoden `applyProposition` för att uppdatera [!DNL DOM] baserat på personaliseringsinnehållet i förslaget.
1. För målformulärbaserade [!DNL HTML]/[!DNL JSON]-erbjudanden och kodbaserade Journey Optimizer-upplevelser måste visningshändelser skickas manuellt för att ange när det returnerade innehållet har visats. Detta görs via kommandot `sendEvent`.

## Cookies {#cookies}

Cookies används för att bevara användaridentitet och klusterinformation.  När du använder en hybridimplementering hanterar webbprogramservern lagringen och sändningen av dessa cookies under livscykeln för begäran.

| Cookie | Syfte | Lagrad av | Skickat av |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Innehåller information om användaridentitet. | Programserver | Programserver |
| `kndctr_AdobeOrg_cluster` | Anger vilket Edge Network-kluster som ska användas för att slutföra begäranden. | Programserver | Programserver |

## Begär placering {#request-placement}

Edge Network API-begäranden krävs för att få förslag och skicka ett visningsmeddelande. När du använder en hybridimplementering skickar programservern dessa begäranden till Edge Network API.

| Begäran | Skapad av |
|---|---|
| Interagera begäran om att hämta förslag | Programserver |
| Interagera begäran om att skicka visningsmeddelanden | Programserver |


## Upprätta Edge Network regionala värd {#regional-host}

Om du vill etablera den regionala Edge Network-värden läser du först platstipset från cookien `kndctr_<orgId>_AdobeOrg_cluster` som kan ha följande värden:

* `va6`
* `or2`
* `irl1`
* `ind1`
* `sgp3`
* `jpn3`
* `aus3`

Exempel: `kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster: va6`

Edge Network regionala värd har följande format:`<location_hint>.server.adobedc.net` och kan ha följande värden:

* `va6.server.adobedc.net`
* `or2.server.adobedc.net`
* `irl1.server.adobedc.net`
* `ind1.server.adobedc.net`
* `sgp3.server.adobedc.net`
* `jpn3.server.adobedc.net`
* `aus3.server.adobedc.net`

Genom att använda dessa specifika värdar dirigeras förfrågningarna till samma Edge Network-plats som användaren besökte tidigare, och systemet kommer att kunna erbjuda den bästa upplevelsen när användardata finns där.

Om det inte finns något platstips (d.v.s. ingen cookie) använder du standardvärden: `server.adobedc.net`.

>[!TIP]
>
>Det är en god vana att använda en lista över tillåtna platser. Detta förhindrar att platstipset värms upp, eftersom det tillhandahålls via cookies på klientsidan.

## Analysens konsekvenser {#analytics}

När ni implementerar hybridpersonalisering måste ni vara särskilt uppmärksamma på att sidträffar inte räknas flera gånger i Analytics.

När du [konfigurerar en datastream](../../datastreams/overview.md) för Analytics vidarebefordras händelser automatiskt så att sidträffar hämtas.

Exemplet från den här implementeringen använder två olika datastreams:

* En datastream har konfigurerats för Analytics. Den här datastream används för SDK-interaktioner på webben.
* En andra datastream utan någon Analytics-konfiguration. Den här datastream används för Edge Network API-begäranden. Du måste konfigurera denna datastream med samma målkonfiguration som den datastream som du konfigurerade för Analytics.

På så sätt registreras inga Analytics-händelser i serversidans begäran, men det gör klientsidans begäranden. Detta leder till att Analytics-förfrågningar räknas korrekt.

## Bygg begäran på serversidan {#server-side-request}

Exemplet nedan visar en Edge Network API-begäran som din programserver kan använda för att hämta personaliseringsinnehållet.

>[!IMPORTANT]
>
>Denna exempelbegäran använder Adobe Target som en personaliseringslösning. Din begäran kan variera beroende på vilken personaliseringslösning du har valt.


**API-format**

```http
POST /ee/v2/interact
```

### Begäran {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries": [{
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
           "value":"CiY0NzE0NzkwMTUyMzYzMzI4NDAxMjc3NDcwNzA2NTcxMjI3OTI1NVIRCJ_S-uCRMRABGAEqBElSTDHwAZ_S-uCRMQ=="
         }, {
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
           "value": "general=in"
         }, {
            "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster",
            "value": "va6"
         }]
      }
   }
}'
```

| Parameter | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | ID:t för den datastream som du använder för att skicka interaktionerna till Edge Network. Mer information om hur du konfigurerar ett datastream finns i [datastreams-översikten](../../datastreams/overview.md). |
| `requestId` | `String` | Nej | Ett slumpmässigt ID för korrelering av interna serverförfrågningar. Om ingen anges genereras en sådan och returneras i svaret. |

### Proxyrubriker {#proxy-headers}

Följande huvuden krävs för att begäran ska kunna behandlas korrekt.

* `Referer`
* `X-Forwarded-For`
* `X-Forwarded-Proto`
* `X-Forwarded-Host`

Se till att ställa in dessa korrekt så att de pekar på den faktiska klientinformationen. Rubriken `X-Forwarded-For` bör till exempel innehålla klient-IP för att rätt geopositionering ska kunna utföras.

### Rubriker för användaragent {#user-agent-headers}

Använd följande användaragentrubriker för att behandla begäran korrekt.

**Standard**

* `User-Agent`

**Låg entropi (obligatoriskt):**

* `Sec-CH-UA`
* `Sec-CH-UA-Mobile`
* `Sec-CH-UA-Platform`

**Hög entropi (valfritt):**

* `Sec-CH-UA-Platform-Version`
* `Sec-CH-UA-Arch`
* `Sec-CH-UA-Model`
* `Sec-CH-UA-Bitness`
* `Sec-CH-UA-WoW64`

Begäran måste skickas så som visas i [Edge Network API-specifikationen](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/). Se [personaliseringsdokumentationen](https://developer.adobe.com/data-collection-apis/docs/getting-started/personalization/) om ditt användningsexempel kräver det.

### Serversidans svar {#server-response}

Edge Network-svaret innehåller `state:store` instruktioner som ska omformas i `Set-Cookie` rubriker. De sparas i webbläsaren och de kan användas i Web SDK-implementeringen.

Cookies bör anges på den översta domänen så att de skickas tillsammans med begäranden till serverimplementeringen samt klientens. (Eller minst en gemensam underdomän som används av båda implementeringarna)

Exempel:

* Serveranrop använder `api.example.com`
* Klientanrop använder `adobe.example.com`

Cookies bör anges på `.example.com` så att de delas i båda fallen.

Serversidans svar är organiserat i fragment som kallas `Handles`, som genereras beroende på datastream-konfigurationen. Realtidspersonaliseringsmotorer returnerar till exempel `personalization:decisions` handtag medan aktiveringsmotorn i realtid skapar `activation:pull` handtag.

Exemplet nedan visar hur Edge Network API-svaret kan se ut.

```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```



## Begäran på klientsidan {#client-request}

På klientsidan anropas kommandot [!DNL Web SDK] `applyResponse` som skickar sidhuvuden och brödtext för svaret på serversidan.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

Formulärbaserade [!DNL JSON]-erbjudanden tillämpas manuellt med metoden `applyPersonalization` för att uppdatera [!DNL DOM] baserat på personaliseringserbjudandet. För formulärbaserade aktiviteter måste visningshändelser skickas manuellt för att ange när erbjudandet har visats. Detta görs via kommandot `sendEvent`.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## Exempelprogram {#sample-app}

För att du ska kunna experimentera och lära dig mer om den här typen av personalisering tillhandahåller vi ett exempelprogram som du kan hämta och använda för testning. Du kan hämta programmet tillsammans med detaljerade anvisningar om hur du använder det från den här [GitHub-databasen](https://github.com/adobe/alloy-samples).
