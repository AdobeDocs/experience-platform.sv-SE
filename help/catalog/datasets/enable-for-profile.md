---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;aktivera datauppsättning
title: Aktivera en datauppsättning för profil- och identitetstjänsten med API:er
type: Tutorial
description: I den här självstudiekursen visas hur du aktiverar en datauppsättning för användning med kundprofil och identitetstjänst i realtid med Adobe Experience Platform API:er.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Aktivera en datauppsättning för [!DNL Profile] och [!DNL Identity Service] med API:er

I den här självstudiekursen beskrivs hur du aktiverar en datauppsättning för användning i [!DNL Real-Time Customer Profile] och [!DNL Identity Service], som delas upp i följande steg:

1. Aktivera en datauppsättning för användning i [!DNL Real-Time Customer Profile], med ett av två alternativ:
   - [Skapa en ny datauppsättning](#create-a-dataset-enabled-for-profile-and-identity)
   - [Konfigurera en befintlig datauppsättning](#configure-an-existing-dataset)
1. [Infoga data i datauppsättningen](#ingest-data-into-the-dataset)
1. [Bekräfta datainmatning med kundprofil för realtid](#confirm-data-ingest-by-real-time-customer-profile)
1. [Bekräfta datainmatning via identitetstjänsten](#confirm-data-ingest-by-identity-service)

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av flera Adobe Experience Platform-tjänster som arbetar med att hantera profilaktiverade datauppsättningar. Innan du börjar med den här självstudiekursen bör du läsa igenom dokumentationen för de här relaterade [!DNL Experience Platform]-tjänsterna:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiverar [!DNL Real-Time Customer Profile] genom att brygga identiteter från olika datakällor som importeras till [!DNL Experience Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Ett RESTful-API som gör att du kan skapa datauppsättningar och konfigurera dem för [!DNL Real-Time Customer Profile] och [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

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

## Skapa en datauppsättning aktiverad för profil och identitet {#create-a-dataset-enabled-for-profile-and-identity}

Du kan aktivera en datauppsättning för kundprofil och identitetstjänst i realtid direkt när den skapas eller när som helst efter att datauppsättningen har skapats. Om du vill aktivera en datamängd som redan har skapats följer du stegen för [att konfigurera en befintlig datamängd](#configure-an-existing-dataset) som hittas senare i det här dokumentet.

>[!NOTE]
>
>Om du vill skapa en ny profilaktiverad datauppsättning måste du känna till ID:t för ett befintligt XDM-schema som är aktiverat för profilen. Information om hur du söker efter eller skapar ett profilaktiverat schema finns i självstudiekursen [Skapa ett schema med API:t för schemaregister](../../xdm/tutorials/create-schema-api.md).

Om du vill skapa en datauppsättning som är aktiverad för profilen kan du använda en POST-begäran för slutpunkten `/dataSets`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Egenskap | Beskrivning |
|---|---|
| `schemaRef.id` | ID:t för det [!DNL Profile]-aktiverade schemat som datauppsättningen ska baseras på. |
| `{TENANT_ID}` | Namnområdet i [!DNL Schema Registry] som innehåller resurser som tillhör din organisation. Mer information finns i avsnittet [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) i [!DNL Schema Registry]-utvecklarhandboken. |

**Svar**

Ett lyckat svar visar en matris som innehåller ID:t för den nya datamängden i formatet `"@/dataSets/{DATASET_ID}"`. När du har skapat och aktiverat en datauppsättning fortsätter du till stegen för [överföring av data](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Konfigurera en befintlig datauppsättning {#configure-an-existing-dataset}

Följande steg beskriver hur du aktiverar en tidigare skapad datauppsättning för [!DNL Real-Time Customer Profile] och [!DNL Identity Service]. Om du redan har skapat en profilaktiverad datauppsättning fortsätter du till stegen för [inhämtning av data](#ingest-data-into-the-dataset).

### Kontrollera om datauppsättningen är aktiverad {#check-if-the-dataset-is-enabled}

Med API:t [!DNL Catalog] kan du undersöka en befintlig datauppsättning för att avgöra om den är aktiverad för användning i [!DNL Real-Time Customer Profile] och [!DNL Identity Service]. Följande anrop hämtar information om en datauppsättning per ID.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Under egenskapen `tags` ser du att både `unifiedProfile` och `unifiedIdentity` finns med värdet `enabled:true`. Därför är [!DNL Real-Time Customer Profile] och [!DNL Identity Service] aktiverade för den här datauppsättningen.

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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

Begärandetexten innehåller `path` till två typer av taggar, `unifiedProfile` och `unifiedIdentity`. `value` av var och en är matriser som innehåller strängen `enabled:true`.

**Svar**

En lyckad PATCH-begäran returnerar HTTP Status 200 (OK) och en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickas i PATCH-begäran. Taggarna `unifiedProfile` och `unifiedIdentity` har nu lagts till och datauppsättningen har aktiverats för användning av profiltjänster och identitetstjänster.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Infoga data i datauppsättningen {#ingest-data-into-the-dataset}

Både [!DNL Real-Time Customer Profile] och [!DNL Identity Service] använder XDM-data när de importeras till en datauppsättning. Instruktioner om hur du överför data till en datauppsättning finns i självstudiekursen [Skapa en datauppsättning med API:er](../../catalog/datasets/create.md). När du planerar vilka data som ska skickas till den [!DNL Profile]-aktiverade datauppsättningen bör du tänka på följande metodtips:

- Inkludera alla data som du vill använda som segmenteringskriterier.
- Ta med så många identifierare du kan identifiera från dina profildata för att maximera identitetsdiagrammet. Detta gör att [!DNL Identity Service] kan sy identiteter över datauppsättningar mer effektivt.

## Bekräfta dataimport av [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

När du överför data till en ny datauppsättning för första gången, eller som en del av en process som inbegriper en ny ETL eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts som förväntat. Med åtkomst-API:t [!DNL Real-Time Customer Profile] kan du hämta batchdata när de läses in till en datamängd. Om du inte kan hämta någon av de entiteter som du förväntar dig, kanske din datauppsättning inte är aktiverad för [!DNL Real-Time Customer Profile]. När du har bekräftat att datauppsättningen har aktiverats kontrollerar du att källdataformatet och identifierarna stöder dina förväntningar. Detaljerade instruktioner om hur du använder [!DNL Real-Time Customer Profile]-API:t för att komma åt [!DNL Profile]-data finns i [entitetens slutpunktshandbok](../../profile/api/entities.md), som också kallas [!DNL Profile Access]-API:t.

## Bekräfta datainhämtning via identitetstjänsten {#confirm-data-ingest-by-identity-service}

Varje inkapslat datafragment som innehåller mer än en identitet skapar en länk i ditt privata identitetsdiagram. Om du vill ha mer information om identitetsdiagram och få tillgång till identitetsdata börjar du med att läsa översikten för [identitetstjänsten](../../identity-service/home.md).
