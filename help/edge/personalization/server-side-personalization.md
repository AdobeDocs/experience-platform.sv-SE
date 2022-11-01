---
title: Personalisering på serversidan med Edge Network Server API
description: I den här artikeln visas hur du kan använda Edge Network Server API för att distribuera anpassning på serversidan på dina webbegenskaper.
keywords: personalisering, server-api; gränsnät, serversidan;
source-git-commit: 3e7084953a5e158059074c857bfce4940a83661b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---


# Personalisering på serversidan med Edge Network Server API

## Översikt {#overview}

Personalisering på serversidan innebär att använda [API för Edge Network Server](../../server-api/overview.md) för att personalisera kundupplevelsen på era webbegenskaper.

I det exempel som beskrivs i den här artikeln hämtas personaliseringsinnehåll på serversidan med Server-API:t. Sedan återges HTML på serversidan baserat på det hämtade personaliseringsinnehållet.

Tabellen nedan visar ett exempel på personaliserat och icke-personaliserat innehåll.

| Exempelsida utan personalisering | Exempelsida med personalisering |
|---|---|
| ![Exempel på webbsida utan personalisering](assets/plain.png) | ![Exempel på webbsida med personalisering](assets/personalized.png) |

## Överväganden {#considerations}

### Cookies {#cookies}

Cookies används för att bevara användaridentitet och klusterinformation.  När du använder en implementering på serversidan hanterar programservern lagringen och sändningen av dessa cookies under livscykeln för begäran.

| Cookie | Syfte | Lagrad av | Skickat av |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Innehåller information om användaridentitet. | Programserver | Programserver |
| `kndctr_AdobeOrg_cluster` | Anger vilket Edge Network-kluster som ska användas för att slutföra begäranden. | Programserver | Programserver |

### Begär placering {#request-placement}

Personaliseringsbegäranden krävs för att få förslag och skicka ett visningsmeddelande. När du använder en implementering på serversidan skickar programservern dessa begäranden till Edge Network Server API.

| Begäran | Skapad av |
|---|---|
| Interagera begäran om att hämta förslag | Programserver som anropar Edge Network Server API. |
| Interagera begäran om att skicka visningsmeddelanden | Programserver som anropar Edge Network Server API. |

## Exempelprogram {#sample-app}

I processen som beskrivs nedan används ett exempelprogram som du kan använda som utgångspunkt för att experimentera och lära dig mer om den här typen av personalisering.

Du kan hämta det här exemplet och anpassa det efter dina egna behov. Du kan till exempel ändra miljövariabler så att exempelprogrammet hämtar in erbjudanden från din egen Experience Platform-konfiguration.

Öppna `.env` på databasens rot och ändra variablerna enligt din konfiguration. Starta om exempelappen så är du redo att experimentera med ditt eget personaliseringsinnehåll.

### Köra exemplet {#running-sample}

Följ stegen nedan för att köra exempelprogrammet.

1. Klona [denna databas](https://github.com/adobe/alloy-samples) till din lokala dator.
2. Öppna en terminal och navigera till `personalization-server-side` mapp.
3. Kör `npm install`.
4. Kör `npm start`.
5. Öppna webbläsaren och navigera till `http://localhost`.

## Processöversikt {#process}

I det här avsnittet beskrivs de steg som används för att hämta personaliseringsinnehåll.

1. [Express](https://expressjs.com/) används för en resurssnål implementering på serversidan. Detta hanterar grundläggande serverförfrågningar och routning.
2. Webbläsaren begär webbsidan. Alla cookies som tidigare lagrats av webbläsaren, prefixerade med `kndctr_`, ingår.
3. När sidan begärs från programservern skickas en händelse till [slutpunkt för interaktiv datainsamling](../../../server-api/interactive-data-collection.md) för att hämta personaliseringsinnehåll. Exempelappen använder hjälpmetoder för att förenkla byggandet och skicka begäranden till API (se [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)). The `POST` begäran innehåller `event` och `query`. Cookies från föregående steg, om sådana finns, ingår i `meta>state>entries` array.

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. Target-erbjudandet från den formulärbaserade aktiviteten läses från svaret och används när svaret från HTML tas fram.
5. För formulärbaserade aktiviteter måste visningshändelser skickas manuellt i implementeringen för att ange när erbjudandet har visats. I det här exemplet skickas meddelandet på serversidan under livscykeln för begäran.

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)] Erbjudandena ignoreras eftersom de bara kan återges via Web SDK.
7. När HTML-svaret returneras ställs identitets- och klustercookies in på programserverns svar.