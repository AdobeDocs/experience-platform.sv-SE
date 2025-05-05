---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: API-slutpunkt för sammanslagningsprinciper
type: Documentation
description: Med Adobe Experience Platform kan ni sammanföra datafragment från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanför dessa data är sammanslagningsprinciper de regler som Experience Platform använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa en enhetlig vy.
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 0%

---

# Slutpunkt för sammanslagningsprinciper

Med Adobe Experience Platform kan ni sammanföra datafragment från flera olika källor och kombinera dem för att få en fullständig bild av varje enskild kund. När du sammanfogar dessa data är sammanfogningsprinciper de regler som [!DNL Experience Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa en enhetlig vy.

Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera profilfragment som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Experience Platform sammanfogas de för att skapa en enda profil för kunden. När data från flera källor står i konflikt (t.ex. ett fragment listar kunden som&quot;enkel&quot; medan det andra listar kunden som&quot;gift&quot;) avgör sammanfogningspolicyn vilken information som ska inkluderas i profilen för den enskilda personen.

Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Den här handboken innehåller steg för hur du arbetar med sammanfogningsprinciper med API:t.

Information om hur du arbetar med sammanfogningsprinciper med hjälp av användargränssnittet finns i [användargränssnittshandboken för sammanfogningsprinciper](../merge-policies/ui-guide.md). Om du vill veta mer om sammanfogningsprinciper i allmänhet och deras roll i Experience Platform kan du börja med att läsa översikten [för sammanfogningsprinciper](../merge-policies/overview.md).

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett [!DNL Experience Platform] -API.

## Komponenter i sammanfogningsprinciper {#components-of-merge-policies}

Sammanslagningsprinciper är privata för din organisation, vilket gör att du kan skapa olika profiler för att sammanfoga scheman på de specifika sätt som du behöver. Alla API:er som har åtkomst till [!DNL Profile]-data kräver en sammanfogningsprincip, men ett standardvärde kommer att användas om det inte uttryckligen anges. [!DNL Experience Platform] innehåller en standardsammanfogningsprincip för organisationer, eller så kan du skapa en sammanfogningsprincip för en specifik XDM-schemaklass (Experience Data Model) och markera den som standard för din organisation.

Även om varje organisation kan ha flera sammanfogningsprinciper per per schemaklass, kan varje klass bara ha en standardsammanfogningsprincip. Alla sammanfogningsprinciper som anges som standard används om namnet på schemaklassen anges och en sammanfogningsprincip krävs men inte anges.

>[!NOTE]
>
>När du anger en ny sammanfogningsprincip som standard uppdateras automatiskt alla befintliga sammanfogningsprinciper som tidigare var inställda som standard så att de inte längre används som standard.

För att säkerställa att alla profilkonsumenter arbetar med samma vy på kanterna kan sammanfogningsprinciper markeras som aktiva på kanten. För att en målgrupp ska kunna aktiveras på kanten (markeras som en målgrupp) måste den vara kopplad till en sammanfogningspolicy som är markerad som aktiv på kanten. Om en målgrupp **inte** är kopplad till en sammanfogningsprincip som är markerad som aktiv i kant, markeras målgruppen inte som aktiv i kant och markeras som en målgrupp för direktuppspelning.

Dessutom kan varje organisation bara ha **en**-sammanslagningsprincip som är aktiv i kant. Om en sammanfogningsprincip är aktiv vid sidan kan den användas för andra system vid sidan, t.ex. Edge-profil, Edge-segmentering och mål på Edge.

### Slutför policyobjekt för sammanfogning

Det fullständiga principobjektet för sammanfogning representerar en uppsättning inställningar som styr aspekter av sammanfogning av profilfragment.

**Kopplingsprincipobjekt**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Egenskap | Beskrivning |
|---|---|
| `id` | Den systemgenererade unika identifieraren som tilldelats vid skapandetillfället |
| `name` | Eget namn som sammanfogningsprincipen kan identifieras med i listvyer. |
| `imsOrgId` | Organisations-ID som den här sammanfogningsprincipen tillhör |
| `schema.name` | Som en del av objektet [`schema`](#schema) innehåller fältet `name` XDM-schemaklassen som sammanfogningsprincipen relaterar till. Mer information om scheman och klasser finns i [XDM-dokumentationen](../../xdm/home.md). |
| `version` | [!DNL Experience Platform] bevarade versionen av sammanfogningsprincipen. Det här skrivskyddade värdet ökas stegvis när en sammanfogningsprincip uppdateras. |
| `identityGraph` | [Identitetsdiagramobjekt](#identity-graph) som anger identitetsdiagrammet som relaterade identiteter ska hämtas från. Profilfragment som hittas för alla relaterade identiteter sammanfogas. |
| `attributeMerge` | [Attributsammanslagningsobjekt](#attribute-merge) anger hur sammanfogningsprincipen prioriterar profilattribut vid datakonflikter. |
| `isActiveOnEdge` | Booleskt värde som anger om sammanfogningsprincipen kan användas på kanten. Standardvärdet är `false`. |
| `default` | Booleskt värde som anger om den här sammanfogningsprincipen är standard för det angivna schemat. |
| `updateEpoch` | Datum för den senaste uppdateringen av sammanfogningsprincipen. |

**Exempel på sammanfogningsprincip**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Identitetsdiagram {#identity-graph}

[Adobe Experience Platform identitetstjänst](../../identity-service/home.md) hanterar de identitetsdiagram som används globalt och för varje organisation på [!DNL Experience Platform]. Attributet `identityGraph` för sammanfogningsprincipen definierar hur relaterade identiteter för en användare ska fastställas.

**identityGraph-objekt**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Där `{IDENTITY_GRAPH_TYPE}` är något av följande:

* **&quot;ingen&quot;:** Utför ingen identitetssammanfogning.
* **&quot;pdg&quot;:** Utför identitetssammanfogning baserat på ditt privata identitetsdiagram.

**Exempel`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Koppla attribut {#attribute-merge}

Ett profilfragment är profilinformationen för endast en identitet från listan över identiteter som finns för en viss användare. När typen av identitetsdiagram som används resulterar i mer än en identitet, finns det en risk för att profilattribut som står i konflikt med varandra, och prioritet måste anges. Med `attributeMerge` kan du ange vilka profilattribut som ska prioriteras i händelse av en sammanslagningskonflikt mellan datamängder av typen nyckelvärde (postdata).

**attributeMerge-objekt**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Där `{ATTRIBUTE_MERGE_TYPE}` är något av följande:

* **`timestampOrdered`**: (standard) Prioritera den profil som uppdaterades senast. Attributet `data` krävs inte med den här sammanfogningstypen.
* **`dataSetPrecedence`**: Prioritera profilfragment baserat på den datauppsättning som de kommer från. Detta kan användas när information som finns i en datauppsättning är att föredra eller betrodd framför data i en annan datauppsättning. När du använder den här sammanfogningstypen krävs attributet `order` eftersom datamängderna visas i prioritetsordning.
   * **`order`**: När&quot;dataSetPriedence&quot; används måste en `order`-matris anges med en lista över datauppsättningar. Datauppsättningar som inte ingår i listan kommer inte att sammanfogas. Datamängder måste med andra ord anges explicit för att sammanfogas till en profil. `order`-arrayen visar datauppsättningens ID i prioritetsordning.

#### Exempel på `attributeMerge`-objekt som använder typen `dataSetPrecedence`

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### Exempel på `attributeMerge`-objekt som använder typen `timestampOrdered`

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Schemaobjektet anger XDM-schemaklassen (Experience Data Model) som sammanfogningsprincipen skapas för.

**`schema`objekt**

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

Om du vill veta mer om XDM och arbeta med scheman i Experience Platform börjar du med att läsa [systemöversikten för XDM](../../xdm/home.md).

## Åtkomst till sammanfogningsprinciper {#access-merge-policies}

Med API:t [!DNL Real-Time Customer Profile] kan du med slutpunkten `/config/mergePolicies` utföra en sökbegäran för att visa en specifik sammanfogningsprincip utifrån dess ID, eller få åtkomst till alla sammanfogningsprinciper i organisationen, filtrerade efter specifika villkor. Du kan också använda slutpunkten `/config/mergePolicies/bulk-get` för att hämta flera sammanfogningsprinciper efter deras ID:n. Steg för att utföra dessa anrop beskrivs i följande avsnitt.

### Åtkomst till en sammanfogningsprincip via ID

Du kan få åtkomst till en enskild sammanfogningsprincip via dess ID genom att göra en GET-begäran till `/config/mergePolicies`-slutpunkten och inkludera `mergePolicyId` i sökvägen för begäran.

**API-format**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beskrivning |
|---|---|
| `{mergePolicyId}` | Identifieraren för den sammanslagningsprincip som du vill ta bort. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Svar**

Ett lyckat svar returnerar information om sammanfogningsprincipen.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

I avsnittet [komponenter för sammanfogningsprinciper](#components-of-merge-policies) i början av det här dokumentet finns mer information om de enskilda elementen som utgör en sammanfogningsprincip.

### Hämta flera sammanfogningsprinciper efter deras ID:n

Du kan hämta flera sammanfogningsprinciper genom att göra en POST-begäran till `/config/mergePolicies/bulk-get`-slutpunkten och inkludera ID:n för de sammanfogningsprinciper som du vill hämta i begärandetexten.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

I avsnittet [komponenter för sammanfogningsprinciper](#components-of-merge-policies) i början av det här dokumentet finns mer information om de enskilda elementen som utgör en sammanfogningsprincip.

### Lista flera sammanfogningsprinciper efter villkor

Du kan lista flera sammanfogningsprinciper inom organisationen genom att skicka en GET-begäran till slutpunkten `/config/mergePolicies` och använda valfria frågeparametrar för att filtrera, ordna och numrera svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (&amp;). Om du anropar den här slutpunkten utan parametrar hämtas alla kopplingsprofiler som är tillgängliga för organisationen.

**API-format**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
|---|---|
| `default` | Ett booleskt värde som filtrerar resultat genom att sammanfogningsprinciperna är standard för en schemaklass eller inte. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. Standardvärde: 20 |
| `orderBy` | Anger fältet som resultatet ska sorteras efter, som i `orderBy=name` eller `orderBy=+name`, för att sortera efter namn i stigande ordning, eller `orderBy=-name` för att sortera i fallande ordning. Om det här värdet utelämnas sorteras `name` som standard i stigande ordning. |
| `isActiveOnEdge` | Ett booleskt värde som filtrerar resulterar i om sammanfogningsprinciperna är aktiva på kanten eller inte. |
| `schema.name` | Namnet på schemat som tillgängliga sammanfogningsprinciper ska hämtas för. |
| `identityGraph.type` | Filtrerar resultat efter typen av identitetsdiagram. Möjliga värden är none och pdg (Private graph). |
| `attributeMerge.type` | Filtrerar resultat efter den attributsammanfogningstyp som används. Möjliga värden är &quot;timestampOrdered&quot; och &quot;dataSetPriedence&quot;. |
| `start` | Sidförskjutning - ange det första ID:t för data som ska hämtas. Standardvärde: 0 |
| `version` | Ange det här alternativet om du vill använda en specifik version av sammanfogningsprincipen. Som standard används den senaste versionen. |

Mer information om `schema.name`, `identityGraph.type` och `attributeMerge.type` finns i avsnittet [komponenter i sammanfogningsprinciper](#components-of-merge-policies) som fanns tidigare i den här handboken.


**Begäran**

I följande begäran visas alla sammanfogningsprinciper för ett givet schema:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
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

## Skapa en sammanfogningsprincip

Du kan skapa en ny sammanfogningsprincip för din organisation genom att göra en POST-begäran till slutpunkten `/config/mergePolicies`.

**API-format**

```http
POST /config/mergePolicies
```

**Begäran**
I följande begäran skapas en ny sammanfogningsprincip som konfigureras av attributvärdena i nyttolasten:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| Egenskap | Beskrivning |
|---|---|
| `name` | Ett användarvänligt namn som sammanfogningsprincipen kan identifieras med i listvyer. |
| `identityGraph.type` | Identitetsdiagramtypen som relaterade identiteter ska sammanfogas från. Möjliga värden: &quot;none&quot; eller &quot;pdg&quot; (privat diagram). |
| `attributeMerge` | Sättet som profilattributvärden ska prioriteras på vid datakonflikter. |
| `schema` | Den XDM-schemaklass som är associerad med sammanfogningsprincipen. |
| `isActiveOnEdge` | Anger om den här sammanfogningsprincipen är aktiv vid kant. |
| `default` | Anger om den här sammanfogningsprincipen är standard för schemat. |

Mer information finns i avsnittet [komponenter för sammanfogningsprinciper](#components-of-merge-policies).

**Svar**

Ett lyckat svar returnerar information om den nya sammanfogningsprincipen.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

I avsnittet [komponenter för sammanfogningsprinciper](#components-of-merge-policies) i början av det här dokumentet finns mer information om de enskilda elementen som utgör en sammanfogningsprincip.

## Uppdatera en sammanfogningsprincip {#update}

Du kan ändra en befintlig kopplingsprofil genom att redigera enskilda attribut (PATCH) eller genom att skriva över hela kopplingsprofilen med nya attribut (PUT). Nedan visas exempel på vart och ett av dem.

### Redigera enskilda kopplingsprincipfält

Du kan redigera enskilda fält för en sammanfogningsprincip genom att göra en PATCH-begäran till slutpunkten `/config/mergePolicies/{mergePolicyId}`:

**API-format**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beskrivning |
|---|---|
| `{mergePolicyId}` | Identifieraren för den sammanslagningsprincip som du vill ta bort. |

**Begäran**

Följande begäran uppdaterar en angiven sammanfogningsprincip genom att ändra värdet för egenskapen `default` till `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Anger vilken åtgärd som ska utföras. Exempel på andra PATCH-åtgärder finns i [JSON Patch-dokumentationen](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | Sökvägen till det fält som ska uppdateras. Godkända värden är: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | Värdet som det angivna fältet ska anges till. |

Mer information finns i avsnittet [komponenter för sammanfogningsprinciper](#components-of-merge-policies).


**Svar**

Ett lyckat svar returnerar information om den nyligen uppdaterade sammanfogningsprincipen.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### Skriv över en sammanfogningsprincip

Ett annat sätt att ändra en kopplingsprofil är att använda en PUT-begäran, som skriver över hela kopplingsprofilen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": true,
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
| `isActiveOnEdge` | Anger om den här sammanfogningsprincipen är aktiv vid kant. |
| `default` | Anger om den här sammanfogningsprincipen är standard för schemat. |

Mer information finns i avsnittet [komponenter för sammanfogningsprinciper](#components-of-merge-policies).

**Svar**

Ett lyckat svar returnerar information om den uppdaterade sammanfogningsprincipen.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## Ta bort en sammanfogningsprincip

Du kan ta bort en sammanfogningsprincip genom att göra en DELETE-begäran till `/config/mergePolicies`-slutpunkten och inkludera ID:t för den sammanfogningsprincip som du vill ta bort i sökvägen för begäran.

>[!NOTE]
>
>Om sammanfogningsprincipen har `isActiveOnEdge` inställt på true går det inte att ta bort sammanfogningsprincipen **&#x200B;**. Använd slutpunkterna [PATCH](#edit-individual-merge-policy-fields) eller [PUT](#overwrite-a-merge-policy) för att uppdatera sammanfogningsprincipen innan du tar bort den.

**API-format**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beskrivning |
|---|---|
| `{mergePolicyId}` | Identifieraren för den sammanslagningsprincip som du vill ta bort. |

**Begäran**

Följande begäran tar bort en sammanfogningsprincip.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

En slutförd borttagningsbegäran returnerar HTTP-status 200 (OK) och en tom svarstext. Du kan bekräfta att borttagningen lyckades genom att utföra en GET-begäran och visa sammanfogningsprincipen med dess ID. Om sammanfogningsprincipen togs bort får du ett HTTP-statusfel 404 (Hittades inte).

## Nästa steg

Nu när du vet hur du skapar och konfigurerar sammanfogningsprinciper för din organisation kan du använda dem för att justera visningen av kundprofiler i Experience Platform och för att skapa målgrupper utifrån dina [!DNL Real-Time Customer Profile]-data.

Se [dokumentationen för Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md) för att börja definiera och arbeta med målgrupper.
