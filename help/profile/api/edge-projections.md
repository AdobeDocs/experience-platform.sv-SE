---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Edge Projection - Real-time Customer Profile API
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 0%

---


# Konfiguration och slutpunkter för kantprojektion

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe Experience Platform ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Adobe-program som Adobe Target och Adobe Campaign använder kanter för att leverera personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Den här guiden innehåller detaljerade anvisningar om hur du använder kundprofils-API i realtid för att arbeta med kantprognoser, inklusive mål och konfigurationer.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [kundprofils-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)i realtid. Innan du fortsätter bör du läsa [Komma igång-guiden](getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

>[!NOTE]
>Begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver en `Content-Type` rubrik. Fler än en `Content-Type` används i det här dokumentet. Var särskilt uppmärksam på rubrikerna i samplingssamtalen för att försäkra dig om att du använder rätt `Content-Type` för varje begäran.

## Projektionsdestinationer

En projektion kan dirigeras till en eller flera kanter genom att ange var data ska skickas. Varje projektmål som skapas har ett unikt ID som sedan används för att skapa projektionskonfigurationen.

### Visa alla mål

Du kan lista de kantmål som redan har skapats för din organisation genom att göra en GET-begäran till `/config/destinations` slutpunkten.

**API-format**

```http
GET /config/destinations
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller en `projectionDestinations` array med information om varje mål som visas som ett enskilt objekt i arrayen. Om inga projektioner har konfigurerats returneras `projectionDestinations` matrisen tom.

>[!NOTE]
>Svaret har förkortats för space och visar endast två mål.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| Egenskap | Beskrivning |
|---|---|
| `_links.self.href` | På den översta nivån matchar sökvägen som användes för att göra GET-begäran. Inom varje enskilt målobjekt kan den här sökvägen användas i en GET-begäran för att söka efter information om ett specifikt mål direkt. |
| `id` | I varje målobjekt `"id"` visas det skrivskyddade, systemgenererade unika ID:t för målet. Detta ID används vid referens till ett specifikt mål och när projektionskonfigurationer skapas. |

Mer information om attributen för ett enskilt mål finns i följande avsnitt om [att skapa ett mål](#create-a-destination) .

### Skapa ett mål {#create-a-destination}

Om målet som du vill använda inte redan finns, kan du skapa ett nytt projektionsmål genom att göra en POST-begäran till `/config/destinations` slutpunkten.

**API-format**

```http
POST /config/destinations
```

**Begäran**

Följande begäran skapar ett nytt kantmål.

>[!NOTE]
>POST-begäran om att skapa ett mål kräver en specifik `Content-Type` rubrik, vilket visas nedan. Om du använder ett felaktigt `Content-Type` huvud genereras ett HTTP-statusfel 415 (medietypen stöds inte).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `type` **(Obligatoriskt)** | Den typ av mål som ska skapas. Det enda godkända värdet, &quot;EDGE&quot;, skapar ett kantmål. |
| `dataCenters` **(Obligatoriskt)** | En strängmatris som visar kanterna som projektionerna ska dirigeras mot. Kan innehålla ett eller flera av följande värden: &quot;OR1&quot; - USA, västra, &quot;VA5&quot; - USA, östra, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obligatoriskt)** | Anger förfallodatum för projektion. Godkänt värdeintervall: 600 till 604800. Standardvärde: 3600. |
| `replicationPolicy` **(Obligatoriskt)** | Definierar beteendet för datareplikeringen från navet till kanterna.  Värden som stöds: PROAKTIVT, REAKTIVT. Standardvärde: REAKTIVT. |

**Svar**

Ett lyckat svar returnerar information om det nya kantmålet, inklusive det skrivskyddade, systemgenererade unika ID:t (`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| Egenskap | Beskrivning |
|---|---|
| `self.href` | Den här sökvägen används för att söka efter (GET) målet direkt och kan även användas för att uppdatera (PUT) eller ta bort (DELETE) målet. |
| `id` | Det skrivskyddade, systemgenererade unika ID:t för målet. Detta ID används för att referera till målet direkt och när projektionskonfigurationer skapas. |
| `version` | Det här skrivskyddade värdet visar målets aktuella version. När ett mål uppdateras ökar versionsnumret automatiskt. |

### Visa ett mål

Om du känner till det unika ID:t för ett projektionsmål kan du utföra en uppslagsbegäran för att visa information om det. Detta gör du genom att göra en GET-begäran till `/config/destinations` slutpunkten och inkludera ID:t för destinationen i sökvägen för begäran.

**API-format**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DESTINATION_ID}` | Unikt ID för det projektionsmål som du vill visa. |

**Begäran**

Följande begäran utför en sökning (GET) för att visa målet för det ID som anges i sökvägen till begäran.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svarsobjektet visar information om projektionsmålet. Attributet `id` ska matcha ID:t för projektionsmålet som angavs i begäran.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### Uppdatera ett mål

En befintlig destination kan uppdateras genom att en PUT-begäran görs till `/config/destinations` slutpunkten och med ID:t för destinationen som ska uppdateras i begärandesökvägen. Den här åtgärden _skriver_ om målet, och därför måste samma attribut anges i texten i begäran som när ett nytt mål skapas.

>[!CAUTION]
>API-svaret på uppdateringsbegäran är omedelbart, men ändringarna av projektionerna tillämpas asynkront. Det finns alltså en tidsskillnad mellan när uppdateringen av måldefinitionen görs och när den tillämpas.

**API-format**

```
PUT /config/destinations/{DESTINATION_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DESTINATION_ID}` | Unikt ID för det projektionsmål som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar det befintliga målet så att det inkluderar en andra plats (`dataCenters`).

>[!IMPORTANT]
>PUT-begäran kräver ett specifikt `Content-Type` huvud, vilket visas nedan. Om du använder ett felaktigt `Content-Type` huvud genereras ett HTTP-statusfel 415 (medietypen stöds inte).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `currentVersion` | Den aktuella versionen av det befintliga målet. Värdet på attributet när `version` du utför en sökningsbegäran för målet. |

**Svar**

Svaret innehåller den uppdaterade informationen för målet, inklusive dess ID och det nya `version` målet.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### Ta bort ett mål

Om din organisation inte längre behöver ett projektionsmål kan du ta bort det genom att göra en DELETE-begäran till `/config/destinations` slutpunkten och inkludera ID:t för målet som du vill ta bort i sökvägen till begäran.

>[!CAUTION]
>API-svaret på borttagningsbegäran är omedelbart, men de faktiska ändringarna av data i kanterna sker asynkront. Profildata kommer med andra ord att tas bort från alla kanter (de `dataCenters` som anges i projektionsmålet), men processen tar tid att slutföra.

**API-format**

```
DELETE /config/destinations/{DESTINATION_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DESTINATION_ID}` | Unikt ID för det projektionsmål som du vill ta bort. |


**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Begäran om borttagning returnerar HTTP-status 204 (inget innehåll) och en tom svarstext. Du kan bekräfta att borttagningen lyckades genom att utföra en sökbegäran för målet med dess ID. Uppslaget ska returnera HTTP-status 404 (Hittades inte).

## Projektionskonfigurationer

Projektionskonfigurationer ger information om vilka data som ska vara tillgängliga på varje kant. I stället för att projicera ett fullständigt XDM-schema (Experience Data Model) till kanten, ger en projektion endast specifika data, eller fält, från schemat. Din organisation kan definiera mer än en projektionskonfiguration för varje XDM-schema.

### Visa alla projektionskonfigurationer

Du kan lista alla projektionskonfigurationer som har skapats för din organisation genom att göra en GET-begäran till `/config/projections` slutpunkten. Du kan också lägga till valfria parametrar i sökvägen för begäran för att komma åt projektionskonfigurationer för ett visst schema eller söka efter en enskild projektion efter dess namn.

**API-format**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parameter | Beskrivning |
|---|---|
| `{SCHEMA_NAME}` | Namnet på schemaklassen som är associerad med den projektionskonfiguration som du vill komma åt. |
| `{PROJECTION_NAME}` | Namnet på den projektionskonfiguration som du vill komma åt. |

>[!NOTE]
>`schemaName` krävs när du använder `name` parametern, eftersom ett projektionskonfigurationsnamn bara är unikt i kontexten för en schemaklass.

**Begäran**

I följande begäran visas alla projektionskonfigurationer som är associerade med Experience Data Model-schemaklassen, XDM Individual Profile. Mer information om XDM och dess roll i Platform finns i [översikten](../../xdm/home.md)över XDM-systemet.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med projektionskonfigurationer i rotattributet `_embedded` , som finns i `projectionConfigs` arrayen. Om inga projektionskonfigurationer har gjorts för din organisation är `projectionConfigs` arrayen tom.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### Skapa en projektionskonfiguration

Du kan skapa (POST) en ny projektionskonfiguration som anger vilka XDM-fält som ska vara tillgängliga vid kanterna.

**API-format**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parameter | Beskrivning |
|---|---|
| `{SCHEMA_NAME}` | Namnet på schemaklassen som är associerad med den projektionskonfiguration som du vill komma åt. |

**Begäran**

>[!NOTE]
>POST-begäran om att skapa en konfiguration kräver en specifik `Content-Type` rubrik, vilket visas nedan. Om du använder ett felaktigt `Content-Type` huvud genereras ett HTTP-statusfel 415 (medietypen stöds inte).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `selector` | En sträng som innehåller en lista med egenskaper i schemat som ska replikeras till kanterna. De bästa sätten att arbeta med väljare finns i avsnittet [Väljare](#selectors) i det här dokumentet. |
| `name` | Ett beskrivande namn för den nya projektionskonfigurationen. |
| `destinationId` | Identifieraren för kantmålet som data projiceras till. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade projektionskonfigurationen.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## Väljare {#selectors}

En väljare är en kommaavgränsad lista med XDM-fältnamn. I en projektionskonfiguration anger väljaren vilka egenskaper som ska ingå i projektioner. Formatet på `selector` parametervärdet baseras löst på XPath-syntax. Syntaxen som stöds sammanfattas nedan, med ytterligare exempel för referens.

### Syntax som stöds

* Använd kommatecken för att markera flera fält. Använd inte blanksteg.
* Använd punktnotation för att markera kapslade fält.
   * Om du till exempel vill markera ett fält med namnet `field` som är kapslat i ett fält med namnet `foo`använder du väljaren `foo.field`.
* När du inkluderar ett fält som innehåller delfält projiceras alla delfält också som standard. Du kan emellertid filtrera de delfält som returneras med parenteser `"( )"`.
   * Returnerar t.ex. bara adresstypen och det land där adressstaden finns för varje `addresses(type,city.country)` `addresses` matriselement.
   * Ovanstående exempel motsvarar `addresses.type,addresses.city.country`.

>[!NOTE]
>Både punktnotation och parentetisk notation stöds för att referera till underfält. Det är dock bäst att använda punktnotation eftersom det är mer kortfattat och ger en bättre bild av fälthierarkin.

* Varje fält i en väljare anges i förhållande till svarsroten.
   * Om data är en samling resurser kommer projektionen att innehålla en array med resurser.
   * Om data är en enda resurs innehåller projektionen fält som är relativa till den resursen.
   * Om fältet du markerar är (eller är en del av) en array, kommer projektionen att inkludera den valda delen av alla element i arrayen.

### Exempel på väljarparametern

I följande exempel visas exempelparametrar `selector` följt av de strukturerade värden som de representerar.

**person.lastName**

Returnerar `lastName` underfältet för `person` objektet i den begärda resursen.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**adresser**

Returnerar alla element i `addresses` arrayen, inklusive alla fält i varje element, men inga andra fält.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName,adresser**

Returnerar `person.lastName` fältet och alla element i `addresses` arrayen.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**adresser.city**

Returnerar endast stadsfältet för alla element i adressarrayen.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>När ett kapslat fält returneras, innehåller projektionen de omslutande överordnade objekten. De överordnade fälten innehåller inga andra underordnade fält såvida de inte också markeras uttryckligen.

**adresser(typ, ort)**

Returnerar bara värdena för `type` och `city` fälten för varje element i `addresses` arrayen. Alla andra underfält i varje `addresses` element filtreras bort.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## Nästa steg

Den här guiden har visat vilka steg som krävs för att konfigurera prognoser och destinationer, inklusive hur du formaterar `selector` parametern korrekt. Nu kan du skapa nya projektionsmål och konfigurationer som är specifika för organisationens behov.