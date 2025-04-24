---
title: Personalisering på serversidan med Edge Network API
description: I den här artikeln visas hur du kan använda Edge Network API för att distribuera anpassning på serversidan på dina webbegenskaper.
keywords: personalisering; server-API; edge network; server-side;
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---


# Personalisering på serversidan med Edge Network API

## Översikt {#overview}

Personalisering på serversidan innebär att [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/getting-started/) används för att anpassa kundupplevelsen på dina webbegenskaper.

I det exempel som beskrivs i den här artikeln hämtas personaliseringsinnehåll på serversidan med Edge Network API. Sedan återges HTML på serversidan baserat på det hämtade personaliseringsinnehållet.

Tabellen nedan visar ett exempel på personaliserat och icke-personaliserat innehåll.

| Exempelsida utan personalisering | Exempelsida med personalisering |
|---|---|
| ![Exempelwebbsida utan personalisering](assets/plain.png) | ![Exempel på webbsida med personalisering](assets/personalized.png) |

## Överväganden {#considerations}

### Cookies {#cookies}

Cookies används för att bevara användaridentitet och klusterinformation.  När du använder en implementering på serversidan hanterar programservern lagringen och sändningen av dessa cookies under livscykeln för begäran.

| Cookie | Syfte | Lagrad av | Skickat av |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Innehåller information om användaridentitet. | Programserver | Programserver |
| `kndctr_AdobeOrg_cluster` | Anger vilket Edge Network-kluster som ska användas för att slutföra begäranden. | Programserver | Programserver |

### Begär placering {#request-placement}

Personalization-begäranden krävs för att få förslag och skicka ett visningsmeddelande. När du använder en implementering på serversidan skickar programservern dessa begäranden till Edge Network API.

| Begäran | Skapad av |
|---|---|
| Interagera begäran om att hämta förslag | Programserver som anropar Edge Network API. |
| Interagera begäran om att skicka visningsmeddelanden | Programserver som anropar Edge Network API. |

## Exempelprogram {#sample-app}

I processen som beskrivs nedan används ett exempelprogram som du kan använda som utgångspunkt för att experimentera och lära dig mer om den här typen av personalisering.

Du kan hämta det här exemplet och anpassa det efter dina egna behov. Du kan till exempel ändra miljövariabler så att exempelprogrammet hämtar in erbjudanden från din egen Experience Platform-konfiguration.

Om du vill göra det öppnar du filen `.env` i databasens rot och ändrar variablerna enligt din konfiguration. Starta om exempelappen så är du redo att experimentera med ditt eget personaliseringsinnehåll.

### Köra exemplet {#running-sample}

Följ stegen nedan för att köra exempelprogrammet.

1. Klona [den här databasen](https://github.com/adobe/alloy-samples) till din lokala dator.
2. Öppna en terminal och navigera till mappen `personalization-server-side`.
3. Kör `npm install`.
4. Kör `npm start`.
5. Öppna webbläsaren och gå till `http://localhost`.

## Processöversikt {#process}

I det här avsnittet beskrivs de steg som används för att hämta personaliseringsinnehåll.

1. [Express](https://expressjs.com/) används för en resurssnål implementering på serversidan. Detta hanterar grundläggande serverförfrågningar och routning.
2. Webbläsaren begär webbsidan. Alla cookies som tidigare lagrats av webbläsaren, med prefix för `kndctr_`, inkluderas.
3. När sidan begärs från programservern skickas en händelse till [slutpunkten för interaktiv datainsamling](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) för att hämta personaliseringsinnehåll. Exempelappen använder hjälpmetoder för att förenkla byggandet och skicka begäranden till API:t (se [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js)). `POST`-begäran innehåller en `event` och en `query`. Cookies från föregående steg, om de är tillgängliga, ingår i `meta>state>entries`-arrayen.

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

4. Target-erbjudandet från den formulärbaserade aktiviteten läses från svaret och används när HTML-svaret skapas.
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

6. [!DNL Visual Experience Composer (VEC)] erbjudanden ignoreras eftersom de bara kan återges via Web SDK.
7. När HTML-svaret returneras ställs identitets- och klustercookies in på programserverns svar.