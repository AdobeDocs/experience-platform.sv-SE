---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera datauppsättning
title: Aktivera en datauppsättning för profiluppdateringar med API:er
type: Tutorial
description: I den här självstudiekursen visas hur du använder Adobe Experience Platform API:er för att aktivera en datauppsättning med"upsert"-funktioner för att uppdatera kundprofildata i realtid.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 6985ebf8705130636abdc50b5c3f50299a60f2aa
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Aktivera en datauppsättning för profiluppdateringar med API:er

Den här självstudiekursen handlar om hur du aktiverar en datauppsättning med&quot;upsert&quot;-funktioner för att uppdatera kundprofildata i realtid. Detta inkluderar steg för att skapa en ny datauppsättning och konfigurera en befintlig datauppsättning.

>[!NOTE]
>
>Arbetsflödet som beskrivs i den här självstudiekursen fungerar bara för batchinmatning. För direktuppspelande ingessionsöverföringar, se guiden på [skicka uppdateringar av delar av rader till kundprofilen i realtid med Data Prep](../../data-prep/upserts.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av flera Adobe Experience Platform-tjänster som arbetar med att hantera profilaktiverade datauppsättningar. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för dessa relaterade [!DNL Platform] tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Catalog Service]](../../catalog/home.md): Ett RESTful API som gör att du kan skapa datauppsättningar och konfigurera dem för [!DNL Real-Time Customer Profile] och [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.
- [Batchförtäring](../../ingestion/batch-ingestion/overview.md): Med API:t för gruppinmatning kan du importera data till Experience Platform som gruppfiler.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API:erna för plattformen.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare `Content-Type` header. Rätt värde för den här rubriken visas vid behov i exempelbegäranden.

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en `x-sandbox-name` huvud som anger namnet på den sandlåda som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

## Skapa en datauppsättning som är aktiverad för profiluppdateringar

När du skapar en ny datauppsättning kan du aktivera datauppsättningen för profilen och aktivera uppdateringsfunktioner när du skapar den.

>[!NOTE]
>
>Om du vill skapa en ny profilaktiverad datauppsättning måste du känna till ID:t för ett befintligt XDM-schema som är aktiverat för profilen. Information om hur du söker efter eller skapar ett profilaktiverat schema finns i självstudiekursen om [skapa ett schema med API:t för schemaregister](../../xdm/tutorials/create-schema-api.md).

Om du vill skapa en datauppsättning som är aktiverad för profil och uppdateringar använder du en POST-förfrågan till `/dataSets` slutpunkt.

**API-format**

```http
POST /dataSets
```

**Begäran**

Genom att inkludera båda `unifiedIdentity` och `unifiedProfile` under `tags` i begärandetexten kommer datauppsättningen att aktiveras för [!DNL Profile] när de skapas. I `unifiedProfile` array, lägga till `isUpsert:true` kommer att lägga till möjligheten för datauppsättningen att stödja uppdateringar.

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
| `schemaRef.id` | ID för [!DNL Profile]-aktiverat schema som datauppsättningen baseras på. |
| `{TENANT_ID}` | Namnutrymmet i [!DNL Schema Registry] som innehåller resurser som tillhör din organisation. Se [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) i [!DNL Schema Registry] för mer information. |

**Svar**

Ett lyckat svar visar en array som innehåller ID:t för den nya datauppsättningen i form av `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurera en befintlig datauppsättning {#configure-an-existing-dataset}

Följande steg beskriver hur du konfigurerar en befintlig profilaktiverad datauppsättning för uppdateringsfunktioner (upsert).

>[!NOTE]
>
>Om du vill konfigurera en befintlig profilaktiverad datauppsättning för uppdatering måste du först inaktivera datauppsättningen för profilen och sedan återaktivera den bredvid `isUpsert` -tagg. Om den befintliga datauppsättningen inte är aktiverad för profilen kan du fortsätta direkt till stegen för [aktivera datauppsättningen för profil och upsert](#enable-the-dataset). Om du är osäker visar följande steg hur du kontrollerar om datauppsättningen redan är aktiverad.

### Kontrollera om datauppsättningen är aktiverad för profilen

Använda [!DNL Catalog] API, du kan undersöka en befintlig datamängd för att avgöra om den är aktiverad för användning i [!DNL Real-Time Customer Profile]. Följande anrop hämtar information om en datauppsättning per ID.

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
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Under `tags` -egenskapen ser du att `unifiedProfile` finns med värdet `enabled:true`. Därför [!DNL Real-Time Customer Profile] är aktiverat för den här datauppsättningen.

### Inaktivera datauppsättningen för profilen

Om du vill konfigurera en profilaktiverad datauppsättning för uppdateringar måste du först inaktivera `unifiedProfile` och `unifiedIdentity` -taggar och sedan återaktivera dem bredvid `isUpsert` -tagg. Detta görs med två PATCH-begäranden, en gång för att inaktivera och en för att återaktivera.

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

Den första texten i PATCH-begäran innehåller en `path` till `unifiedProfile` och `path` till `unifiedIdentity`, ange `value` till `enabled:false` för båda dessa sökvägar för att inaktivera taggarna.

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

En lyckad PATCH-begäran returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickades i PATCH-begäran. The `unifiedProfile` och `unifiedIdentity` -taggar har nu inaktiverats.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Aktivera datauppsättningen för profil och upsert {#enable-the-dataset}

En befintlig datauppsättning kan aktiveras för profiluppdateringar och attributuppdateringar med en enda begäran från PATCH.

>[!IMPORTANT]
>
>När du aktiverar din datauppsättning för profil bör du kontrollera att schemat som datauppsättningen är associerad med är **även** Profilaktiverad. Om schemat inte är profilaktiverat kommer datauppsättningen att **not** visas som profilaktiverat i plattformsgränssnittet.

**API-format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill uppdatera. |

**Begäran**

Begärandetexten innehåller en `path` till `unifiedProfile` ställa in `value` som innehåller `enabled` och `isUpsert` taggar, båda inställda på `true`och en `path` till `unifiedIdentity` ställa in `value` som innehåller `enabled` tagg angiven till `true`.

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

En lyckad PATCH-begäran returnerar HTTP-status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickades i PATCH-begäran. The `unifiedProfile` tagg och `unifiedIdentity` -taggen har nu aktiverats och konfigurerats för attributuppdateringar.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Nästa steg

Din profilaktiverade och upsert-aktiverade datauppsättning kan nu användas av arbetsflöden för batchimport för att uppdatera profildata. Om du vill veta mer om inmatning av data i Adobe Experience Platform börjar du med att läsa [dataöverföring - översikt](../../ingestion/home.md).
