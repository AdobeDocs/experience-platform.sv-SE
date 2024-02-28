---
keywords: Experience Platform;startsida;populära ämnen;handbok för utvecklare av sandlådor
solution: Experience Platform
title: API-slutpunkt för sandlådehantering
description: Med slutpunkten /sandbox i sandbox-API kan du programmässigt hantera sandlådor i Adobe Experience Platform.
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 1%

---

# Slutpunkt för sandlådehantering

Sandlådor i Adobe Experience Platform har isolerade utvecklingsmiljöer där du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka produktionsmiljön. The `/sandboxes` slutpunkt i [!DNL Sandbox] Med API kan du programmässigt hantera sandlådor i plattformen.

## Komma igång

API-slutpunkten som används i den här guiden är en del av [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Innan du fortsätter bör du granska [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med sandlådor {#list}

Du kan lista alla sandlådor som tillhör din organisation (aktiv eller annan) genom att göra en GET-förfrågan till `/sandboxes` slutpunkt.

**API-format**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Se avsnittet om [frågeparametrar](./appendix.md#query) för mer information. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med sandlådor som tillhör din organisation, inklusive information som `name`, `title`, `state`och `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på sandlådan. Den här egenskapen används för uppslagssyften i API-anrop. |
| `title` | Visningsnamnet för sandlådan. |
| `state` | Sandlådans aktuella bearbetningstillstånd. En sandlådestatus kan vara något av följande: <br/><ul><li>`creating`: Sandlådan har skapats, men etableras fortfarande av systemet.</li><li>`active`: Sandlådan skapas och är aktiv.</li><li>`failed`: På grund av ett fel kunde sandlådan inte etableras av systemet och är inaktiverad.</li><li>`deleted`: Sandlådan har inaktiverats manuellt.</li></ul> |
| `type` | Sandlådetypen. De sandlådetyper som stöds för närvarande är `development` och `production`. |
| `isDefault` | En boolesk egenskap som anger om den här sandlådan är standardproduktionssandlådan för organisationen. |
| `eTag` | En identifierare för en specifik version av sandlådan. Detta värde används för versionskontroll och cachelagring av effektivitet och uppdateras varje gång en ändring görs i sandlådan. |

## Söka efter en sandlåda {#lookup}

Du kan söka efter en enskild sandlåda genom att göra en GET-begäran som innehåller sandlådans `name` i sökvägen för begäran.

**API-format**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | The `name` egenskapen för den sandlåda som du vill söka efter. |

**Begäran**

Följande begäran hämtar en sandlåda med namnet &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Svar**

Ett lyckat svar returnerar informationen om sandlådan, inklusive dess `name`, `title`, `state`och `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på sandlådan. Den här egenskapen används för uppslagssyften i API-anrop. |
| `title` | Visningsnamnet för sandlådan. |
| `state` | Sandlådans aktuella bearbetningstillstånd. En sandlådestatus kan vara något av följande: <ul><li>**skapa**: Sandlådan har skapats, men etableras fortfarande av systemet.</li><li>**aktiv**: Sandlådan skapas och är aktiv.</li><li>**misslyckades**: På grund av ett fel kunde sandlådan inte etableras av systemet och är inaktiverad.</li><li>**borttagen**: Sandlådan har inaktiverats manuellt.</li></ul> |
| `type` | Sandlådetypen. De sandlådetyper som stöds för närvarande är: `development` och `production`. |
| `isDefault` | En boolesk egenskap som anger om den här sandlådan är standardsandlådan för organisationen. Vanligtvis är det här produktionssandlådan. |
| `eTag` | En identifierare för en specifik version av sandlådan. Detta värde används för versionskontroll och cachelagring av effektivitet och uppdateras varje gång en ändring görs i sandlådan. |

## Skapa en sandlåda {#create}

>[!NOTE]
>
>När en ny sandlåda skapas måste du först lägga till den nya sandlådan i din produktprofil i [Adobe Admin Console](https://adminconsole.adobe.com/) innan du kan börja använda den nya sandlådan. Läs dokumentationen om [hantera behörigheter för en produktprofil](../../access-control/ui/permissions.md) om du vill ha information om hur du distribuerar en sandlåda till en produktprofil.

Du kan skapa en ny utvecklings- eller produktionssandlåda genom att göra en POST-förfrågan till `/sandboxes` slutpunkt.

### Skapa en utvecklingssandlåda

Om du vill skapa en utvecklingssandlåda måste du ange en `type` attribut med värdet `development` i nyttolasten för begäran.

**API-format**

```http
POST /sandboxes
```

**Begäran**

Följande begäran skapar en ny utvecklingssandlåda med namnet&quot;acme-dev&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Den identifierare som ska användas för att komma åt sandlådan i framtida begäranden. Detta värde måste vara unikt och det bästa sättet är att göra det så beskrivande som möjligt. Värdet får inte innehålla blanksteg eller specialtecken. |
| `title` | Ett läsbart namn som används för visning i användargränssnittet för plattformen. |
| `type` | Den typ av sandlåda som ska skapas. För en icke-produktionssandlåda måste värdet vara `development`. |

**Svar**

Ett lyckat svar returnerar informationen om den nya sandlådan, vilket visar att dess `state` är &quot;creating&quot;.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Sandlådor tar cirka 30 sekunder att tilldela av systemet, varefter deras `state` blir &quot;aktiv&quot; eller &quot;misslyckades&quot;.

### Skapa en produktionssandlåda

Om du vill skapa en produktionssandlåda måste du ange en `type` attribut med värdet `production` i nyttolasten för begäran.

**API-format**

```http
POST /sandboxes
```

**Begäran**

Följande begäran skapar en ny produktionssandlåda med namnet&quot;acme&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Den identifierare som ska användas för att komma åt sandlådan i framtida begäranden. Detta värde måste vara unikt och det bästa sättet är att göra det så beskrivande som möjligt. Värdet får inte innehålla blanksteg eller specialtecken. |
| `title` | Ett läsbart namn som används för visning i användargränssnittet för plattformen. |
| `type` | Den typ av sandlåda som ska skapas. För en produktionssandlåda måste värdet vara `production`. |

**Svar**

Ett lyckat svar returnerar informationen om den nya sandlådan, vilket visar att dess `state` är &quot;creating&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>Sandlådor tar cirka 30 sekunder att tilldela av systemet, varefter deras `state` blir &quot;aktiv&quot; eller &quot;misslyckades&quot;.

## Uppdatera en sandlåda {#put}

Du kan uppdatera ett eller flera fält i en sandlåda genom att göra en PATCH-begäran som innehåller sandlådans `name` i sökvägen till begäran och egenskapen som ska uppdateras i nyttolasten för begäran.

>[!NOTE]
>
>För närvarande är det bara en sandlåda `title` kan uppdateras.

**API-format**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | The `name` egenskapen för den sandlåda som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar `title` i sandlådan med namnet&quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) med information om den nyligen uppdaterade sandlådan.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Återställ en sandlåda {#reset}

Sandlådor har en &quot;fabriksåterställningsfunktion&quot; som tar bort alla icke-standardresurser från en sandlåda. Du kan återställa en sandlåda genom att göra en PUT-begäran som innehåller sandlådans `name` i sökvägen till begäran.

**API-format**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | The `name` egenskapen för den sandlåda som du vill återställa. |
| `validationOnly` | En valfri parameter som gör att du kan utföra en kontroll före flygning av sandlådeåterställningsåtgärden utan att göra den faktiska begäran. Ställ in den här parametern på `validationOnly=true` om du vill kontrollera om sandlådan du håller på att återställa innehåller Adobe Analytics-, Adobe Audience Manager- eller segmentdelningsdata. |

**Begäran**

Följande begäran återställer en sandlåda med namnet&quot;acme-dev&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `action` | Den här parametern måste anges med värdet &quot;reset&quot; i nyttolasten för begäran för att sandlådan ska kunna återställas. |

**Svar**

>[!NOTE]
>
>När en sandlåda har återställts tar det cirka 30 sekunder att etablera den av systemet.

Ett godkänt svar returnerar informationen om den uppdaterade sandlådan, vilket visar att `state` är &quot;resetting&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

Standardproduktionssandlådan och alla användarskapade produktionssandlådor kan inte återställas om identitetsdiagrammet som finns i den också används av Adobe Analytics för [CDA (Cross Device Analytics)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=sv) eller om identitetsdiagrammet som finns i det också används av Adobe Audience Manager för [Personbaserade mål (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=sv) -funktion.

Nedan följer en lista över möjliga undantag som kan förhindra att en sandlåda återställs:

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

Du kan återställa en produktionssandlåda som används för dubbelriktad segmentdelning med [!DNL Audience Manager] eller [!DNL Audience Core Service] genom att lägga till `ignoreWarnings` parameter till din begäran.

**API-format**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | The `name` egenskapen för den sandlåda som du vill återställa. |
| `ignoreWarnings` | En valfri parameter som gör att du kan hoppa över valideringskontrollen och tvinga fram återställningen av en produktionssandlåda som används för dubbelriktad segmentdelning med [!DNL Audience Manager] eller [!DNL Audience Core Service]. Den här parametern kan inte tillämpas på en standardproduktionssandlåda. |

**Begäran**

Följande begäran återställer en produktionssandlåda med namnet &quot;acme&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Svar**

Ett godkänt svar returnerar informationen om den uppdaterade sandlådan, vilket visar att `state` är &quot;resetting&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## Ta bort en sandlåda {#delete}

>[!IMPORTANT]
>
>Det går inte att ta bort standardproduktionssandlådan.

Du kan ta bort en sandlåda genom att göra en DELETE-begäran som innehåller sandlådans `name` i sökvägen till begäran.

>[!NOTE]
>
>Göra detta API-anrop uppdaterar sandlådans `status` egenskapen till&quot;deleted&quot; och inaktiverar den. GET-begäranden kan fortfarande hämta sandlådans information efter att den har tagits bort.

**API-format**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SANDBOX_NAME}` | The `name` för den sandlåda som du vill ta bort. |
| `validationOnly` | En valfri parameter som gör att du kan utföra en kontroll före flygning av sandlådeborttagningsåtgärden utan att göra den faktiska begäran. Ställ in den här parametern på `validationOnly=true` om du vill kontrollera om sandlådan du håller på att återställa innehåller Adobe Analytics-, Adobe Audience Manager- eller segmentdelningsdata. |
| `ignoreWarnings` | En valfri parameter som gör att du kan hoppa över valideringskontrollen och framtvinga borttagning av en användarskapad produktionssandlåda som används för dubbelriktad segmentdelning med [!DNL Audience Manager] eller [!DNL Audience Core Service]. Den här parametern kan inte tillämpas på en standardproduktionssandlåda. |

**Begäran**

Följande begäran tar bort en produktionssandlåda med namnet &quot;acme&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar sandlådans uppdaterade information, vilket visar att dess `state` är &quot;deleted&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
