---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera datauppsättning
title: Konfigurera en datauppsättning för profil- och identitetstjänsten med API:er
topic: tutorial
type: Tutorial
description: I den här självstudiekursen visas hur du aktiverar en datauppsättning för användning med kundprofil och identitetstjänst i realtid med Adobe Experience Platform API:er.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 0%

---


# Konfigurera en datauppsättning för [!DNL Profile] och [!DNL Identity Service] med API:er

I den här självstudiekursen beskrivs hur du aktiverar en datauppsättning för användning i [!DNL Real-time Customer Profile] och [!DNL Identity Service], enligt följande:

1. Aktivera en datauppsättning för användning i [!DNL Real-time Customer Profile], med ett av två alternativ:
   - [Skapa en ny datauppsättning](#create-a-dataset-enabled-for-profile-and-identity)
   - [Konfigurera en befintlig datauppsättning](#configure-an-existing-dataset)
1. [Infoga data i datauppsättningen](#ingest-data-into-the-dataset)
1. [Bekräfta datainmatning med kundprofil i realtid](#confirm-data-ingest-by-real-time-customer-profile)
1. [Bekräfta datainhämtning via identitetstjänsten](#confirm-data-ingest-by-identity-service)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används för att hantera [!DNL Profile]-aktiverade datauppsättningar. Innan du börjar med den här självstudiekursen bör du läsa igenom dokumentationen för de här relaterade [!DNL Platform]-tjänsterna:

- [[!DNL Real-time Customer Profile]](../home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Identity Service]](../../identity-service/home.md): Möjliggör  [!DNL Real-time Customer Profile] genom att överbrygga identiteter från olika datakällor som importeras till  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Ett RESTful-API som gör att du kan skapa datauppsättningar och konfigurera dem för  [!DNL Real-time Customer Profile] och  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:erna för plattformen.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Skapa en datauppsättning som är aktiverad för [!DNL Profile] och [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Du kan aktivera en datauppsättning för [!DNL Real-time Customer Profile] och [!DNL Identity Service] direkt när den skapas eller när som helst efter att datauppsättningen har skapats. Om du vill aktivera en datamängd som redan har skapats följer du stegen för [konfigurera en befintlig datamängd](#configure-an-existing-dataset) som hittas senare i det här dokumentet. Om du vill skapa en ny datauppsättning måste du känna till ID:t för ett befintligt XDM-schema som är aktiverat för kundprofil i realtid. Information om hur du söker efter eller skapar ett profilaktiverat schema finns i självstudiekursen om att [skapa ett schema med API:t för schemaregister](../../xdm/tutorials/create-schema-api.md). Följande anrop till API:t [!DNL Catalog] aktiverar en datamängd för [!DNL Profile] och [!DNL Identity Service].

**API-format**

```http
POST /dataSets
```

**Begäran**

Genom att ta med `unifiedProfile` och `unifiedIdentity` under `tags` i begärandetexten aktiveras datauppsättningen omedelbart för [!DNL Profile] respektive [!DNL Identity Service]. Värdena för dessa taggar måste vara en array som innehåller strängen `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Egenskap | Beskrivning |
|---|---|
| `schemaRef.id` | ID:t för det [!DNL Profile]-aktiverade schema som datauppsättningen ska baseras på. |
| `{TENANT_ID}` | Namnutrymmet i [!DNL Schema Registry] som innehåller resurser som tillhör din IMS-organisation. Mer information finns i avsnittet [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) i [!DNL Schema Registry]-utvecklarhandboken. |

**Svar**

Ett lyckat svar visar en matris som innehåller ID:t för den nya datamängden i formatet `"@/dataSets/{DATASET_ID}"`. När du har skapat och aktiverat en datauppsättning fortsätter du till stegen för [överföring av data](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurera en befintlig datauppsättning {#configure-an-existing-dataset}

Följande steg beskriver hur du aktiverar en tidigare skapad datauppsättning för [!DNL Real-time Customer Profile] och [!DNL Identity Service]. Om du redan har skapat en profilaktiverad datauppsättning går du vidare till stegen för [datainhämtning](#ingest-data-into-the-dataset).

### Kontrollera om datauppsättningen är aktiverad {#check-if-the-dataset-is-enabled}

Med API:t [!DNL Catalog] kan du undersöka en befintlig datamängd för att avgöra om den är aktiverad för användning i [!DNL Real-time Customer Profile] och [!DNL Identity Service]. Följande anrop hämtar information om en datauppsättning per ID.

**API-format**

```http
GET /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DATASET_ID}` | ID:t för en datauppsättning som du vill inspektera. |

**Begäran**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Under egenskapen `tags` ser du att både `unifiedProfile` och `unifiedIdentity` finns med värdet `enabled:true`. Därför är [!DNL Real-time Customer Profile] och [!DNL Identity Service] aktiverade för den här datauppsättningen.

### Aktivera datauppsättningen {#enable-the-dataset}

Om den befintliga datauppsättningen inte har aktiverats för [!DNL Profile] eller [!DNL Identity Service] kan du aktivera den genom att göra en PATCH-begäran med datauppsättnings-ID:t.

**API-format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera. |

**Begäran**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

Begärandetexten innehåller en `tags`-egenskap som innehåller två underegenskaper: `"unifiedProfile"` och `"unifiedIdentity"`. Värdena för dessa underegenskaper är arrayer som innehåller strängen `"enabled:true"`.

**Svar:**
En lyckad PATCH-begäran returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickades i PATCH-begäran. Taggarna `"unifiedProfile"` och `"unifiedIdentity"` har nu lagts till och datauppsättningen är aktiverad för användning av profil- och identitetstjänster.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Infoga data i datauppsättningen {#ingest-data-into-the-dataset}

Både [!DNL Real-time Customer Profile] och [!DNL Identity Service] använder XDM-data när de hämtas till en datauppsättning. Instruktioner om hur du överför data till en datauppsättning finns i självstudiekursen om att [skapa en datauppsättning med API:er](../../catalog/datasets/create.md). När du planerar vilka data som ska skickas till den [!DNL Profile]-aktiverade datauppsättningen bör du tänka på följande metodtips:

- Inkludera alla data som du vill använda som målgruppsvillkor.
- Ta med så många identifierare du kan identifiera från dina profildata för att maximera identitetsdiagrammet. Detta gör att [!DNL Identity Service] kan sy identiteter över datauppsättningar mer effektivt.

## Bekräfta dataimport med [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts som förväntat. Med åtkomst-API:t [!DNL Real-time Customer Profile] kan du hämta batchdata när de läses in till en datauppsättning. Om du inte kan hämta någon av de enheter du förväntar dig, kanske din datauppsättning inte är aktiverad för [!DNL Real-time Customer Profile]. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar. Detaljerade instruktioner om hur du använder [!DNL Real-time Customer Profile]-API:t för att komma åt [!DNL Profile]-data finns i [entitetens slutpunktshandbok](../api/entities.md), som också kallas [!DNL Profile Access]-API:t.

## Bekräfta datainhämtning via identitetstjänsten {#confirm-data-ingest-by-identity-service}

Varje inkapslat datafragment som innehåller mer än en identitet skapar en länk i ditt privata identitetsdiagram. Mer information om identitetsdiagram och åtkomst till identitetsdata finns i [översikten över identitetstjänsten](../../identity-service/home.md).