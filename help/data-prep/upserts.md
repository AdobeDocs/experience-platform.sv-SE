---
keywords: Experience Platform;hem;populära ämnen;dataförberedelse;Dataprep;strömning;upsert;strömning upsert
title: Skicka uppdateringar av delar av rader till kundprofil i realtid med hjälp av Data Prep
description: Lär dig hur du skickar uppdateringar av delar av rader till kundprofilen i realtid med Data Prep.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: db6a0b45d600d16b24f7f749e414dfd0998fbf5e
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---

# Skicka uppdateringar av delar av rader till [!DNL Real-Time Customer Profile] använda [!DNL Data Prep]

>[!WARNING]
>
>Inmatning i XDM-meddelanden (Experience Data Model) för entitetsuppdatering (med JSON PATCH-åtgärder) för profiluppdateringar via DCS-inloppet har tagits bort. Som ett alternativ kan du [importera rådata till DCS-ingången](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) och ange nödvändiga datamappningar för att omvandla data till XDM-kompatibla meddelanden för profiluppdateringar.

Direktuppspelande överföringar i [!DNL Data Prep] kan du skicka uppdateringar av delar av rader till [!DNL Real-Time Customer Profile] data samtidigt som nya identitetslänkar skapas och etableras med en enda API-begäran.

Genom att direktuppspela uppladdningar kan du behålla dataformatet samtidigt som du översätter dessa data till [!DNL Real-Time Customer Profile] PATCH begär vid förtäring. Baserat på de indata du anger [!DNL Data Prep] gör att du kan skicka en enda API-nyttolast och översätta data till båda [!DNL Real-Time Customer Profile] PATCH och [!DNL Identity Service] SKAPA förfrågningar.

>[!NOTE]
>
>För att utnyttja uppgraderingsfunktionen rekommenderar vi att du inaktiverar XDM-kompatibla konfigurationer under datainmatning och mappar om inkommande nyttolast med [Data Prep Mapper](./ui/mapping.md).

Det här dokumentet innehåller information om hur du direktuppspelar överföringar i [!DNL Data Prep].

## Komma igång

Den här översikten kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] gör att datatekniker kan mappa, omvandla och validera data till och från Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
* [Kundprofil i realtid](../profile/home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [Källor](../sources/home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.

## Använd direktuppspelande upserts i [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Följande källor har stöd för direktuppspelande upserts:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Direktuppspelning ger ett arbetsflöde på hög nivå

Direktuppspelande överföringar i [!DNL Data Prep] fungerar på följande sätt:

* Du måste först skapa och aktivera en datauppsättning för [!DNL Profile] förbrukning. Se guiden på [aktivera en datauppsättning för [!DNL Profile]](../catalog/datasets/enable-for-profile.md) för mer information.
* Om nya identiteter måste länkas måste du också skapa ytterligare en datauppsättning **med samma schema** som [!DNL Profile] datauppsättning.
* När datauppsättningarna har förberetts måste du skapa ett dataflöde för att mappa din inkommande begäran till [!DNL Profile] datauppsättning,
* Därefter måste du uppdatera den inkommande begäran så att de nödvändiga rubrikerna inkluderas. Dessa rubriker definierar:
   * Den dataåtgärd som krävs för att utföras med [!DNL Profile]: `create`, `merge`och `delete`.
   * Den valfria identitetsåtgärden som ska utföras med [!DNL Identity Service]: `create`.

### Konfigurera identitetsdatauppsättningen

Om nya identiteter måste länkas måste du skapa och skicka ytterligare en datauppsättning i den inkommande nyttolasten. När du skapar en identitetsdatauppsättning måste du se till att följande krav uppfylls:

* Identitetsdatauppsättningen måste ha sitt associerade schema som [!DNL Profile] datauppsättning. Om scheman inte matchar kan det leda till inkonsekvent systembeteende.
* Du måste dock se till att identitetsdatauppsättningen skiljer sig från [!DNL Profile] datauppsättning. Om datauppsättningarna är desamma skrivs data över i stället för att uppdateras.
* När den första datauppsättningen måste aktiveras för [!DNL Profile], identitetsdatauppsättningen **ska inte aktiveras** for [!DNL Profile]. Annars skrivs data också över i stället för att uppdateras. Identitetsdatauppsättningen **ska vara aktiverat** for [!DNL Identity Service].

#### Obligatoriska fält i scheman som är associerade med identitetsdatauppsättningen {#identity-dataset-required-fileds}

Om schemat innehåller obligatoriska fält måste valideringen av datauppsättningen inaktiveras för att aktivera [!DNL Identity Service] om du bara vill ta emot identiteterna. Du kan inaktivera valideringen genom att använda `disabled` värdet till `acp_validationContext` parameter. Se exemplet nedan:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>Du behöver inte göra någon ytterligare konfiguration om det schema som är associerat med identitetsdatauppsättningen inte har några obligatoriska fält.

## Inkommande nyttolaststruktur

I följande exempel visas ett exempel på en inkommande nyttolaststruktur som skapar nya identitetslänkar.

### Nyttolast med identitetskonfiguration

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| Parameter | Beskrivning |
| --- | --- |
| `flowId` | Ett unikt ID som identifierar ett dataflöde. Detta dataflödes-ID ska motsvara den källanslutning som skapats med [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], eller [!DNL HTTP API]. Det här dataflödet ska även ha en [!DNL Profile]-aktiverad datauppsättning som måldatauppsättning. **Anteckning**: ID för [!DNL Profile]-aktiverad måldatauppsättning används också som `datasetId` parameter. |
| `imsOrgId` | Det ID som motsvarar din organisation. |
| `datasetId` | ID:t för [!DNL Profile]-aktiverade måldatauppsättningar för ditt dataflöde. **Anteckning**: Detta är samma ID som [!DNL Profile]-aktiverat måldatauppsättnings-ID hittades i ditt dataflöde. |
| `operations` | Den här parametern visar de åtgärder som [!DNL Data Prep] baseras på den inkommande begäran. |
| `operations.data` | Definierar de åtgärder som måste utföras i [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Definierar de åtgärder som tillåts på data av [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Valfritt) ID:t för identitetsdatauppsättningen som krävs bara om nya identiteter måste länkas. |

#### Åtgärder som stöds

Följande åtgärder stöds av [!DNL Real-Time Customer Profile]:

| Användning | Beskrivning |
| --- | --- | 
| `create` | Standardåtgärden. Detta genererar en XDM-metod för att skapa en enhet för [!DNL Real-Time Customer Profile]. |
| `merge` | Detta genererar en XDM-entitetsuppdateringsmetod för [!DNL Real-Time Customer Profile]. |
| `delete` | Detta genererar en XDM-metod för entitetsborttagning för [!DNL Real-Time Customer Profile] och permanent tar bort data från [!DNL Profile Store]. |

Följande åtgärder stöds av [!DNL Identity Service]:

| Användning | Beskrivning |
| --- | --- |
| `create` | Den enda tillåtna åtgärden för den här parametern. If `create` skickas som ett värde för `operations.identity`sedan [!DNL Data Prep] genererar en XDM-entitetsskapandebegäran för [!DNL Identity Service]. Om identiteten redan finns ignoreras identiteten. **Obs!** If `operations.identity` är inställd på `create`och sedan `identityDatasetId` måste också anges. XDM-entiteten skapar meddelanden som genererats internt av [!DNL Data Prep] kommer att genereras för detta datauppsättnings-ID. |

### Nyttolast utan identitetskonfiguration

Om nya identiteter inte behöver länkas kan du utelämna `identity` och `identityDatasetId` parametrar i operationerna. Om du gör det skickas endast data till [!DNL Real-Time Customer Profile] och hoppar över [!DNL Identity Service]. Se nyttolasten nedan för exempel:

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## Skicka primära identiteter dynamiskt

För XDM-uppdateringar måste schemat aktiveras för [!DNL Profile] och innehåller en primär identitet. Du kan ange den primära identiteten för ett XDM-schema på två sätt:

* Ange ett statiskt fält som primär identitet i XDM-schemat.
* Ange ett av identitetsfälten som primär identitet via fältgruppen för identitetskarta i XDM-schemat.

### Ange ett statiskt fält som primärt identitetsfält i XDM-schemat

I exemplet nedan `state`, `homePhone.number` och andra attribut ersätts med sina respektive givna värden i [!DNL Profile] med den primära identiteten för `sampleEmail@gmail.com`. Ett uppdateringsmeddelande för en XDM-enhet genereras sedan av direktuppspelningen [!DNL Data Prep] -komponenten. [!DNL Real-Time Customer Profile] bekräftar sedan att XDM-uppdateringsmeddelandet ska infoga profilposten.

>[!NOTE]
>
>I det här exemplet kommer identiteter inte att länkas ihop eftersom inga åtgärder har definierats för identiteten.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### Ange ett av identitetsfälten som primär identitet via fältgruppen för identitetsmappning i XDM-schemat

I det här exemplet innehåller rubriken `operations` attributet med `identity` och `identityDatasetId` egenskaper. Detta gör att data kan sammanfogas med [!DNL Real-Time Customer Profile] och även för identiteter som ska skickas till [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## Kända begränsningar och viktiga överväganden

Följande visar en lista med kända begränsningar att tänka på vid direktuppspelning med [!DNL Data Prep]:

* Metoden för direktuppspelning av överföringar bör endast användas när partiella raduppdateringar skickas till [!DNL Real-Time Customer Profile]. Uppdateringar av delar av rader är **not** som konsumeras av en datasjö.
* Metoden för att skicka direktuppspelning stöder inte uppdatering, ersättning och borttagning av identiteter. Nya identiteter skapas om de inte finns. Därför är `identity` måste alltid anges för att skapa. Om en identitet redan finns är åtgärden no-op.
* Metoden för direktuppspelning stöder för närvarande inte [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) och [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Nästa steg

Genom att läsa det här dokumentet bör du nu förstå hur du direktuppspelar överföringar i [!DNL Data Prep] för att skicka uppdateringar av delar av rader till [!DNL Real-Time Customer Profile] data, samtidigt som du skapar och länkar identiteter med en enda API-begäran. Mer information om andra [!DNL Data Prep] funktioner, läs [[!DNL Data Prep] översikt](./home.md). Så här använder du mappningsuppsättningar i [!DNL Data Prep] API, läs [[!DNL Data Prep] utvecklarhandbok](./api/overview.md).
