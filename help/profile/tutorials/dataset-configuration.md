---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Konfigurera en datauppsättning för profil- och identitetstjänsten med API:er
topic: tutorial
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# Konfigurera en datauppsättning för profil- och identitetstjänsten med API:er

I den här självstudiekursen beskrivs hur du aktiverar en datauppsättning för användning i kundprofil och identitetstjänst i realtid, enligt följande:

1. Aktivera en datauppsättning för användning i kundprofilen i realtid med något av följande två alternativ:
   - [Skapa en ny datauppsättning](#create-a-dataset-enabled-for-profile-and-identity)
   - [Konfigurera en befintlig datauppsättning](#configure-an-existing-dataset)
1. [Infoga data i datauppsättningen](#ingest-data-into-the-dataset)
1. [Bekräfta datainmatning med kundprofil i realtid](#confirm-data-ingest-by-real-time-customer-profile)
1. [Bekräfta datainhämtning via identitetstjänsten](#confirm-data-ingest-by-identity-service)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika Adobe Experience Platform-tjänsterna som används för att hantera profilaktiverade datauppsättningar. Innan du börjar med den här självstudiekursen ska du läsa dokumentationen för de här relaterade plattformstjänsterna:

- [Kundprofil](../home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Identitetstjänst](../../identity-service/home.md): Möjliggör kundprofil i realtid genom att överbrygga identiteter från olika datakällor som hämtas in till Platform.
- [Katalogtjänst](../../catalog/home.md): Ett RESTful API som gör att du kan skapa datauppsättningar och konfigurera dem för kundprofil och identitetstjänst i realtid.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:erna för plattformen.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: application/json

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Skapa en datauppsättning som är aktiverad för profil och identitet {#create-a-dataset-enabled-for-profile-and-identity}

Du kan aktivera en datauppsättning för kundprofil och identitetstjänst i realtid direkt när den skapas eller när som helst efter att datauppsättningen har skapats. Om du vill aktivera en datauppsättning som redan har skapats följer du stegen för [att konfigurera en befintlig datauppsättning](#configure-an-existing-dataset) som hittas senare i det här dokumentet. Om du vill skapa en ny datauppsättning måste du känna till ID:t för ett befintligt XDM-schema som är aktiverat för kundprofil i realtid. Information om hur du söker efter eller skapar ett profilaktiverat schema finns i självstudiekursen om hur du [skapar ett schema med API:t](../../xdm/tutorials/create-schema-api.md)för schemaregister. Följande anrop till katalog-API:t aktiverar en datauppsättning för profil- och identitetstjänsten.

**API-format**

```http
POST /dataSets
```

**Begäran**

Genom att inkludera `unifiedProfile` och `unifiedIdentity` under `tags` i begärandetexten aktiveras datauppsättningen omedelbart för profiltjänsten respektive identitetstjänsten. Värdena för dessa taggar måste vara en array som innehåller strängen `"enabled:true"`.

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
| `schemaRef.id` | ID:t för det profilaktiverade schema som datauppsättningen ska baseras på. |
| `{TENANT_ID}` | Namnområdet i schemaregistret som innehåller resurser som tillhör din IMS-organisation. Mer information finns i avsnittet [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) i Utvecklarhandbok för schemaregister. |

**Svar**

Ett lyckat svar visar en array som innehåller ID:t för den nya datauppsättningen i form av `"@/dataSets/{DATASET_ID}"`. När du har skapat och aktiverat en datauppsättning fortsätter du till stegen för [överföring av data](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurera en befintlig datauppsättning {#configure-an-existing-dataset}

Följande steg beskriver hur du aktiverar en tidigare skapad datauppsättning för kundprofil och identitetstjänst i realtid. Om du redan har skapat en profilaktiverad datauppsättning fortsätter du till stegen för [datainhämtning](#ingest-data-into-the-dataset).

### Kontrollera om datauppsättningen är aktiverad {#check-if-the-dataset-is-enabled}

Med hjälp av Catalog API kan du undersöka en befintlig datauppsättning för att avgöra om den är aktiverad för användning i kundprofil och identitetstjänst i realtid. Följande anrop hämtar information om en datauppsättning per ID.

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

Under `tags` egenskapen ser du att `unifiedProfile` och `unifiedIdentity` båda finns med värdet `enabled:true`. Därför är kundprofil och identitetstjänst i realtid aktiverad för den här datauppsättningen.

### Aktivera datauppsättningen {#enable-the-dataset}

Om den befintliga datauppsättningen inte har aktiverats för profil- eller identitetstjänsten kan du aktivera den genom att göra en PATCH-begäran med datauppsättnings-ID:t.

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

Begärandetexten innehåller en `tags` egenskap som innehåller två underegenskaper: `"unifiedProfile"` och `"unifiedIdentity"`. Värdena för dessa underegenskaper är arrayer som innehåller strängen `"enabled:true"`.

**Svar** En lyckad PATCH-begäran returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickas i PATCH-begäran. Taggarna `"unifiedProfile"` och `"unifiedIdentity"` har nu lagts till och datauppsättningen är aktiverad för användning av tjänsterna Profil och Identitet.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Infoga data i datauppsättningen {#ingest-data-into-the-dataset}

Både kundprofil och identitetstjänst i realtid använder XDM-data när de hämtas in till en datauppsättning. Instruktioner om hur du överför data till en datauppsättning finns i självstudiekursen om hur du [skapar en datauppsättning med API:er](../../catalog/datasets/create.md). När du planerar vilka data som ska skickas till din profilaktiverade datauppsättning bör du tänka på följande metodtips:

- Inkludera alla data som du vill använda som målgruppsvillkor.
- Ta med så många identifierare du kan identifiera från dina profildata för att maximera identitetsdiagrammet. Detta gör att identitetstjänsten kan sy identiteter över datauppsättningar mer effektivt.

## Bekräfta datainmatning med kundprofil i realtid {#confirm-data-ingest-by-real-time-customer-profile}

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts som förväntat. Med hjälp av API:t för kundprofilåtkomst i realtid kan du hämta batchdata när de läses in till en datauppsättning. Om du inte kan hämta någon av de enheter du förväntar dig, kanske din datauppsättning inte är aktiverad för kundprofil i realtid. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar. Detaljerade instruktioner om hur du använder kundprofils-API:t i realtid för att få åtkomst till profildata finns i [underhandboken om entiteter, som även kallas &quot;API:t för profilåtkomst&quot;](../api/entities.md).

## Bekräfta datainhämtning via identitetstjänsten {#confirm-data-ingest-by-identity-service}

Varje inkapslat datafragment som innehåller mer än en identitet skapar en länk i ditt privata identitetsdiagram. Om du vill ha mer information om identitetsdiagram och få tillgång till identitetsdata börjar du med att läsa översikten över [identitetstjänsten](../../identity-service/home.md).