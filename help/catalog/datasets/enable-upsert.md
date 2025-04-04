---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera datauppsättning
title: Aktivera en datauppsättning för profiluppdateringar med API:er
type: Tutorial
description: I den här självstudiekursen visas hur du använder Adobe Experience Platform API:er för att aktivera en datauppsättning med"upsert"-funktioner för att uppdatera kundprofildata i realtid.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Aktivera en datauppsättning för profiluppdateringar med API:er

Den här självstudiekursen handlar om hur du aktiverar en datauppsättning med&quot;upsert&quot;-funktioner för att uppdatera kundprofildata i realtid. Detta inkluderar steg för att skapa en ny datauppsättning och konfigurera en befintlig datauppsättning.

>[!NOTE]
>
>Arbetsflödet som beskrivs i den här självstudiekursen fungerar bara för batchinmatning. För direktuppspelande ingessionsöverföringar, se guiden om att [skicka uppdateringar (del av rad) till kundprofilen i realtid med Data Prep](../../data-prep/upserts.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av flera Adobe Experience Platform-tjänster som arbetar med att hantera profilaktiverade datauppsättningar. Innan du börjar med den här självstudiekursen bör du läsa igenom dokumentationen för de här relaterade [!DNL Experience Platform]-tjänsterna:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Catalog Service]](../../catalog/home.md): Ett RESTful-API som gör att du kan skapa datauppsättningar och konfigurera dem för [!DNL Real-Time Customer Profile] och [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.
- [Gruppinmatning](../../ingestion/batch-ingestion/overview.md): Med API:t för gruppinmatning kan du importera data till Experience Platform som gruppfiler.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa Experience Platform API:er.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik för `Content-Type`. Rätt värde för den här rubriken visas vid behov i exempelbegäranden.

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver ett `x-sandbox-name`-huvud som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

## Skapa en datauppsättning som är aktiverad för profiluppdateringar

När du skapar en ny datauppsättning kan du aktivera datauppsättningen för profilen och aktivera uppdateringsfunktioner när du skapar den.

>[!NOTE]
>
>Om du vill skapa en ny profilaktiverad datauppsättning måste du känna till ID:t för ett befintligt XDM-schema som är aktiverat för profilen. Information om hur du söker efter eller skapar ett profilaktiverat schema finns i självstudiekursen [Skapa ett schema med API:t för schemaregister](../../xdm/tutorials/create-schema-api.md).

Om du vill skapa en datauppsättning som är aktiverad för profil och uppdateringar använder du en POST-begäran till slutpunkten `/dataSets`.

**API-format**

```http
POST /dataSets
```

**Begäran**

Genom att inkludera både `unifiedIdentity` och `unifiedProfile` under `tags` i begärandetexten aktiveras datauppsättningen för [!DNL Profile] när den skapas. Om du lägger till `isUpsert:true` i `unifiedProfile`-arrayen kan datauppsättningen ha stöd för uppdateringar.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schemaRef.id` | ID:t för det [!DNL Profile]-aktiverade schemat som datauppsättningen ska baseras på. |
| `{TENANT_ID}` | Namnområdet i [!DNL Schema Registry] som innehåller resurser som tillhör din organisation. Mer information finns i avsnittet [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) i [!DNL Schema Registry]-utvecklarhandboken. |

**Svar**

Ett lyckat svar visar en matris som innehåller ID:t för den nya datamängden i formatet `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurera en befintlig datauppsättning {#configure-an-existing-dataset}

Följande steg beskriver hur du konfigurerar en befintlig profilaktiverad datauppsättning för uppdateringsfunktioner (upsert).

>[!NOTE]
>
>Om du vill konfigurera en befintlig profilaktiverad datauppsättning för uppdatering måste du först inaktivera datauppsättningen för profilen och sedan återaktivera den tillsammans med taggen `isUpsert`. Om den befintliga datauppsättningen inte är aktiverad för profilen kan du fortsätta direkt till stegen för [att aktivera datauppsättningen för profil och upsert](#enable-the-dataset). Om du är osäker visar följande steg hur du kontrollerar om datauppsättningen redan är aktiverad.

### Kontrollera om datauppsättningen är aktiverad för profilen

Med API:t [!DNL Catalog] kan du undersöka en befintlig datauppsättning för att avgöra om den är aktiverad för användning i [!DNL Real-Time Customer Profile]. Följande anrop hämtar information om en datauppsättning per ID.

**API-format**

```http
GET /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | ID:t för en datauppsättning som du vill inspektera. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Under egenskapen `tags` ser du att `unifiedProfile` finns med värdet `enabled:true`. Därför är [!DNL Real-Time Customer Profile] aktiverat för den här datauppsättningen.

### Inaktivera datauppsättningen för profilen

Om du vill konfigurera en profilaktiverad datauppsättning för uppdateringar måste du först inaktivera taggarna `unifiedProfile` och `unifiedIdentity` och sedan återaktivera dem tillsammans med taggen `isUpsert`. Detta görs med två PATCH-förfrågningar, en gång för att inaktivera och en för att återaktivera.

>[!WARNING]
>
>Data som hämtas till datauppsättningen när den är inaktiverad kommer inte att hämtas till profilarkivet. Du bör undvika att samla in data i datauppsättningen tills den har återaktiverats för profilen.

**API-format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera. |

**Begäran**

Den första PATCH-begärandetexten innehåller en `path` till `unifiedProfile` och en `path` till `unifiedIdentity`, vilket ställer in `value` på `enabled:false` för båda sökvägarna för att inaktivera taggarna.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**Svar**

En lyckad PATCH-begäran returnerar HTTP Status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickas i PATCH-begäran. Taggarna `unifiedProfile` och `unifiedIdentity` har nu inaktiverats.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Aktivera datauppsättningen för profil och upsert {#enable-the-dataset}

En befintlig datauppsättning kan aktiveras för profiluppdateringar och attributuppdateringar med en enda PATCH-begäran.

>[!IMPORTANT]
>
>När du aktiverar din datauppsättning för profil kontrollerar du att schemat som datauppsättningen är kopplad till är **även** profilinaktiverat. Om schemat inte är profilaktiverat visas datauppsättningen **inte** som profilaktiverad i Experience Platform-gränssnittet.

**API-format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera. |

**Begäran**

Begärandetexten innehåller en `path` till `unifiedProfile` som anger att `value` ska inkludera taggarna `enabled` och `isUpsert`, båda inställda på `true`, och en `path` till `unifiedIdentity` som anger att `value` ska innehålla taggen `enabled` inställd på `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**Svar**

En lyckad PATCH-begäran returnerar HTTP Status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickas i PATCH-begäran. Taggen `unifiedProfile` och taggen `unifiedIdentity` har nu aktiverats och konfigurerats för attributuppdateringar.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Nästa steg

Din profilaktiverade och upsert-aktiverade datauppsättning kan nu användas av arbetsflöden för batchimport för att uppdatera profildata. Om du vill veta mer om hur du importerar data till Adobe Experience Platform börjar du med att läsa översikten över [dataimporten](../../ingestion/home.md).
