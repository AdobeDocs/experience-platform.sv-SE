---
keywords: Experience Platform;hem;populära ämnen;api;Attributbaserad åtkomstkontroll;attributbaserad åtkomstkontroll
solution: Experience Platform
title: API-slutpunkt för åtkomstkontrollprinciper
description: Med slutpunkten /policies i API:t för attributbaserad åtkomstkontroll kan du programmässigt hantera principer i Adobe Experience Platform.
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---

# Slutpunkt för åtkomstkontrollprinciper

Åtkomstkontrollprinciper är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Dessa profiler kan antingen vara lokala eller globala och kan åsidosätta andra principer. The `/policies` -slutpunkten i det attributbaserade API:t för åtkomstkontroll gör det möjligt att programmässigt hantera principer, inklusive information om reglerna som styr dem samt deras respektive ämnesvillkor.

>[!IMPORTANT]
>
>Den här slutpunkten ska inte blandas ihop med `/policies` slutpunkt i [API för datastyrning](../../../data-governance/api/policies.md), som används för att hantera dataanvändningsprinciper.

## Komma igång

API-slutpunkten som används i den här guiden är en del av det attributbaserade API:t för åtkomstkontroll. Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med profiler {#list}

Gör en GET-förfrågan till `/policies` slutpunkt för att lista alla befintliga policyer i organisationen.

**API-format**

```http
GET /policies
```

**Begäran**

Följande begäran hämtar en lista över befintliga principer.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett godkänt svar returnerar en lista över befintliga principer.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar en princip. Den här identifieraren genereras automatiskt och kan användas för att söka efter, uppdatera och ta bort en princip. |
| `imsOrgId` | Organisationen där den efterfrågade policyn är tillgänglig. |
| `createdBy` | ID för den användare som skapade profilen. |
| `createdAt` | Tiden då profilen skapades. The `createdAt` egenskapen visas i en Unix Epooch-tidsstämpel. |
| `modifiedBy` | ID för den användare som senast uppdaterade profilen. |
| `modifiedAt` | Tidpunkten när profilen senast uppdaterades. The `modifiedAt` egenskapen visas i en Unix Epooch-tidsstämpel. |
| `name` | Namnet på principen. |
| `description` | (Valfritt) En egenskap som kan läggas till för att ge mer information om en viss princip. |
| `status` | Aktuell status för en princip. Den här egenskapen definierar om en princip används `active` eller `inactive`. |
| `subjectCondition` | Vilka villkor som gäller för ett motiv. Ett ämne är en användare med vissa attribut som begär åtkomst till en resurs för att utföra en åtgärd. I detta fall `subjectCondition` är frågeliknande villkor som tillämpas på ämnesattributen. |
| `rules` | Den uppsättning regler som definierar en princip. Regler definierar vilka attributkombinationer som är auktoriserade för att ämnet ska kunna utföra en åtgärd på resursen. |
| `rules.effect` | Effekten som blir resultatet efter att värden bedömts för `action`, `condition` och `resource`. Möjliga värden är: `permit`, `deny`, eller `indeterminate`. |
| `rules.resource` | Resursen eller objektet som ett ämne kan eller inte kan komma åt.  Resurser kan vara filer, program, servrar eller till och med API:er. |
| `rules.condition` | De villkor som används för en resurs. Om en resurs till exempel är ett schema kan ett schema ha vissa etiketter som bidrar till om en åtgärd mot det schemat är tillåten eller otillåten. |
| `rules.action` | Den åtgärd som ett ämne tillåts att göra mot en frågad resurs. Möjliga värden är: `read`, `create`, `edit`och `delete`. |

## Slå upp principinformation efter ID {#lookup}

Gör en GET-förfrågan till `/policies` slutpunkten när ett princip-ID angavs i sökvägen för begäran för att hämta information om den enskilda principen.

**API-format**

```http
GET /policies/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| {POLICY_ID} | ID:t för profilen som du vill hämta. |

**Begäran**

Följande begäran hämtar information om en enskild princip.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

En slutförd begäran returnerar information om det efterfrågade princip-ID:t.

```json
{
    "id": "13138ef6-c007-495d-837f-0a248867e219",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652859368555,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652890780206,
    "name": "Documentation-Copy",
    "description": "xyz",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        },
        {
            "effect": "Deny",
            "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar en princip. Den här identifieraren genereras automatiskt och kan användas för att söka efter, uppdatera och ta bort en princip. |
| `imsOrgId` | Organisationen där den efterfrågade policyn är tillgänglig. |
| `createdBy` | ID för den användare som skapade profilen. |
| `createdAt` | Tiden då profilen skapades. The `createdAt` egenskapen visas i en Unix Epooch-tidsstämpel. |
| `modifiedBy` | ID för den användare som senast uppdaterade profilen. |
| `modifiedAt` | Tidpunkten när profilen senast uppdaterades. The `modifiedAt` egenskapen visas i en Unix Epooch-tidsstämpel. |
| `name` | Namnet på principen. |
| `description` | (Valfritt) En egenskap som kan läggas till för att ge mer information om en viss princip. |
| `status` | Aktuell status för en princip. Den här egenskapen definierar om en princip används `active` eller `inactive`. |
| `subjectCondition` | Vilka villkor som gäller för ett motiv. Ett ämne är en användare med vissa attribut som begär åtkomst till en resurs för att utföra en åtgärd. I detta fall `subjectCondition` är frågeliknande villkor som tillämpas på ämnesattributen. |
| `rules` | Den uppsättning regler som definierar en princip. Regler definierar vilka attributkombinationer som är auktoriserade för att ämnet ska kunna utföra en åtgärd på resursen. |
| `rules.effect` | Effekten som blir resultatet efter att värden bedömts för `action`, `condition` och `resource`. Möjliga värden är: `permit`, `deny`, eller `indeterminate`. |
| `rules.resource` | Resursen eller objektet som ett ämne kan eller inte kan komma åt.  Resurser kan vara filer, program, servrar eller till och med API:er. |
| `rules.condition` | De villkor som används för en resurs. Om en resurs till exempel är ett schema kan ett schema ha vissa etiketter som bidrar till om en åtgärd mot det schemat är tillåten eller otillåten. |
| `rules.action` | Den åtgärd som ett ämne tillåts att göra mot en frågad resurs. Möjliga värden är: `read`, `create`, `edit`och `delete`. |


## Skapa en profil {#create}

Om du vill skapa en ny princip skickar du en POST till `/policies` slutpunkt.

**API-format**

```http
POST /policies
```

**Begäran**

Följande begäran skapar en ny princip med namnet: `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "read"
          ]
        }
      ]
    }'
```

| Parameter | Beskrivning |
| --- | --- |
| `name` | Namnet på principen. |
| `description` | (Valfritt) En egenskap som kan läggas till för att ge mer information om en viss princip. |
| `imsOrgId` | Organisationen som innehåller policyn. |
| `rules` | Den uppsättning regler som definierar en princip. Regler definierar vilka attributkombinationer som är auktoriserade för att ämnet ska kunna utföra en åtgärd på resursen. |
| `rules.effect` | Effekten som blir resultatet efter att värden bedömts för `action`, `condition` och `resource`. Möjliga värden är: `permit`, `deny`, eller `indeterminate`. |
| `rules.resource` | Resursen eller objektet som ett ämne kan eller inte kan komma åt.  Resurser kan vara filer, program, servrar eller till och med API:er. |
| `rules.condition` | De villkor som används för en resurs. Om en resurs till exempel är ett schema kan ett schema ha vissa etiketter som bidrar till om en åtgärd mot det schemat är tillåten eller otillåten. |
| `rules.action` | Den åtgärd som ett ämne tillåts att göra mot en frågad resurs. Möjliga värden är: `read`, `create`, `edit`och `delete`. |

**Svar**

En lyckad begäran returnerar den nyligen skapade principen, inklusive dess unika princip-ID och associerade regler.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar en princip. Den här identifieraren genereras automatiskt och kan användas för att söka efter, uppdatera och ta bort en princip. |
| `name` | Namnet på en princip. |
| `rules` | Den uppsättning regler som definierar en princip. Regler definierar vilka attributkombinationer som är auktoriserade för att ämnet ska kunna utföra en åtgärd på resursen. |
| `rules.effect` | Effekten som blir resultatet efter att värden bedömts för `action`, `condition` och `resource`. Möjliga värden är: `permit`, `deny`, eller `indeterminate`. |
| `rules.resource` | Resursen eller objektet som ett ämne kan eller inte kan komma åt.  Resurser kan vara filer, program, servrar eller till och med API:er. |
| `rules.condition` | De villkor som används för en resurs. Om en resurs till exempel är ett schema kan ett schema ha vissa etiketter som bidrar till om en åtgärd mot det schemat är tillåten eller otillåten. |
| `rules.action` | Den åtgärd som ett ämne tillåts att göra mot en frågad resurs. Möjliga värden är: `read`, `create`, `edit`och `delete`. |


## Uppdatera en princip per princip-ID {#put}

Om du vill uppdatera reglerna för en enskild princip skickar du en PUT-begäran till `/policies` slutpunkten när ID för principen som du vill uppdatera anges i sökvägen till begäran.

**API-format**

```http
PUT /policies/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| {POLICY_ID} | ID:t för profilen som du vill uppdatera. |

**Begäran**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "read"
        ]
      }
    ]
  }'
```

**Svar**

Ett lyckat svar returnerar den uppdaterade principen.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Uppdatera principegenskaper {#patch}

Om du vill uppdatera egenskaperna för en enskild princip skickar du en PATCH-begäran till `/policies` slutpunkten när ID för principen som du vill uppdatera anges i sökvägen till begäran.

**API-format**

```http
PATCH /policies/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| {POLICY_ID} | ID:t för profilen som du vill uppdatera. |

**Begäran**

Följande begäran ersätter värdet för `/description` i princip-ID `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
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

Ett lyckat svar returnerar det efterfrågade princip-ID:t med uppdaterad beskrivning.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Ta bort en profil {#delete}

Om du vill ta bort en princip skickar du en DELETE-begäran till `/policies` slutpunkten när ID för profilen som du vill ta bort anges.

**API-format**

```http
DELETE /policies/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| {POLICY_ID} | ID för profilen som du vill ta bort. |

**Begäran**

Följande begäran tar bort principen med ID:t för `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) på profilen. Du får HTTP-statusen 404 (Hittades inte) eftersom profilen har tagits bort från administrationen.
