---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: säkerställa att målgruppssegmentens dataanvändning följs
topic: tutorial
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Använd API:er för att säkerställa att data används korrekt för ett målgruppssegment

Den här självstudiekursen beskriver stegen för att implementera efterlevnad av dataanvändning för målgruppssegment för kundprofiler i realtid med API:er.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Kundprofil](../../profile/home.md)i realtid: Kundprofilen i realtid är ett generiskt uppslagsenhetsarkiv och används för att hantera XDM-data (Experience Data Model) inom plattformen. Profilen sammanfogar data över olika företagsdata och ger åtkomst till dessa data i en enhetlig presentation.
   - [Sammanslagningsprinciper](../../profile/api/merge-policies.md): Regler som används av kundprofilen i realtid för att avgöra vilka data som kan sammanfogas i en enhetlig vy under vissa villkor. Sammanslagningsprinciper kan konfigureras för datastyrning.
- [Segmentering](../home.md): Hur kundprofilen i realtid delar upp en stor grupp individer som finns i profilbutiken i mindre grupper som har liknande egenskaper och som reagerar på liknande sätt som marknadsföringsstrategier.
- [Datastyrning](../../data-governance/home.md): Datastyrning tillhandahåller infrastruktur för märkning och verkställighet av dataanvändning (DULE) med hjälp av följande komponenter:
   - [Dataanvändningsetiketter](../../data-governance/labels/user-guide.md): Etiketter som används för att beskriva datauppsättningar och fält utifrån känslighetsnivån som deras respektive data ska hanteras med.
   - [Dataanvändningsprinciper](../../data-governance/api/getting-started.md): Konfigurationer som anger vilka marknadsföringsåtgärder som tillåts för data som kategoriseras av särskilda dataanvändningsetiketter.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:erna för plattformen.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Söka efter en sammanfogningsprincip för en segmentdefinition

Det här arbetsflödet börjar med att man får åtkomst till ett känt målgruppssegment. Segment som har aktiverats för användning i kundprofilen i realtid innehåller ett ID för sammanfogningsprincip i segmentdefinitionen. Den här sammanfogningsprincipen innehåller information om vilka datauppsättningar som ska inkluderas i segmentet, som i sin tur innehåller tillämpliga dataanvändningsetiketter.

Med hjälp av [Segmenterings-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)kan du söka efter en segmentdefinition med hjälp av dess ID för att hitta den associerade sammanfogningsprincipen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrgId": "{IMS_ORG}",
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

## Hitta källdatauppsättningarna från sammanfogningsprincipen

Sammanslagningsprinciper innehåller information om deras källdatauppsättningar, som i sin tur innehåller DULE-etiketter. Du kan söka efter information om en sammanfogningsprincip genom att ange sammanfogningsprincip-ID i en GET-begäran till profilens API.

**API-format**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | ID:t för sammanfogningsprincipen som hämtades i [föregående steg](#lookup-a-merge-policy-for-a-segment-definition). |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om sammanfogningsprincipen.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
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
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schema.name` | Namnet på schemat som är associerat med sammanfogningsprincipen. |
| `attributeMerge.type` | Konfigurationstypen för sammanslagningsprincipen med prioritet för data. Om värdet är `dataSetPrecedence`listas de datauppsättningar som är associerade med den här sammanfogningsprincipen under `attributeMerge > data > order`. Om värdet är `timestampOrdered`används alla datauppsättningar som är associerade med schemat som refereras i av sammanfogningsprincipen `schema.name` . |
| `attributeMerge.data.order` | Om attributet `attributeMerge.type` är `dataSetPrecedence`det är en array som innehåller ID:n för de datauppsättningar som används av den här sammanfogningsprincipen. Dessa ID:n används i nästa steg. |

## Söka efter dataanvändningsetiketter för källdatauppsättningar

När du har samlat in ID:n för sammanfogningsprincipens källdatauppsättningar kan du använda dessa ID:n för att söka efter de dataanvändningsetiketter som konfigurerats för själva datauppsättningarna och eventuella specifika datafält som finns i dem.

Följande anrop till [katalogtjänstens API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) hämtar dataanvändningsetiketter som är associerade med en enskild datauppsättning genom att ange dess ID i sökvägen för begäran:

**API-format**

```http
GET /dataSets/{DATASET_ID}/dule
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{DATASET_ID}` | ID:t för den datauppsättning vars dataanvändningsetiketter du vill söka efter. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista över dataanvändningsetiketter som är associerade med datauppsättningen som helhet och eventuella särskilda datafält som är associerade med källschemat.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `dataset` | Ett objekt som innehåller dataanvändningsetiketterna som används för datauppsättningen som helhet. |
| `schemaFields` | En array med objekt som representerar specifika schemafält där dataanvändningsetiketter används. |
| `schemaFields.path` | Sökvägen till schemafältet vars dataanvändningsetiketter visas i samma objekt. |

## Filtrera datafält

>[!NOTE] Det här steget är valfritt. Om du inte vill justera de data som ingår i ditt segment baserat på dina resultat i det föregående steget av att [söka efter dataanvändningsetiketter](#lookup-data-usage-labels-for-the-source-datasets), kan du gå vidare till det sista steget i att [utvärdera data för policyöverträdelser](#evaluate-data-for-policy-violations).

Om du vill justera data som ingår i målgruppssegmentet kan du göra det på något av följande två sätt:

### Uppdatera segmentdefinitionens sammanfogningsprincip

Om du uppdaterar sammanfogningsprincipen för en segmentdefinition justeras de datauppsättningar och fält som inkluderas när segmentjobbet körs. Mer information finns i avsnittet [Uppdatera en befintlig sammanfogningsprincip](../../profile/api/merge-policies.md) i självstudiekursen för sammanfogningsprinciper.

### Begränsa specifika datafält när segmentet exporteras

När du exporterar ett segment till en datauppsättning med hjälp av kundprofils-API:t i realtid kan du filtrera de data som ingår i exporten med hjälp av `fields` parametern. Alla datafält som läggs till i den här parametern inkluderas i exporten, medan alla andra datafält exkluderas.

Tänk dig ett segment som har datafält med namnen&quot;A&quot;,&quot;B&quot; och&quot;C&quot;. Om du bara vill exportera fält C, innehåller parametern bara fält C. `fields` Om du gör det exkluderas fälten A och B när du exporterar segmentet.

Mer information finns i avsnittet [Exportera ett segment](./evaluate-a-segment.md#export-a-segment) i självstudiekursen för segmentering.

## Utvärdera data för policyöverträdelser

Nu när du har samlat in etiketter för dataanvändning som hör till målgruppssegmentet kan du testa dessa etiketter mot marknadsföringsåtgärder för att utvärdera eventuella överträdelser av dataanvändningspolicyn. Detaljerade steg om hur du utför principutvärderingar med API:t för [DULE Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)finns i dokumentet om [principutvärdering](../../data-governance/enforcement/overview.md).

## Nästa steg

Genom att följa den här självstudiekursen har du tittat på etiketterna för dataanvändning som är kopplade till ett målgruppssegment och testat dem för policyöverträdelser mot specifika marknadsföringsåtgärder. Mer information om datastyrning i Experience Platform finns i [datastyrningsöversikten](../../data-governance/home.md).