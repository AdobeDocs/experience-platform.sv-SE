---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: API-slutpunkter för Edge Projection
type: Documentation
description: Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid genom att göra rätt data lättillgänglig och kontinuerligt uppdaterad när förändringar inträffar. Detta görs genom användning av kanter, en geografiskt placerad server som lagrar data och gör dem tillgängliga för program.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 0%

---

# Konfiguration och slutpunkter för kantprojektion

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe Experience Platform ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. Till exempel använder Adobe-program som Adobe Target och Adobe Campaign kanter för att leverera personaliserade kundupplevelser i realtid. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Den här guiden innehåller detaljerade anvisningar om hur du använder [!DNL Real-Time Customer Profile] API för att arbeta med kantprognoser, inklusive mål och konfigurationer.

## Komma igång

API-slutpunkten som används i den här guiden är en del av [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Läs igenom [komma igång-guide](getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anrop i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna ringa anrop till [!DNL Experience Platform] API.

>[!NOTE]
>
>Begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver en `Content-Type` header. Mer än en `Content-Type` används i det här dokumentet. Var särskilt uppmärksam på rubrikerna i samplingssamtalen för att försäkra dig om att du använder rätt `Content-Type` för varje begäran.

## Projektionsdestinationer

En projektion kan dirigeras till en eller flera kanter genom att ange var data ska skickas. Varje projektmål som skapas har ett unikt ID som sedan används för att skapa projektionskonfigurationen.

### Visa alla mål

Du kan lista de kantmål som redan har skapats för din organisation genom att göra en GET-förfrågan till `/config/destinations` slutpunkt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller en `projectionDestinations` arrayen med information för varje mål som visas som ett enskilt objekt i arrayen. Om inga projektioner har konfigurerats `projectionDestinations` matrisen returnerar tom.

>[!NOTE]
>
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
| `_links.self.href` | På den översta nivån matchar den sökväg som användes för att göra en GET-förfrågan. I varje enskilt målobjekt kan den här sökvägen användas i en GET-begäran för att söka efter information om ett specifikt mål direkt. |
| `id` | Inom varje målobjekt `"id"` visar det skrivskyddade, systemgenererade unika ID:t för målet. Detta ID används vid referens till ett specifikt mål och när projektionskonfigurationer skapas. |

Mer information om attributen för en enskild destination finns i avsnittet om [skapa ett mål](#create-a-destination) som följer.

### Skapa ett mål {#create-a-destination}

Om det mål du vill använda inte redan finns kan du skapa ett nytt projektionsmål genom att göra en POST-förfrågan till `/config/destinations` slutpunkt.

**API-format**

```http
POST /config/destinations
```

**Begäran**

Följande begäran skapar ett nytt kantmål.

>[!NOTE]
>
>För att POSTEN ska kunna skapa ett mål krävs en specifik `Content-Type` sidhuvud, enligt nedan. Använda ett felaktigt `Content-Type` header resulterar i ett HTTP Status 415-fel (mediatypen stöds inte).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Om du känner till det unika ID:t för ett projektionsmål kan du utföra en uppslagsbegäran för att visa information om det. Detta gör du genom att göra en GET-förfrågan till `/config/destinations` slutpunkten och ID:t för destinationen i sökvägen för begäran tas med.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svarsobjektet visar information om projektionsmålet. The `id` -attributet ska matcha ID:t för projektionsmålet som angavs i begäran.

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

Ett befintligt mål kan uppdateras genom att en PUT-begäran görs till `/config/destinations` slutpunkt och inklusive ID för målet som ska uppdateras i sökvägen för begäran. Den här åtgärden skriver i stort sett om målet, och därför måste samma attribut anges i texten i begäran som när ett nytt mål skapas.

>[!CAUTION]
>
>API-svaret på uppdateringsbegäran är omedelbart, men ändringarna av projektionerna tillämpas asynkront. Det finns alltså en tidsskillnad mellan när uppdateringen av måldefinitionen görs och när den tillämpas.

**API-format**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DESTINATION_ID}` | Unikt ID för det projektionsmål som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar det befintliga målet så att det inkluderar en andra plats (`dataCenters`).

>[!IMPORTANT]
>
>Begäran från PUT kräver en specifik `Content-Type` sidhuvud, enligt nedan. Använda ett felaktigt `Content-Type` header resulterar i ett HTTP Status 415-fel (mediatypen stöds inte).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `currentVersion` | Den aktuella versionen av det befintliga målet. Värdet för `version` när du utför en uppslagsbegäran för målet. |

**Svar**

Svaret innehåller den uppdaterade informationen om målet, inklusive dess ID och det nya `version` för destinationen.

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

Om din organisation inte längre behöver ett projektionsmål kan du ta bort det genom att göra en DELETE-begäran till `/config/destinations` slutpunkten och inklusive ID:t för målet som du vill ta bort i sökvägen för begäran.

>[!CAUTION]
>
>API-svaret på borttagningsbegäran är omedelbart, men de faktiska ändringarna av data i kanterna sker asynkront. Profildata kommer med andra ord att tas bort från alla kanter ( `dataCenters` anges i projektionsmålet) men processen tar tid att slutföra.

**API-format**

```http
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Begäran om borttagning returnerar HTTP-status 204 (inget innehåll) och en tom svarstext. Du kan bekräfta att borttagningen lyckades genom att utföra en sökbegäran för målet med dess ID. Uppslaget ska returnera HTTP-status 404 (Hittades inte).

## Projektionskonfigurationer

Projektionskonfigurationer ger information om vilka data som ska vara tillgängliga på varje kant. I stället för att projicera en fullständig [!DNL Experience Data Model] (XDM) schema till kanten, en projektion ger bara specifika data, eller fält, från schemat. Din organisation kan definiera mer än en projektionskonfiguration för varje XDM-schema.

### Visa alla projektionskonfigurationer

Du kan lista alla projektionskonfigurationer som har skapats för din organisation genom att göra en GET-förfrågan till `/config/projections` slutpunkt. Du kan också lägga till valfria parametrar i sökvägen för begäran för att komma åt projektionskonfigurationer för ett visst schema eller söka efter en enskild projektion efter dess namn.

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
>
>`schemaName` krävs när du använder `name` parameter, som ett projektionskonfigurationsnamn är bara unikt i kontexten för en schemaklass.

**Begäran**

I följande begäran visas alla projektionskonfigurationer som är associerade med [!DNL Experience Data Model] schemaklass, [!DNL XDM Individual Profile]. Mer information om XDM och dess roll i [!DNL Platform], kan du börja med att läsa [XDM - systemöversikt](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med projektionskonfigurationer i roten `_embedded` -attribut, som finns i `projectionConfigs` array. Om inga projektionskonfigurationer har gjorts för din organisation kan `projectionConfigs` matrisen kommer att vara tom.

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
>
>POSTEN som begär att få skapa en konfiguration kräver en specifik `Content-Type` sidhuvud, enligt nedan. Använda ett felaktigt `Content-Type` header resulterar i ett HTTP Status 415-fel (mediatypen stöds inte).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `selector` | En sträng som innehåller en lista med egenskaper i schemat som ska replikeras till kanterna. De bästa sätten att arbeta med väljare finns i [Väljare](#selectors) i det här dokumentet. |
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

En väljare är en kommaavgränsad lista med XDM-fältnamn. I en projektionskonfiguration anger väljaren vilka egenskaper som ska ingå i projektioner. Formatet på `selector` parametervärdet är löst baserat på XPath-syntax. Syntaxen som stöds sammanfattas nedan, med ytterligare exempel för referens.

### Syntax som stöds

* Använd kommatecken för att markera flera fält. Använd inte blanksteg.
* Använd punktnotation för att markera kapslade fält.
   * Om du till exempel vill välja ett fält med namnet `field` som är kapslad i ett fält med namnet `foo`använder du väljaren `foo.field`.
* När du inkluderar ett fält som innehåller delfält projiceras alla delfält också som standard. Du kan emellertid filtrera de delfält som returneras med parenteser `"( )"`.
   * Till exempel: `addresses(type,city.country)` returnerar bara adresstypen och landet där adressens ort finns för varje `addresses` arrayelement.
   * Exemplet ovan motsvarar `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Både punktnotation och parentetisk notation stöds för att referera till underfält. Det är dock bäst att använda punktnotation eftersom det är mer kortfattat och ger en bättre bild av fälthierarkin.

* Varje fält i en väljare anges i förhållande till svarsroten.
   * Om data är en samling resurser kommer projektionen att innehålla en array med resurser.
   * Om data är en enda resurs innehåller projektionen fält som är relativa till den resursen.
   * Om fältet du markerar är (eller är en del av) en array, kommer projektionen att inkludera den valda delen av alla element i arrayen.

### Exempel på väljarparametern

Exemplen nedan visar exempel `selector` parametrar, följt av de strukturerade värden de representerar.

**person.lastName**

Returnerar `lastName` delfält i `person` objekt i den begärda resursen.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**adresser**

Returnerar alla element i `addresses` -array, inklusive alla fält i varje element, men inga andra fält.

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

Returnerar `person.lastName` och alla element i `addresses` array.

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
>
>När ett kapslat fält returneras, innehåller projektionen de omslutande överordnade objekten. De överordnade fälten innehåller inga andra underordnade fält såvida de inte också markeras uttryckligen.

**adresser(typ, ort)**

Returnerar endast värdena för `type` och `city` fält för varje element i `addresses` array. Alla andra underfält i varje `addresses` -elementet har filtrerats bort.

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

Den här guiden har visat vilka steg som krävs för att konfigurera prognoser och destinationer, inklusive hur du formaterar `selector` parameter. Nu kan du skapa nya projektionsmål och konfigurationer som är specifika för organisationens behov.
