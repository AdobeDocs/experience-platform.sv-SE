---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Utvecklarhandbok för kundprofil-API i realtid
topic: guide
translation-type: tm+mt
source-git-commit: 4bab89c981f7e30b28477068625d1b6f534fa838
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 0%

---


# Sammanfoga profiler

Med Adobe Experience Platform kan ni samla data från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som används av Platform för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. I den här handboken visas steg för hur du arbetar med sammanfogningsprinciper med API:t. Om du vill arbeta med sammanfogningsprinciper med hjälp av användargränssnittet läser du i [användarhandboken](../ui/merge-policies.md)för sammanfogningsprinciper.

## Komma igång

API-slutpunkterna som används i den här guiden ingår i kundprofils-API:t i realtid. Innan du fortsätter bör du läsa utvecklarhandboken för [kundprofiler i realtid](getting-started.md). Avsnittet [](getting-started.md#getting-started) Komma igång i guiden för profilutvecklare innehåller länkar till relaterade ämnen, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa API:er för Experience Platform.

## Komponenter i sammanfogningsprinciper {#components-of-merge-policies}

Sammanslagningsprinciper är privata för IMS-organisationen, vilket gör att du kan skapa olika profiler för att sammanfoga scheman på det sätt du behöver. Alla API:er som använder profildata kräver en sammanfogningsprincip, men en standardprincip används om ingen sådan uttryckligen anges. Plattformen innehåller en standardprincip för sammanslagning, eller så kan du skapa en sammanfogningsprincip för ett specifikt schema och markera den som standard för din organisation. Varje organisation kan ha flera sammanfogningsprinciper per per schema, men varje schema kan bara ha en standardsammanfogningsprincip. Alla sammanfogningsprinciper som anges som standard används i de fall där schemanamnet anges och en sammanfogningsprincip krävs, men inte anges. När du anger en sammanfogningsprincip som standard kommer alla befintliga sammanfogningsprinciper som tidigare var inställda som standard automatiskt att uppdateras till att inte längre användas som standard.

### Slutför policyobjekt för sammanfogning

Det fullständiga principobjektet för sammanfogning representerar en uppsättning inställningar som styr aspekter av sammanfogning av profilfragment.

**Kopplingsprincipobjekt**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": {BOOLEAN},
        "updateEpoch": {UPDATE_TIME}
    }
```

| Egenskap | Beskrivning |
|---|---|
| `id` | Den systemgenererade unika identifieraren som tilldelats vid skapandetillfället |
| `name` | Eget namn som sammanfogningsprincipen kan identifieras med i listvyer. |
| `imsOrgId` | Organisations-ID som den här sammanfogningsprincipen tillhör |
| `identityGraph` | [Identitetsdiagramobjekt](#identity-graph) som anger identitetsdiagrammet som relaterade identiteter ska hämtas från. Profilfragment som hittas för alla relaterade identiteter sammanfogas. |
| `attributeMerge` | [Kopplingsobjekt för](#attribute-merge) attribut anger på vilket sätt sammanfogningsprincipen prioriterar profilattributsvärden vid datakonflikter. |
| `schema` | Det [schemaobjekt](#schema) som sammanfogningsprincipen kan användas på. |
| `default` | Booleskt värde som anger om den här sammanfogningsprincipen är standard för det angivna schemat. |
| `version` | Plattformsbaserad version av sammanslagningsprincipen. Det här skrivskyddade värdet ökas stegvis när en sammanfogningsprincip uppdateras. |
| `updateEpoch` | Datum för den senaste uppdateringen av sammanfogningsprincipen. |

**Exempel på sammanfogningsprincip**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Identitetsdiagram {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) hanterar de identitetsdiagram som används globalt och för varje organisation på Experience Platform. Attributet `identityGraph` för sammanfogningsprincipen definierar hur relaterade identiteter för en användare ska fastställas.

**identityGraph-objekt**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Där `{IDENTITY_GRAPH_TYPE}` är något av följande:

* **&quot;none&quot;:** Utför ingen identitetssammanfogning.
* **&quot;pdg&quot;:** Utför identitetssammanfogning baserat på ditt privata identitetsdiagram.

**Exempel`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Koppla attribut {#attribute-merge}

Ett profilfragment är profilinformationen för endast en identitet från listan över identiteter som finns för en viss användare. När typen av identitetsdiagram som används resulterar i mer än en identitet, finns det en risk för att värden som står i konflikt med varandra för profilegenskaper och prioritet måste anges. Med `attributeMerge`kan du ange vilka datamängdsprofilvärden som ska prioriteras i händelse av en sammanslagningskonflikt.

**attributeMerge, objekt**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Där `{ATTRIBUTE_MERGE_TYPE}` är något av följande:

* **&quot;timestampOrdered&quot;**: (standard) Prioritera profilen som uppdaterades senast vid en eventuell konflikt. Attributet är inte obligatoriskt om du använder den här sammanfogningstypen `data` .
* **&quot;dataSetPriedence&quot;** : Prioritera profilfragment baserat på den datauppsättning som de kommer från. Detta kan användas när information som finns i en datauppsättning är att föredra eller betrodd framför data i en annan datauppsättning. När du använder den här sammanfogningstypen är attributet obligatoriskt, eftersom det visar datauppsättningarna i prioritetsordning. `order`
   * **&quot;beställ&quot;**: När&quot;dataSetPriedence&quot; används måste en `order` array anges med en lista över datauppsättningar. Datauppsättningar som inte ingår i listan kommer inte att sammanfogas. Datamängder måste med andra ord anges explicit för att sammanfogas till en profil. Arrayen visar `order` datauppsättningens ID i prioritetsordning.

**Exempel på attributeMerge-objekt som använder datamängdPrioritet-typ**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**Exempel på attributeMerge-objekt med typen timestampOrdered**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Schemaobjektet anger det XDM-schema som den här sammanfogningsprincipen skapas för.

**`schema`object **

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Där värdet för `name` är namnet på XDM-klassen som schemat som är associerat med sammanfogningsprincipen baseras på.

**Exempel`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## Åtkomst till sammanfogningsprinciper {#access-merge-policies}

Med hjälp av API:t för kundprofil i realtid kan du utföra en sökbegäran för att visa en specifik sammanfogningsprincip utifrån dess ID, eller få tillgång till alla sammanfogningsprinciper i IMS-organisationen, filtrerade efter specifika villkor. `/config/mergePolicies` Du kan också använda `/config/mergePolicies/bulk-get` slutpunkten för att hämta flera sammanfogningsprinciper efter deras ID:n. Steg för att utföra dessa anrop beskrivs i följande avsnitt.

### Åtkomst till en sammanfogningsprincip via ID

Du kan få åtkomst till en enskild sammanfogningsprincip via dess ID genom att göra en GET-begäran till `/config/mergePolicies` slutpunkten och inkludera den `mergePolicyId` i sökvägen för begäran.

**API-format**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beskrivning |
|---|---|
| `{mergePolicyId}` | Identifieraren för den sammanfogningsprincip som du vill ta bort. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Svar**

Ett lyckat svar returnerar information om sammanfogningsprincipen.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

I avsnittet [Komponenter för sammanfogningsprinciper](#components-of-merge-policies) i början av det här dokumentet finns mer information om de enskilda elementen som utgör en sammanfogningsprincip.

### Hämta flera sammanfogningsprinciper efter deras ID:n

Du kan hämta flera sammanfogningsprinciper genom att göra en POST-begäran till `/config/mergePolicies/bulk-get` slutpunkten och inkludera ID:n för de sammanfogningsprinciper som du vill hämta i begärandetexten.

**API-format**

```http
POST /config/mergePolicies/bulk-get
```

**Begäran**

Begärandetexten innehåller en &quot;ids&quot;-array med enskilda objekt som innehåller &quot;id&quot; för varje sammanfogningsprincip som du vill hämta information för.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 207 (Multi-Status) och information om de sammanfogningsprinciper vars ID:n angavs i POST-begäran.

```json
{
    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
    "name": "Profile Default Merge Policy",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": true,
    "updateEpoch": 1552086578
},
{
    "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
    "name": "Dataset Precedence Merge Policy",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": false,
    "updateEpoch": 1576099719
}
```

I avsnittet [Komponenter för sammanfogningsprinciper](#components-of-merge-policies) i början av det här dokumentet finns mer information om de enskilda elementen som utgör en sammanfogningsprincip.

### Lista flera sammanfogningsprinciper efter villkor

Du kan lista flera sammanfogningsprinciper inom IMS-organisationen genom att skicka en GET-begäran till `/config/mergePolicies` slutpunkten och använda valfria frågeparametrar för att filtrera, ordna och numrera svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (&amp;). Om du anropar den här slutpunkten utan parametrar hämtas alla kopplingsprofiler som är tillgängliga för organisationen.

**API-format**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
|---|---|
| `default` | Ett booleskt värde som filtrerar resultat genom att sammanfogningsprinciperna är standard för en schemaklass eller inte. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. Standardvärde: 20 |
| `orderBy` | Anger fältet som resultatet ska sorteras efter som i `orderBy=name` eller `orderBy=+name` sorteras efter namn i stigande ordning, eller `orderBy=-name`sorteras i fallande ordning. Om du utelämnar det här värdet sorteras standardvärdet i `name` stigande ordning. |
| `schema.name` | Namnet på schemat som tillgängliga sammanfogningsprinciper ska hämtas för. |
| `identityGraph.type` | Filtrerar resultat efter typen av identitetsdiagram. Möjliga värden är none och pdg (Private graph). |
| `attributeMerge.type` | Filtrerar resultat efter den attributsammanfogningstyp som används. Möjliga värden är &quot;timestampOrdered&quot; och &quot;dataSetPriedence&quot;. |
| `start` | Sidförskjutning - ange det första ID:t för data som ska hämtas. Standardvärde: 0 |
| `version` | Ange det här alternativet om du vill använda en specifik version av sammanfogningsprincipen. Som standard används den senaste versionen. |

Mer information om `schema.name`, `identityGraph.type`och `attributeMerge.type`finns i avsnittet [Komponenter i sammanfogningsprinciper](#components-of-merge-policies) som fanns tidigare i den här handboken.


**Begäran**

I följande begäran visas alla sammanfogningsprinciper för ett givet schema:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Svar**

Ett lyckat svar returnerar en numrerad lista med sammanfogningsprinciper som uppfyller villkoren som anges av frågeparametrarna som skickas i begäran.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Egenskap | Beskrivning |
|---|---|
| `_links.next.href` | En URI-adress för nästa resultatsida. Använd denna URI som begärandeparameter för ett annat API-anrop till samma slutpunkt för att visa sidan. Om det inte finns någon nästa sida blir värdet en tom sträng. |

## Skapa en kopplingsprofil

Du kan skapa en ny sammanfogningsprincip för din organisation genom att göra en POST-begäran till `/config/mergePolicies` slutpunkten.

**API-format**

```http
POST /config/mergePolicies
```

**Begäran** Följande begäran skapar en ny sammanfogningsprincip som konfigureras av attributvärdena i nyttolasten:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Egenskap | Beskrivning |
|---|---|
| `name` | Ett användarvänligt namn som sammanfogningsprincipen kan identifieras med i listvyer. |
| `identityGraph.type` | Identitetsdiagramtypen som relaterade identiteter ska sammanfogas från. Möjliga värden: &quot;none&quot; eller &quot;pdg&quot; (privat diagram). |
| `attributeMerge` | Sättet som profilattributvärden ska prioriteras på vid datakonflikter. |
| `schema` | Den XDM-schemaklass som är associerad med sammanfogningsprincipen. |
| `default` | Anger om den här sammanfogningsprincipen är standard för schemat. |

Mer information finns i avsnittet [Komponenter för sammanfogningsprinciper](#components-of-merge-policies) .

**Svar**

Ett lyckat svar returnerar information om den nya sammanfogningsprincipen.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

I avsnittet [Komponenter för sammanfogningsprinciper](#components-of-merge-policies) i början av det här dokumentet finns mer information om de enskilda elementen som utgör en sammanfogningsprincip.

## Uppdatera en sammanfogningsprincip {#update}

Du kan ändra en befintlig kopplingsprofil genom att redigera enskilda attribut (PATCH) eller genom att skriva över hela kopplingsprofilen med nya attribut (PUT). Nedan visas exempel på vart och ett av dem.

### Redigera enskilda kopplingsprincipfält

Du kan redigera enskilda fält för en sammanfogningsprincip genom att göra en PATCH-begäran till `/config/mergePolicies/{mergePolicyId}` slutpunkten:

**API-format**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beskrivning |
|---|---|
| `{mergePolicyId}` | Identifieraren för den sammanfogningsprincip som du vill ta bort. |

**Begäran**

Följande begäran uppdaterar en angiven sammanfogningsprincip genom att ändra värdet för dess `default` egenskap till `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Egenskap | Beskrivning |
|---|---|
| `op` | Anger vilken åtgärd som ska utföras. Exempel på andra PATCH-åtgärder finns i [JSON-patchdokumentationen](http://jsonpatch.com) |
| `path` | Sökvägen till det fält som ska uppdateras. Godkända värden är: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | Värdet som det angivna fältet ska anges till. |

Mer information finns i avsnittet [Komponenter för sammanfogningsprinciper](#components-of-merge-policies) .


**Svar**

Ett lyckat svar returnerar information om den nyligen uppdaterade sammanfogningsprincipen.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Skriv över en sammanfogningsprincip

Ett annat sätt att ändra en sammanfogningsprincip är att använda en PUT-begäran, som skriver över hela sammanfogningsprincipen.

**API-format**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beskrivning |
|---|---|
| `{mergePolicyId}` | Identifieraren för den sammanfogningsprincip som du vill skriva över. |

**Begäran**

Följande begäran skriver över den angivna sammanfogningsprincipen och ersätter dess attributvärden med dem som anges i nyttolasten. Eftersom den här begäran helt ersätter en befintlig sammanfogningsprincip måste du ange alla fält som krävdes när sammanfogningsprincipen ursprungligen definierades. Den här gången anger du dock uppdaterade värden för de fält som du vill ändra.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Egenskap | Beskrivning |
|---|---|
| `name` | Ett användarvänligt namn som sammanfogningsprincipen kan identifieras med i listvyer. |
| `identityGraph` | Det identitetsdiagram som relaterade identiteter ska sammanfogas från. |
| `attributeMerge` | Sättet som profilattributvärden ska prioriteras på vid datakonflikter. |
| `schema` | Den XDM-schemaklass som är associerad med sammanfogningsprincipen. |
| `default` | Anger om den här sammanfogningsprincipen är standard för schemat. |

Mer information finns i avsnittet [Komponenter för sammanfogningsprinciper](#components-of-merge-policies) .


**Svar**

Ett lyckat svar returnerar information om den uppdaterade sammanfogningsprincipen.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Ta bort en sammanfogningsprincip

Du kan ta bort en sammanfogningsprincip genom att göra en DELETE-begäran till `/config/mergePolicies` slutpunkten och inkludera ID:t för den sammanfogningsprincip som du vill ta bort i sökvägen till begäran.

**API-format**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beskrivning |
|---|---|
| `{mergePolicyId}` | Identifieraren för den sammanfogningsprincip som du vill ta bort. |

**Begäran**

Följande begäran tar bort en sammanfogningsprincip.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

En slutförd borttagningsbegäran returnerar HTTP-status 200 (OK) och en tom svarstext. För att bekräfta att borttagningen lyckades kan du utföra en GET-begäran för att visa sammanfogningsprincipen efter dess ID. Om sammanfogningsprincipen togs bort får du ett HTTP-statusfel 404 (Hittades inte).

## Nästa steg

Nu när du vet hur man skapar och konfigurerar sammanfogningsprinciper för IMS-organisationen kan du använda dem för att skapa målgruppssegment utifrån kundprofildata i realtid. Läs dokumentationen [till](../../segmentation/home.md) Adobe Experience Platform Segmentation Service om hur du börjar definiera och arbeta med segment.



