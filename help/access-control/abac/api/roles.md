---
keywords: Experience Platform;hem;populära ämnen;api;Attributbaserad åtkomstkontroll;attributbaserad åtkomstkontroll
solution: Experience Platform
title: Roller API-slutpunkt
description: Med slutpunkten /roles i det attributbaserade åtkomstkontrolls-API:t kan du programmässigt hantera roller i Adobe Experience Platform.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---

# Rollslutpunkt

>[!NOTE]
>
>Om en användartoken skickas måste användaren av token ha rollen&quot;org admin&quot; för den begärda organisationen.

Roller definierar åtkomsten som en administratör, en specialist eller en slutanvändare har till resurser i organisationen. I en rollbaserad miljö för åtkomstkontroll är etableringen av användaråtkomst grupperad genom vanliga ansvarsområden och behov. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilket synområde eller vilken skrivbehörighet de behöver.

The `/roles` -slutpunkten i det attributbaserade API:t för åtkomstkontroll gör att du kan hantera roller i organisationen programmatiskt.

## Komma igång

API-slutpunkten som används i den här guiden är en del av det attributbaserade API:t för åtkomstkontroll. Innan du fortsätter bör du granska [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med roller {#list}

Du kan visa alla befintliga roller som tillhör din organisation genom att göra en GET-förfrågan till `/roles` slutpunkt.

**API-format**

```http
GET /roles/
```

**Begäran**

Följande begäran hämtar en lista över roller som tillhör din organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett godkänt svar returnerar en lista med roller i organisationen, inklusive information om deras respektive rolltyp, behörighetsgrupper och ämnesattribut.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar rollen. Detta ID genereras automatiskt. |
| `name` | Namnet på din roll. |
| `description` | Egenskapen description innehåller ytterligare information om din roll. |
| `roleType` | Den angivna typen av roll. Möjliga värden för rolltypen är: `user-defined` och `system-defined`. |
| `permissionSets` | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| `sandboxes` | Den här egenskapen visar de sandlådor i organisationen som har etablerats för en viss roll. |
| `subjectAttributes` | De attribut som anger korrelationen mellan ett ämne och de plattformsresurser som de har tillgång till. |
| `subjectAttributes.labels` | Visar dataanvändningsetiketter som används för den efterfrågade rollen. |

## Söka efter en roll {#lookup}

Du kan söka efter en enskild roll genom att göra en GET-förfrågan som innehåller motsvarande `roleId` i sökvägen till begäran.

**API-format**

```http
GET /roles/{ROLE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| {ROLE_ID} | ID:t för rollen som du vill söka efter. |

**Begäran**

Följande begäran hämtar information om `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett godkänt svar returnerar information om det efterfrågade roll-ID:t, inklusive information om dess rolltyp, behörighetsgrupper och ämnesattribut.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar rollen. Detta ID genereras automatiskt. |
| `name` | Namnet på din roll. |
| `description` | Egenskapen description innehåller ytterligare information om din roll. |
| `roleType` | Den angivna typen av roll. Möjliga värden för rolltypen är: `user-defined` och `system-defined`. |
| `permissionSets` | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| `sandboxes` | Den här egenskapen visar de sandlådor i organisationen som har etablerats för en viss roll. |
| `subjectAttributes` | De attribut som anger korrelationen mellan ett ämne och de plattformsresurser som de har tillgång till. |
| `subjectAttributes.labels` | Visar dataanvändningsetiketter som används för den efterfrågade rollen. |

## Söka efter ämnen efter roll-ID

Du kan även hämta ämnen genom att göra en GET-förfrågan till `/roles` slutpunkt när en {ROLE_ID}.

**API-format**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parameter | Beskrivning |
| --- | --- |
| {ROLE_ID} | ID för rollen som är associerad med de ämnen du vill söka efter. |

**Begäran**

Följande begäran hämtar ämnen som är associerade med `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett lyckat svar returnerar de ämnen som är associerade med det efterfrågade roll-ID:t, inklusive motsvarande ämne-ID och subjekttyp.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `roleId` | Det roll-ID som är associerat med det frågade ämnet. |
| `subjectType` | Den typ av ämne som frågan gäller. |
| `subjectId` | Det ID som motsvarar det frågade ämnet. |

## Skapa en roll {#create}

Om du vill skapa en ny roll skickar du en POST till `/roles` slutpunkt med värden för rollens namn, beskrivning och rolltyp.

**API-format**

```http
POST /roles/
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på din roll. Se till att namnet på din roll är beskrivande, eftersom du kan använda det för att söka efter information om din roll. |
| `description` | (Valfritt) Ett beskrivande värde som du kan ta med för att ge mer information om din roll. |
| `roleType` | Den angivna typen av roll. Möjliga värden för rolltypen är: `user-defined` och `system-defined`. |

**Svar**

Ett svar returnerar din nya roll, med dess motsvarande roll-ID, samt information om rolltyp, behörighetsgrupper och ämnesattribut.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar rollen. Detta ID genereras automatiskt. |
| `name` | Namnet på din roll. |
| `description` | Egenskapen description innehåller ytterligare information om din roll. |
| `roleType` | Den angivna typen av roll. Möjliga värden för rolltypen är: `user-defined` och `system-defined`. |
| `permissionSets` | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| `sandboxes` | Den här egenskapen visar de sandlådor i organisationen som har etablerats för en viss roll. |
| `subjectAttributes` | De attribut som anger korrelationen mellan ett ämne och de plattformsresurser som de har tillgång till. |
| `subjectAttributes.labels` | Visar dataanvändningsetiketter som används för den efterfrågade rollen. |

## Uppdatera en roll {#patch}

Du kan uppdatera egenskaperna för en roll genom att göra en PATCH-förfrågan till `/roles` slutpunkten när du anger motsvarande roll-ID och värden för de åtgärder du vill använda.

**API-format**

```http
PATCH /roles/{ROLE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| {ROLE_ID} | ID:t för rollen som du vill uppdatera. |

**Begäran**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| Användning | Beskrivning |
| --- | --- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera rollen. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Sökvägen till den parameter som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar den uppdaterade rollen, inklusive nya värden för de egenskaper som du valde att uppdatera.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar rollen. Detta ID genereras automatiskt. |
| `name` | Namnet på din roll. |
| `description` | Egenskapen description innehåller ytterligare information om din roll. |
| `roleType` | Den angivna typen av roll. Möjliga värden för rolltypen är: `user-defined` och `system-defined`. |
| `permissionSets` | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| `sandboxes` | Den här egenskapen visar de sandlådor i organisationen som har etablerats för en viss roll. |
| `subjectAttributes` | De attribut som anger korrelationen mellan ett ämne och de plattformsresurser som de har tillgång till. |
| `subjectAttributes.labels` | Visar dataanvändningsetiketter som används för den efterfrågade rollen. |

## Uppdatera en roll efter roll-ID {#put}

Du kan uppdatera en roll genom att göra en PUT-förfrågan till `/roles` slutpunkt och ange det roll-ID som motsvarar den roll som du vill uppdatera.

**API-format**

```http
PUT /roles/{ROLE_ID}
```

**Begäran**

Följande begäran uppdaterar namn, beskrivning och rolltyp för roll-ID: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Det uppdaterade namnet på en roll. |
| `description` | Den uppdaterade beskrivningen av en roll. |
| `roleType` | Den angivna typen av roll. Möjliga värden för rolltypen är: `user-defined` och `system-defined`. |

**Svar**

Ett godkänt svar returnerar din uppdaterade roll, inklusive nya värden för namn, beskrivning och rolltyp.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar rollen. Detta ID genereras automatiskt. |
| `name` | Namnet på din roll. |
| `description` | Egenskapen description innehåller ytterligare information om din roll. |
| `roleType` | Den angivna typen av roll. Möjliga värden för rolltypen är: `user-defined` och `system-defined`. |
| `permissionSets` | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| `sandboxes` | Den här egenskapen visar de sandlådor i organisationen som har etablerats för en viss roll. |
| `subjectAttributes` | De attribut som anger korrelationen mellan ett ämne och de plattformsresurser som de har tillgång till. |
| `subjectAttributes.labels` | Visar dataanvändningsetiketter som används för den efterfrågade rollen. |

## Uppdatera ämne efter roll-ID

Om du vill uppdatera de ämnen som är associerade med en roll skickar du en PATCH-förfrågan till `/roles` slutpunkten när du anger roll-ID för de ämnen du vill uppdatera.

**API-format**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Parameter | Beskrivning |
| --- | --- |
| {ROLE_ID} | ID för rollen som är associerad med de ämnen som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar de ämnen som är associerade med `{ROLE_ID}`.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| Användning | Beskrivning |
| --- | --- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera rollen. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Sökvägen till den parameter som ska uppdateras. |
| `value` | Det nya värdet som du vill uppdatera parametern med. |

**Svar**

Ett lyckat svar returnerar din uppdaterade roll, inklusive nya värden för personerna.

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## Ta bort en roll {#delete}

Om du vill ta bort en roll gör du en DELETE-förfrågan till `/roles` slutpunkten när du anger ID:t för rollen som du vill ta bort.

**API-format**

```http
DELETE /roles/{ROLE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| {ROLE_ID} | ID för rollen som du vill ta bort. |

**Begäran**

Följande begäran tar bort rollen med ID för `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) till rollen. Du får HTTP-statusen 404 (Hittades inte) eftersom rollen har tagits bort från administrationen.

## Lägg till API-autentiseringsuppgifter {#apicredential}

Om du vill lägga till en API-autentiseringsuppgift ska du göra en PATCH-begäran på `/roles` slutpunkt när du anger deltagarnas roll-ID.

**API-format**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| Användning | Beskrivning |
| --- | --- |
| `op` | Åtgärdsanropet som används för att definiera åtgärden som krävs för att uppdatera rollen. Åtgärderna omfattar: `add`, `replace`och `remove`. |
| `path` | Sökvägen till den parameter som ska läggas till. |
| `value` | Värdet som du vill lägga till parametern med. |

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.
