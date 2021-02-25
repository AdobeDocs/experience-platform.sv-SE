---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: API-slutpunkt för beräknade attribut
topic: guide
type: Dokumentation
description: I Adobe Experience Platform är beräknade attribut funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Den här guiden visar hur du skapar, visar, uppdaterar och tar bort beräknade attribut med kundprofils-API:t i realtid.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 0%

---


# (Alfa) API-slutpunkt för beräknade attribut

>[!IMPORTANT]
>
>Den beräknade attributfunktionen som beskrivs i det här dokumentet är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Den här guiden innehåller exempel på API-anrop för att utföra grundläggande CRUD-åtgärder med `/computedAttributes`-slutpunkten.

Om du vill veta mer om beräknade attribut börjar du med att läsa översikten [beräknade attribut](overview.md).

## Komma igång

API-slutpunkten som används i den här guiden ingår i [Kundprofils-API:t för realtid](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Innan du fortsätter bör du läsa [guiden Komma igång med profil-API](../api/getting-started.md) för att få länkar till rekommenderad dokumentation, en guide till hur du läser de exempel på API-anrop som visas i det här dokumentet samt viktig information om vilka huvuden som krävs för att kunna anropa något Experience Platform-API.

## Konfigurera ett beräknat attributfält

För att kunna skapa ett beräknat attribut måste du först identifiera fältet i ett schema som innehåller det beräknade attributvärdet.

Se dokumentationen om [hur du konfigurerar ett beräknat attribut](configure-api.md) för en fullständig guide för att skapa ett beräknat attributfält i ett schema.

>[!WARNING]
>
>Om du vill fortsätta med API-guiden måste du ha ett beräknat attributfält konfigurerat.

## Skapa ett beräknat attribut {#create-a-computed-attribute}

Med ditt beräknade attributfält definierat i ditt profilaktiverade schema kan du nu konfigurera ett beräknat attribut. Om du inte redan har gjort det följer du arbetsflödet som beskrivs i [Konfigurera ett beräknat attribut](configure-api.md)-dokumentationen.

Om du vill skapa ett beräknat attribut börjar du med att göra en begäran om POST till `/config/computedAttributes`-slutpunkten med en begärandetext som innehåller information om det beräknade attributet som du vill skapa.

**API-format**

```http
POST /config/computedAttributes
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `name` | Namnet på det beräknade attributfältet, som en sträng. |
| `path` | Sökvägen till fältet som innehåller det beräknade attributet. Sökvägen finns i attributet `properties` för schemat och ska INTE innehålla fältnamnet i sökvägen. När du skriver sökvägen utelämnar du de olika nivåerna för `properties`-attribut. |
| `{TENANT_ID}` | Om du inte känner till ditt klient-ID läser du stegen för att hitta ditt klient-ID i [Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | En beskrivning av det beräknade attributet. Detta är särskilt användbart när flera beräknade attribut har definierats, eftersom det kommer att hjälpa andra inom IMS-organisationen att fastställa rätt beräknat attribut att använda. |
| `expression.value` | Ett giltigt [!DNL Profile Query Language]-uttryck (PQL). Beräknade attribut har för närvarande stöd för följande funktioner: sum, count, min, max och boolesk. En lista med exempeluttryck finns i [exempeldokumentationen för PQL-uttryck](expressions.md). |
| `schema.name` | Den klass som schemat som innehåller det beräknade attributfältet baseras på. Exempel: `_xdm.context.experienceevent` för ett schema baserat på klassen XDM ExperienceEvent. |

**Svar**

Ett beräknat attribut som skapats returnerar HTTP-status 200 (OK) och en svarstext som innehåller information om det nya beräknade attributet. Dessa uppgifter innehåller en unik, skrivskyddad, systemgenererad `id` som kan användas för att referera till det beräknade attributet under andra API-åtgärder.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Egenskap | Beskrivning |
|---|---|
| `id` | Ett unikt, skrivskyddat, systemgenererat ID som kan användas för att referera till det beräknade attributet under andra API-åtgärder. |
| `imsOrgId` | IMS-organisationen som är relaterad till det beräknade attributet ska matcha värdet som skickades i begäran. |
| `sandbox` | Sandlådeobjektet innehåller information om den sandlåda som det beräknade attributet konfigurerades i. Den här informationen hämtas från sandlådehuvudet som skickas i begäran. Mer information finns i [översikten över sandlådor](../../sandboxes/home.md). |
| `positionPath` | En array som innehåller det dekonstruerade `path` till fältet som skickades i begäran. |
| `returnSchema.meta:xdmType` | Den typ av fält där det beräknade attributet ska lagras. |
| `definedOn` | En array som visar de föreningsscheman som det beräknade attributet har definierats på. Innehåller ett objekt per union-schema, vilket innebär att det kan finnas flera objekt i arrayen om det beräknade attributet har lagts till i flera scheman baserade på olika klasser. |
| `active` | Ett booleskt värde som visar om det beräknade attributet är aktivt eller inte. Som standard är värdet `true`. |
| `type` | Den typ av resurs som skapas, i det här fallet är &quot;ComputedAttribute&quot; standardvärdet. |
| `createEpoch` och `updateEpoch` | Den tidpunkt då det beräknade attributet skapades och senast uppdaterades. |

## Skapa ett beräknat attribut som refererar till befintliga beräknade attribut

Det går också att skapa ett beräknat attribut som refererar till befintliga beräknade attribut. Börja med att göra en POST-förfrågan till `/config/computedAttributes`-slutpunkten. Begärandetexten innehåller referenser till de beräknade attributen i fältet `expression.value`, vilket visas i följande exempel.

**API-format**

```http
POST /config/computedAttributes
```

**Begäran**

I det här exemplet har två beräknade attribut redan skapats och kommer att användas för att definiera en tredje. De befintliga beräknade attributen är:

* **`totalSpend`:** Fångar hela dollarbeloppet som en kund har spenderat.
* **`countPurchases`:** Räknar antalet inköp som en kund har gjort.

Begäran nedan refererar till de två befintliga beräknade attributen och använder en giltig PQL för att dividera för att beräkna det nya `averageSpend` beräknade attributet.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `name` | Namnet på det beräknade attributfältet, som en sträng. |
| `path` | Sökvägen till fältet som innehåller det beräknade attributet. Sökvägen finns i attributet `properties` för schemat och ska INTE innehålla fältnamnet i sökvägen. När du skriver sökvägen utelämnar du de olika nivåerna för `properties`-attribut. |
| `{TENANT_ID}` | Om du inte känner till ditt klient-ID läser du stegen för att hitta ditt klient-ID i [Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | En beskrivning av det beräknade attributet. Detta är särskilt användbart när flera beräknade attribut har definierats, eftersom det kommer att hjälpa andra inom IMS-organisationen att fastställa rätt beräknat attribut att använda. |
| `expression.value` | Ett giltigt PQL-uttryck. Beräknade attribut har för närvarande stöd för följande funktioner: sum, count, min, max och boolesk. En lista med exempeluttryck finns i [exempeldokumentationen för PQL-uttryck](expressions.md).<br/><br/>I det här exemplet refererar uttrycket till två befintliga beräknade attribut. Attributen refereras med `path` och `name` för det beräknade attributet så som de visas i det schema i vilket de beräknade attributen definierades. Till exempel är `path` för det första refererade beräknade attributet `_{TENANT_ID}.purchaseSummary` och `name` `totalSpend`. |
| `schema.name` | Den klass som schemat som innehåller det beräknade attributfältet baseras på. Exempel: `_xdm.context.experienceevent` för ett schema baserat på klassen XDM ExperienceEvent. |

**Svar**

Ett beräknat attribut som skapats returnerar HTTP-status 200 (OK) och en svarstext som innehåller information om det nya beräknade attributet. Dessa uppgifter innehåller en unik, skrivskyddad, systemgenererad `id` som kan användas för att referera till det beräknade attributet under andra API-åtgärder.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| Egenskap | Beskrivning |
|---|---|
| `id` | Ett unikt, skrivskyddat, systemgenererat ID som kan användas för att referera till det beräknade attributet under andra API-åtgärder. |
| `imsOrgId` | IMS-organisationen som är relaterad till det beräknade attributet ska matcha värdet som skickades i begäran. |
| `sandbox` | Sandlådeobjektet innehåller information om den sandlåda som det beräknade attributet konfigurerades i. Den här informationen hämtas från sandlådehuvudet som skickas i begäran. Mer information finns i [översikten över sandlådor](../../sandboxes/home.md). |
| `positionPath` | En array som innehåller det dekonstruerade `path` till fältet som skickades i begäran. |
| `returnSchema.meta:xdmType` | Den typ av fält där det beräknade attributet ska lagras. |
| `definedOn` | En array som visar de föreningsscheman som det beräknade attributet har definierats på. Innehåller ett objekt per union-schema, vilket innebär att det kan finnas flera objekt i arrayen om det beräknade attributet har lagts till i flera scheman baserade på olika klasser. |
| `active` | Ett booleskt värde som visar om det beräknade attributet är aktivt eller inte. Som standard är värdet `true`. |
| `type` | Den typ av resurs som skapas, i det här fallet är &quot;ComputedAttribute&quot; standardvärdet. |
| `createEpoch` och `updateEpoch` | Den tidpunkt då det beräknade attributet skapades och senast uppdaterades. |

## Få åtkomst till beräknade attribut

När du arbetar med beräknade attribut med API:t finns det två alternativ för att komma åt beräknade attribut som har definierats av din organisation. Det första är att lista alla beräknade attribut, det andra är att visa ett specifikt beräknat attribut med dess unika `id`.

Steg för båda åtkomstmönstren beskrivs i det här dokumentet. Välj något av följande för att börja:

* **[Lista alla befintliga beräknade attribut](#list-all-computed-attributes):** Returnera en lista med alla befintliga beräknade attribut som din organisation har skapat.
* **[Visa ett specifikt beräknat attribut](#view-a-computed-attribute):** Returnera information om ett enskilt beräknat attribut genom att ange dess ID under begäran.

### Visa alla beräknade attribut {#list-all-computed-attributes}

IMS-organisationen kan skapa flera beräknade attribut, och om du utför en GET-begäran till `/config/computedAttributes`-slutpunkten kan du visa alla befintliga beräknade attribut för din organisation.

**API-format**

```http
GET /config/computedAttributes
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett svar innehåller ett `_page`-attribut som anger det totala antalet beräknade attribut (`totalCount`) och antalet beräknade attribut på sidan (`pageSize`).

Svaret innehåller också en `children`-array som består av ett eller flera objekt, där var och en innehåller information om ett beräknat attribut. Om din organisation inte har några beräknade attribut kommer `totalCount` och `pageSize` att vara 0 (noll) och `children`-arrayen att vara tom.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Egenskap | Beskrivning |
|---|---|
| `_page.totalCount` | Det totala antalet beräknade attribut som definieras av IMS-organisationen. |
| `_page.pageSize` | Antalet beräknade attribut som returneras på den här resultatsidan. Om `pageSize` är lika med `totalCount` betyder det att det bara finns en resultatsida och att alla beräknade attribut har returnerats. Om de inte är lika finns det ytterligare resultatsidor som du kan komma åt. Mer information finns i `_links.next`. |
| `children` | En array som består av ett eller flera objekt, där vart och ett innehåller detaljerna för ett enskilt beräknat attribut. Om inga beräknade attribut har definierats är `children`-arrayen tom. |
| `id` | Ett unikt, skrivskyddat, systemgenererat värde som automatiskt tilldelas ett beräknat attribut när det skapas. Mer information om komponenterna i ett beräknat attributobjekt finns i avsnittet [skapa ett beräknat attribut](#create-a-computed-attribute) tidigare i den här självstudiekursen. |
| `_links.next` | Om en enda sida med beräknade attribut returneras är `_links.next` ett tomt objekt, vilket visas i exempelsvaret ovan. Om din organisation har många beräknade attribut returneras de på flera sidor som du kan komma åt genom att göra en GET-begäran till `_links.next`-värdet. |

### Visa ett beräknat attribut {#view-a-computed-attribute}

Du kan visa ett specifikt beräknat attribut genom att göra en GET-begäran till `/config/computedAttributes`-slutpunkten och inkludera det beräknade attribut-ID:t i begärandesökvägen.

**API-format**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{ATTRIBUTE_ID}` | ID:t för det beräknade attribut som du vill visa. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Uppdatera ett beräknat attribut

Om du upptäcker att du behöver uppdatera ett befintligt beräknat attribut kan du göra det genom att göra en PATCH-begäran till `/config/computedAttributes`-slutpunkten och inkludera ID:t för det beräknade attribut som du vill uppdatera i sökvägen till begäran.

**API-format**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{ATTRIBUTE_ID}` | ID:t för det beräknade attribut som du vill uppdatera. |

**Begäran**

I den här begäran används [JSON Patch-formatering](http://jsonpatch.com/) för att uppdatera värdet i uttrycksfältet.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Egenskap | Beskrivning |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Ett giltigt [!DNL Profile Query Language]-uttryck (PQL). Beräknade attribut har för närvarande stöd för följande funktioner: sum, count, min, max och boolesk. En lista med exempeluttryck finns i [exempeldokumentationen för PQL-uttryck](expressions.md). |

**Svar**

En lyckad uppdatering returnerar HTTP-status 204 (inget innehåll) och en tom svarstext. Om du vill bekräfta att uppdateringen lyckades kan du utföra en GET-förfrågan för att visa det beräknade attributet med dess ID.

## Ta bort ett beräknat attribut

Det går också att ta bort ett beräknat attribut med API:t. Detta gör du genom att göra en DELETE-begäran till `/config/computedAttributes`-slutpunkten och inkludera ID:t för det beräknade attributet som du vill ta bort i begärandesökvägen.

>[!NOTE]
>
>Var försiktig när du tar bort ett beräknat attribut eftersom det kan användas i mer än ett schema och åtgärden DELETE inte kan ångras.

**API-format**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{ATTRIBUTE_ID}` | ID:t för det beräknade attribut som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Svar**

En slutförd borttagningsbegäran returnerar HTTP-status 200 (OK) och en tom svarstext. För att bekräfta att borttagningen lyckades kan du utföra en GET-begäran för att söka efter det beräknade attributet med dess ID. Om attributet har tagits bort får du ett HTTP Status 404-fel (Hittades inte).

## Skapa en segmentdefinition som refererar till ett beräknat attribut

Med Adobe Experience Platform kan du skapa segment som definierar en grupp med specifika attribut eller beteenden från en grupp profiler. En segmentdefinition innehåller ett uttryck som kapslar in en fråga skriven i PQL. Dessa uttryck kan också referera till beräknade attribut.

I följande exempel skapas en segmentdefinition som refererar till ett befintligt beräknat attribut. Mer information om segmentdefinitioner och hur du arbetar med dem i segmenteringstjänstens API finns i [API-slutpunktshandboken för segmentdefinitioner](../../segmentation/api/segment-definitions.md).

Börja med att göra en begäran om POST till `/segment/definitions`-slutpunkten, som tillhandahåller det beräknade attributet i begärandetexten.

**API-format**

```http
POST /segment/definitions
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Ett unikt namn för segmentet, som en sträng. |
| `description` | En läsbar beskrivning av definitionen. |
| `schema.name` | Det schema som är associerat med entiteterna i segmentet. Består av antingen ett `id`- eller `name`-fält. |
| `expression` | Ett objekt som innehåller fält med information om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara PQL. |
| `expression.format` | Anger strukturen för uttrycket i värdet. För närvarande stöds bara `pql/text`. |
| `expression.value` | Ett giltigt PQL-uttryck, i det här exemplet innehåller det en referens till ett befintligt beräknat attribut. |

Mer information om schemadefinitionsattribut finns i exemplen i [API-slutpunktshandboken för segmentdefinitioner](../../segmentation/api/segment-definitions.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den segmentdefinition du nyss skapade. Mer information om svarsåtgärder för segmentdefinitioner finns i [API-slutpunktshandboken för segmentdefinitioner](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## Nästa steg

Nu när du har lärt dig grunderna i beräknade attribut kan du börja definiera dem för din organisation.