---
title: Samla in analyser och tillämpa personalisering i ChatGPT-appar (MCP-datainsamling)
description: Använd en hybrid-MCP-server + Web SDK applyResponse-mönster för att skicka händelser till Adobe Experience Platform Edge Network och återge personalisering inuti ett ChatGPT-appgränssnitt.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, ChatGPT Apps, applyResponse, interact endpoint, personalization, analytics
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Samla in analyser och tillämpa personalisering i ChatGPT-appar (MCP-datainsamling)

I det här exemplet visas hur du ansluter en ChatGPT-app (Model Context Protocol-server + valfria UI-komponenter) till Adobe Experience Platform Edge Network. Med den här typen av datainsamling kan du spela in analyser för konversationsinteraktioner som anropar dina verktyg och levererar personaliseringsbeslut från Edge Network till en widget som renderas av ChatGPT.

>[!NOTE]
>
>Dokumentet underhålls baserat på de senaste tillgängliga uppdateringarna från både Adobe datainsamlingsgrupper och de senaste teknikuppdateringarna från OpenAI. Därför räknar Adobe med att det här dokumentet kommer att utvecklas över tid och rekommenderar att man kontrollerar om det finns uppdateringar.

I det här användningsexemplet rekommenderas en hybridstrategi där både en implementering på serversidan används för datainsamling och en implementering på klientsidan används för återgivning av personaliserat innehåll. Den här metoden är perfekt eftersom anropet till MCP-verktyget är det mest tillförlitliga tillfället att samla in analyser. Widgeten körs i en webbläsarkontext och är rätt plats att lagra identitet (i en cookie) och tillämpa personaliseringsbeslut.

Det här användningsexemplet innehåller ett exempel på en fullt fungerande kod. Se [ChatGPT-appen + Adobe Experience Platform Edge](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app) i `alloy-samples`-databasen på GitHub för exempel på kod och implementeringsinstruktioner.

>[!IMPORTANT]
>
>På den här sidan beskrivs en referensimplementering som är avsedd att illustrera ett integreringsmönster. Granska säkerhets-, sekretess-, samtycke- och produktionskrav innan du börjar använda metoden i programmet.

## Arkitektur

På en hög nivå finns det fem rörliga delar:

1. **MCP-värd (ChatGPT)**: ChatGPT anropar verktyg som exponeras av MCP-servern och tillhandahåller en stabil pseudonym användaridentifierare i metadata för begäran.
1. **MCP-server (backend)**: Ägs av din organisation. Den implementerar verktyg som att lista objekt, hämta information eller skicka begäranden.
1. **Adobe IMS**: Utfärdar åtkomsttoken som används av MCP-servern för att anropa Adobe API:er för datainsamling.
1. **Adobe Experience Platform Edge Network**: Tar emot upplevelsehändelser som skickas av din MCP-server och returnerar analysbekräftelser, tillståndsuppdateringar (som identitet) och personaliseringsbeslut.
1. **Inbäddat webbgränssnitt (klientwidget renderad av MCP-värden)**: Visar strukturerade resultat och använder Adobe-metadata som tagits emot från MCP-serverns serverdel.

## Dataflöde

1. **Användare** frågar **ChatGPT** med hjälp av MCP-servern.
1. **ChatGPT** tolkar promptens avsikt och anropar rätt **backend MCP-verktyg**.
1. **Backend MCP-servern** använder API:erna för datainsamling (`interact` slutpunkt) för att skicka en upplevelsehändelse till **Edge Network** för analyssamling och valfri personalisering.
1. **Edge Network** returnerar svarsreferenser, inklusive lägesuppdateringar och personaliseringsbeslut, till **backend MCP-verktyget**.
1. **Backend MCP-verktyget** returnerar ett verktygsresultat som innehåller affärsdata i `structuredContent` och Adobe-metadata i `_meta` till **ChatGPT**.
1. **ChatGPT** levererar verktygsresultatet till **klientwidgeten** som återger affärsdata och använder Adobe-metadata med hjälp av `applyResponse`-kommandot i Web SDK JavaScript-biblioteket. Detta kommando utökar klientens tillstånd och ger möjlighet till personalisering i användargränssnittet.

I följande avsnitt beskrivs varje steg i detalj.

## Steg 1: Användaren uppmanar ChatGPT med hjälp av MCP-servern

Det här steget är startpunkten för arbetsflödet. Användaren anger en naturlig språkmetod:

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

Mer information finns i [Bygg din MCP-server](https://developers.openai.com/apps-sdk/build/mcp-server/) i dokumentationen för OpenAI-utvecklare.

## Steg 2: ChatGPT tolkar metod och anropar ett MCP-verktyg

ChatGPT tolkar avsikten och anropar rätt verktygshanterare på MCP-servern baserat på MCP-serverns metadata. Det här verktygsanropet skapar en sanning på serversidan för den interaktion som är oberoende av hur användargränssnittet återges. Ett av verktygen kan ha följande metadata:

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

Se [Definiera verktyg](https://developers.openai.com/apps-sdk/plan/tools/) i dokumentationen för OpenAI-utvecklare för mer information om hur du talar om för ChatGPT vad varje MCP-verktyg gör.

## Steg 3: MCP-servern skickar en upplevelsehändelse till Edge Network

När din MCP-server tar emot en begäran, utlöses ett anrop till Adobe Experience Platform Edge Network för att registrera analysdata och eventuellt begära beslut/personalisering. Eftersom den här begäran är server-till-server använder du den autentiserade [`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)-slutpunkten som en del av [API:erna för datainsamling](https://developer.adobe.com/data-collection-apis/docs/). Adobe rekommenderar att du använder ett [anpassat namnutrymme](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities) för att skicka den unika identifieraren OpenAI. Kontrollera att namnutrymmet som du skapar i identitetsgränssnittet och det identitetsnamnutrymme som du definierar i anropet matchar (skiftlägeskänsligt).

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## Steg 4: Edge Network returnerar handtag

När Edge Network tar emot ditt `interact`-anrop svarar det med en `handle`-matris. Arrayen kan innehålla identitets- och personaliseringsbeslut, beroende på din datastream-konfiguration. Ett exempelsvar kan se ut så här:

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

Din MCP-server kan sedan extrahera information från Edge Network svar för att bevara identitetsinformationen:

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## Steg 5: MCP-servern returnerar utdata från strukturerade verktyg plus Adobe-metadata till ChatGPT

I MCP-verktygets svar ingår både utdata för strukturerade verktyg och personalisering från Edge Network.

* Objektet `structuredContent` innehåller affärsdata som ChatGPT kan läsa och lägga till berättarröst från.
* Objektet `_meta` innehåller Adobe-svarshandtag och serverberäknade `identityMap` så att widgeten kan läsa dem utan att visa dessa data för ChatGPT. Om du sparar den här informationen i `_meta.adobe` kan du vara konsekvent på var informationen finns. Om du skickar samma `identityMap` framåt blir det lättare för widgeten att använda samma anpassade identitet för alla senare händelser på användargränssnittets sida.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

Mer information finns i [Verktygsresultat](https://developers.openai.com/apps-sdk/reference/#tool-results) i referenshandboken för OpenAI-utvecklare.

## Steg 6: Widget återger resultatet och tillämpar `_adobe.handles` med `applyResponse`

Widgeten återger affärsdata från `structuredContent` och läser sedan Adobe-metadata från `_meta.adobe`. I ChatGPT är samma data tillgängliga för widgeten via kompatibilitetslagret:

* `window.openai.toolOutput` innehåller `structuredContent`
* `window.openai.toolResponseMetadata` innehåller `_meta`

Widgeten använder Web SDK JavaScript-bibliotekets [`applyResponse`](../../js/commands/applyresponse.md)-kommando för att hydratisera klientläget och återge personaliseringsbeslut som returneras av `interact` -anropet på serversidan. Kontrollera att du anropar kommandot [`configure`](../../js/commands/configure/overview.md) innan du anropar `applyResponse`. Eftersom MCP-servern utförde ett `interact`-anrop behöver du inte omedelbart anropa kommandot [`sendEvent`](../../js/commands/sendevent/overview.md) för verktygsanropets interaktion.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

Om widgeten senare skickar ytterligare gränssnittshändelser kan du inkludera samma `identityMap` för dessa samtal:

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

Det här mönstret håller identitetsanvändningen på serversidan och i användargränssnittet justerad samtidigt som `interact`-anropet på serversidan fortfarande kan användas för att förbli källan för insamling och beslutsfattande av analyser.

## Validering

När alla ovanstående steg har konfigurerats kan du validera följande:

* **Datainsamling:** Kontrollera att händelser når den önskade datauppsättningen och att varje händelse bearbetas som förväntat.
* **Personalization:** Verifiera att beslut returneras av Edge Network och att dessa beslut återges av din widget.

## Säkerhet och integritet

* Behandla ChatGPT-identifierare som känsliga, även om de är pseudonyma.
* Se till att du tillämpar organisationens rutiner för samtycke och datahantering i det här arbetsflödet.
* Adobe rekommenderar att arbetsflöden för OAuth 2.1 används för auktorisering.
* Se till att åtkomsttoken och hemligheter aldrig når klienten eller gränssnittet.
