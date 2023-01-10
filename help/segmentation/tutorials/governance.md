---
keywords: Experience Platform;hemmabruk;populära ämnen;efterlevnad av dataanvändning;framtvinga efterlevnad av dataanvändning;Segmenteringstjänst;segmentering;Segmentering;
solution: Experience Platform
title: Tvinga regelefterlevnad för dataanvändning för ett målgruppssegment med API:er
type: Tutorial
description: Den här självstudiekursen beskriver stegen för att implementera efterlevnad av dataanvändning för målgruppssegment för kundprofiler i realtid med API:er.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 0%

---

# Använd API:er för att säkerställa att data används korrekt för ett målgruppssegment

Den här självstudiekursen handlar om hur du kontrollerar att dataanvändningen följs för [!DNL Real-Time Customer Profile] målgruppssegment med API:er.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i [!DNL Adobe Experience Platform]:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] är ett generiskt sökentitetsarkiv och används för att hantera [!DNL Experience Data Model (XDM)] data inom [!DNL Platform]. Profilen sammanfogar data över olika företagsdata och ger åtkomst till dessa data i en enhetlig presentation.
   - [Sammanfoga profiler](../../profile/api/merge-policies.md): Regler som används av [!DNL Real-Time Customer Profile] för att fastställa vilka data som kan sammanfogas i en enhetlig vy under vissa förhållanden. Sammanslagningsprinciper kan konfigureras för datastyrning.
- [[!DNL Segmentation]](../home.md): Hur [!DNL Real-Time Customer Profile] delar upp en stor grupp individer som finns i profilbutiken i mindre grupper som delar liknande egenskaper och kommer att svara på liknande sätt som marknadsföringsstrategier.
- [Datastyrning](../../data-governance/home.md): Datastyrning tillhandahåller infrastruktur för märkning och verkställighet av dataanvändning med hjälp av följande komponenter:
   - [Dataanvändningsetiketter](../../data-governance/labels/user-guide.md): Etiketter som används för att beskriva datauppsättningar och fält utifrån känslighetsnivån som deras respektive data ska hanteras med.
   - [Dataanvändningspolicyer](../../data-governance/policies/overview.md): Konfigurationer som anger vilka marknadsföringsåtgärder som tillåts för data som kategoriseras av särskilda dataanvändningsetiketter.
   - [Politiska åtgärder](../../data-governance/enforcement/overview.md): Gör att du kan tillämpa dataanvändningsprinciper och förhindra dataåtgärder som utgör policyöverträdelser.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ringa samtal till [!DNL Platform] API:er.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Söka efter en sammanfogningsprincip för en segmentdefinition {#merge-policy}

Det här arbetsflödet börjar med att man får åtkomst till ett känt målgruppssegment. Segment som är aktiverade för användning i [!DNL Real-Time Customer Profile] innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter.

Använda [!DNL Segmentation] API kan du söka efter en segmentdefinition med hjälp av dess ID för att hitta den associerade sammanfogningsprincipen.

**API-format**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID:t för segmentdefinitionen som du vill söka efter. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar informationen om segmentdefinitionen.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `mergePolicyId` | ID för den sammanfogningsprincip som används för segmentdefinitionen. Detta kommer att användas i nästa steg. |

## Hitta källdatauppsättningarna från sammanfogningsprincipen {#datasets}

Sammanslagningsprinciper innehåller information om deras källdatauppsättningar, som i sin tur innehåller dataanvändningsetiketter. Du kan söka efter information om en sammanfogningsprincip genom att ange sammanfogningsprincip-ID i en GET-begäran till [!DNL Profile] API. Mer information om kopplingsprofiler finns i [slutpunktshandbok för sammanslagningsprinciper](../../profile/api/merge-policies.md).

**API-format**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID:t för sammanfogningsprincipen som hämtats i [föregående steg](#merge-policy). |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om sammanfogningsprincipen.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schema.name` | Namnet på schemat som är associerat med sammanfogningsprincipen. |
| `attributeMerge.type` | Konfigurationstypen för sammanslagningsprincipen med prioritet för data. Om värdet är `dataSetPrecedence`, listas de datauppsättningar som är kopplade till den här sammanfogningsprincipen under `attributeMerge > data > order`. Om värdet är `timestampOrdered`och sedan alla datauppsättningar som är kopplade till schemat som refereras i `schema.name` används av sammanfogningsprincipen. |
| `attributeMerge.data.order` | Om `attributeMerge.type` är `dataSetPrecedence`blir det här attributet en array som innehåller ID:n för de datauppsättningar som används av den här sammanfogningsprincipen. Dessa ID:n används i nästa steg. |

## Utvärdera datauppsättningar för policyöverträdelser

>[!NOTE]
>
> I det här steget antas att du har minst en aktiv dataanvändningsprincip som förhindrar att specifika marknadsföringsåtgärder utförs på data som innehåller vissa etiketter. Om du inte har några tillämpliga användarprofiler för de datauppsättningar som utvärderas, följ [självstudiekurs om hur du skapar principer](../../data-governance/policies/create.md) om du vill skapa en innan du fortsätter med det här steget.

När du har fått ID:n för sammanfogningsprincipens källdatauppsättningar kan du använda [API för principtjänst](https://www.adobe.io/experience-platform-apis/references/policy-service/) utvärdera dessa datauppsättningar mot specifika marknadsföringsåtgärder för att kontrollera om det finns överträdelser mot dataanvändningspolicyn.

Om du vill utvärdera datauppsättningarna måste du ange namnet på marknadsföringsåtgärden i sökvägen till en begäran om POST, samtidigt som du anger datauppsättnings-ID:n i begärandetexten, vilket visas i exemplet nedan.

**API-format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den marknadsföringsåtgärd som är associerad med dataanvändningsprincipen som du utvärderar datauppsättningarna efter. Beroende på om policyn har definierats av Adobe eller din organisation måste du använda `/marketingActions/core` eller `/marketingActions/custom`, respektive. |

**Begäran**

Följande förfrågan testar `exportToThirdParty` marknadsföringsåtgärd mot datauppsättningar som erhållits i [föregående steg](#datasets). Nyttolasten för begäran är en array som innehåller ID:n för varje datamängd.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `entityType` | Varje objekt i nyttolastarrayen måste ange vilken typ av enhet som definieras. I det här fallet kommer värdet alltid att vara &quot;dataSet&quot;. |
| `entityID` | Varje objekt i nyttolastarrayen måste ange ett unikt ID för en datamängd. |

**Svar**

Ett lyckat svar returnerar URI:n för marknadsföringsåtgärden, dataanvändningsetiketterna som samlades in från de angivna datauppsättningarna och en lista över dataanvändningsprinciper som överträtts som ett resultat av testning av åtgärden mot dessa etiketter. I det här exemplet visas principen &quot;Exportera data till tredje part&quot; i `violatedPolicies` , vilket anger att marknadsföringsåtgärden utlöste en policyöverträdelse.

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{ORG_ID}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `duleLabels` | En lista över dataanvändningsetiketter som har extraherats från de angivna datauppsättningarna. |
| `discoveredLabels` | En lista över de datauppsättningar som tillhandahölls i nyttolasten för begäran, med information om de datauppsättningsnivårubriker och fältetiketter som hittades i varje. |
| `violatedPolicies` | En matris med en lista över dataanvändningsprinciper som har överträtts genom att marknadsföringsåtgärden testas (anges i `marketingActionRef`) mot den tillhandahållna `duleLabels`. |

Med hjälp av data som returneras i API-svaret kan du skapa protokoll i ditt upplevelseprogram för att se till att regelöverträdelser verkställs korrekt när de inträffar.

## Filtrera datafält

Om ditt målgruppssegment inte klarar utvärderingen kan du justera data som ingår i segmentet på något av de två sätt som beskrivs nedan.

### Uppdatera segmentdefinitionens sammanfogningsprincip

Om du uppdaterar sammanfogningsprincipen för en segmentdefinition justeras de datauppsättningar och fält som inkluderas när segmentjobbet körs. Se avsnittet om [uppdatera en befintlig kopplingsprofil](../../profile/api/merge-policies.md#update) i självstudiekursen om API-sammanslagningsprinciper om du vill ha mer information.

### Begränsa specifika datafält när segmentet exporteras

När du exporterar ett segment till en datauppsättning med [!DNL Segmentation] API, du kan filtrera data som ingår i exporten med hjälp av `fields` parameter. Alla datafält som läggs till i den här parametern inkluderas i exporten, medan alla andra datafält exkluderas.

Tänk dig ett segment som har datafält med namnen&quot;A&quot;,&quot;B&quot; och&quot;C&quot;. Om du bara vill exportera fält C, `fields` parametern skulle innehålla enbart fältet&quot;C&quot;. Om du gör det exkluderas fälten A och B när du exporterar segmentet.

Se avsnittet om [exportera ett segment](./evaluate-a-segment.md#export) i segmenteringsjälvstudiekursen för mer information.

## Nästa steg

Genom att följa den här självstudiekursen har du tittat på etiketterna för dataanvändning som är kopplade till ett målgruppssegment och testat dem för policyöverträdelser mot specifika marknadsföringsåtgärder. Mer information om datastyrning i [!DNL Experience Platform], läs översikten för [Datastyrning](../../data-governance/home.md).
