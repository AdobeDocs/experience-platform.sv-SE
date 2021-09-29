---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera datauppsättning
title: Aktivera en datauppsättning för profiluppdateringar med API:er
type: Tutorial
description: I den här självstudiekursen visas hur du använder Adobe Experience Platform API:er för att aktivera en datauppsättning med"upsert"-funktioner för att uppdatera kundprofildata i realtid.
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Aktivera en datauppsättning för profiluppdateringar med API:er

Den här självstudiekursen handlar om hur du aktiverar en datauppsättning med&quot;upsert&quot;-funktioner för att uppdatera kundprofildata i realtid. Detta inkluderar steg för att skapa en ny datauppsättning och konfigurera en befintlig datauppsättning.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av flera Adobe Experience Platform-tjänster som arbetar med att hantera profilaktiverade datauppsättningar. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för dessa relaterade tjänster för DNL Platform:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Catalog Service]](../../catalog/home.md): Ett RESTful-API som gör att du kan skapa datauppsättningar och konfigurera dem för  [!DNL Real-time Customer Profile] och  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.
- [Batchförtäring](../../ingestion/batch-ingestion/overview.md)

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:erna för plattformen.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett `Content-Type`-huvud. Rätt värde för den här rubriken visas vid behov i exempelbegäranden.

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver ett `x-sandbox-name`-huvud som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

## Skapa en datauppsättning som är aktiverad för profiluppdateringar

När du skapar en ny datauppsättning kan du aktivera datauppsättningen för profilen och aktivera uppdateringsfunktioner när du skapar den.

>[!NOTE]
>
>Om du vill skapa en ny profilaktiverad datauppsättning måste du känna till ID:t för ett befintligt XDM-schema som är aktiverat för profilen. Information om hur du söker efter eller skapar ett profilaktiverat schema finns i självstudiekursen om att [skapa ett schema med API:t för schemaregister](../../xdm/tutorials/create-schema-api.md).

Om du vill skapa en datauppsättning som är aktiverad för profil och uppdateringar använder du en POST-förfrågan till `/dataSets`-slutpunkten.

**API-format**

```http
POST /dataSets
```

**Begäran**

Genom att ta med `unifiedProfile` under `tags` i begärandetexten aktiveras datauppsättningen för [!DNL Profile] när den skapas. Om du lägger till `isUpsert:true` i `unifiedProfile`-arrayen kan datauppsättningen stödja uppdateringar.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "fields":[],
        "schemaRef" : {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
          "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags" : {
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `schemaRef.id` | ID:t för det [!DNL Profile]-aktiverade schema som datauppsättningen ska baseras på. |
| `{TENANT_ID}` | Namnutrymmet i [!DNL Schema Registry] som innehåller resurser som tillhör din IMS-organisation. Mer information finns i avsnittet [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) i [!DNL Schema Registry]-utvecklarhandboken. |

**Svar**

Ett lyckat svar visar en matris som innehåller ID:t för den nya datamängden i formatet `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurera en befintlig datauppsättning {#configure-an-existing-dataset}

Följande steg beskriver hur du konfigurerar en befintlig profilaktiverad datauppsättning för uppdateringsfunktioner (&quot;upsert&quot;).

>[!NOTE]
>
>Om du vill konfigurera en befintlig profilaktiverad datauppsättning för &quot;upsert&quot; måste du först inaktivera datauppsättningen för profilen och sedan återaktivera den tillsammans med `isUpsert`-taggen. Om den befintliga datauppsättningen inte är aktiverad för Profil kan du fortsätta direkt till stegen för [att aktivera datauppsättningen för Profil och infoga](#enable-the-dataset). Om du är osäker visar följande steg hur du kontrollerar om datauppsättningen redan är aktiverad.

### Kontrollera om datauppsättningen är aktiverad för profilen

Med API:t [!DNL Catalog] kan du undersöka en befintlig datamängd för att avgöra om den är aktiverad för användning i [!DNL Real-time Customer Profile]. Följande anrop hämtar information om en datauppsättning per ID.

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
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
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
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
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

Under egenskapen `tags` ser du att `unifiedProfile` finns med värdet `enabled:true`. Därför är [!DNL Real-time Customer Profile] aktiverat för den här datauppsättningen.

### Inaktivera datauppsättningen för profilen

Om du vill konfigurera en profilaktiverad datauppsättning för uppdateringar måste du först inaktivera taggen `unifiedProfile` och sedan återaktivera den tillsammans med taggen `isUpsert`. Detta görs med två PATCH-begäranden, en gång för att inaktivera och en för att återaktivera.

>[!WARNING]
>
>Data som hämtas till datauppsättningen när den är inaktiverad kommer inte att hämtas till profilarkivet. Vi rekommenderar att du undviker att samla in data i datauppsättningen tills den har återaktiverats för profilen.

**API-format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera. |

**Begäran**

Den första PATCH-begärandetexten innehåller en `path` till `unifiedProfile`-inställning för `value` till `enabled:false` för att inaktivera taggen.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

**Svar:**
En lyckad PATCH-begäran returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickades i PATCH-begäran. Taggen `unifiedProfile` har nu inaktiverats.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Aktivera datauppsättningen för profil och upsert {#enable-the-dataset}

En befintlig datauppsättning kan aktiveras för profiluppdateringar och attributuppdateringar med en enda begäran från PATCH.

**API-format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
|---|---|
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera. |

**Begäran**

Begärandetexten innehåller en `path` till `unifiedProfile`-inställning för `value` att inkludera taggarna `enabled` och `isUpsert`, som båda är inställda på `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

**Svar:**
En lyckad PATCH-begäran returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickades i PATCH-begäran. Taggen `unifiedProfile` har nu aktiverats och konfigurerats för attributuppdateringar.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Nästa steg

Din profil och datauppsättning som har stöd för upsert kan nu användas av arbetsflöden för import av grupper och strömning för att göra uppdateringar av profildata. Om du vill veta mer om hur du importerar data till Adobe Experience Platform kan du börja med att läsa översikten över dataöverföring[a1/>.](../../ingestion/home.md)
