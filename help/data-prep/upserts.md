---
keywords: Experience Platform;home;populära topics;data prep;data prep;streaming;upsert;streaming upsert
title: Skicka uppdateringar av delar av rader till kundprofil i realtid med hjälp av Data Prep
description: Lär dig hur du skickar uppdateringar av delar av rader till kundprofilen i realtid med Data Prep.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# Skicka uppdateringar av delar av rader till [!DNL Real-Time Customer Profile] med [!DNL Data Prep]

>[!IMPORTANT]
>
>* Inmatning av XDM-meddelanden (Experience Data Model) för entitetsuppdatering (med JSON PATCH-åtgärder) för profiluppdateringar via DCS-inloppet har tagits bort. Följ stegen som beskrivs i den här handboken som ett alternativ.
>
>* Du kan också använda HTTP API-källan för att [importera rådata till DCS-inloppet](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) och ange nödvändiga datamappningar för att omvandla dina data till XDM-kompatibla meddelanden för profiluppdateringar.
>
>* När du använder arrayer i direktuppspelande upserts måste du uttryckligen använda `upsert_array_append` eller `upsert_array_replace` för att definiera en rensad metod för åtgärden. Du kan få felmeddelanden om dessa funktioner saknas.

Använd direktuppspelande upserts i [!DNL Data Prep] för att skicka uppdateringar (del av rad) till [!DNL Real-Time Customer Profile]-data samtidigt som nya identitetslänkar skapas och etableras med en enda API-begäran.

Genom att direktuppspela uppladdningar kan du behålla dataformatet samtidigt som du översätter dessa data till [!DNL Real-Time Customer Profile] PATCH-förfrågningar under importen. Baserat på de indata du anger kan du i [!DNL Data Prep] skicka en enda API-nyttolast och översätta data till både [!DNL Real-Time Customer Profile] PATCH- och [!DNL Identity Service] CREATE-begäranden.

[!DNL Data Prep] använder rubrikparametrar för att skilja mellan infogningar och infogningar. Alla rader som använder upserts måste ha en rubrik. Du kan använda upserts med eller utan identitetsbeskrivare. Om du använder överföringar med identiteter måste du följa de konfigurationssteg som beskrivs i avsnittet [Konfigurera identitetsdatauppsättningen](#configure-the-identity-dataset). Om du använder överföringar utan identiteter behöver du inte ange några identitetskonfigurationer i din begäran. Läs avsnittet om [direktuppspelande överföringar utan identiteter](#payload-without-identity-configuration) om du vill ha mer information.

>[!NOTE]
>
>Om du vill utnyttja uppgraderingsfunktionen rekommenderar vi att du inaktiverar XDM-kompatibla konfigurationer under datainmatning och mappar om inkommande nyttolast med [Data Prep Mapper](./ui/mapping.md).

Det här dokumentet innehåller information om hur du direktuppspelar överföringar i [!DNL Data Prep].

## Komma igång

Den här översikten kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
* [Kundprofil i realtid](../profile/home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [Källor](../sources/home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.

## Använd direktuppspelande upserts i [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Följande källor har stöd för direktuppspelande upserts:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Direktuppspelning ger ett arbetsflöde på hög nivå

Direktuppspelande uppdateringar i [!DNL Data Prep] fungerar så här:

* Du måste först skapa och aktivera en datauppsättning för [!DNL Profile]-förbrukning. Mer information finns i guiden [Aktivera en datauppsättning för  [!DNL Profile]](../catalog/datasets/enable-for-profile.md).
* Om nya identiteter måste länkas måste du också skapa ytterligare en datamängd **med samma schema** som [!DNL Profile]-datamängden.
* När datauppsättningarna har förberetts måste du skapa ett dataflöde för att mappa din inkommande begäran till datauppsättningen [!DNL Profile].
* Därefter måste du uppdatera den inkommande begäran så att de nödvändiga rubrikerna inkluderas. Dessa rubriker definierar:
   * Den dataåtgärd som krävs för att utföras med [!DNL Profile]: `create`, `merge` och `delete`.
   * Den valfria identitetsåtgärden som ska utföras med [!DNL Identity Service]: `create`.

### Konfigurera identitetsdatauppsättningen {#configure-the-identity-dataset}

Om nya identiteter måste länkas måste du skapa och skicka ytterligare en datauppsättning i den inkommande nyttolasten. När du skapar en identitetsdatauppsättning måste du se till att följande krav uppfylls:

* Identitetsdatauppsättningen måste ha sitt associerade schema som datamängden [!DNL Profile]. Om scheman inte matchar kan det leda till inkonsekvent systembeteende.
* Du måste dock se till att identitetsdatauppsättningen skiljer sig från datauppsättningen [!DNL Profile]. Om datauppsättningarna är desamma skrivs data över i stället för att uppdateras.
* Även om den initiala datauppsättningen måste aktiveras för [!DNL Profile], ska identitetsdatauppsättningen **inte aktiveras** för [!DNL Profile]. Annars skrivs data också över i stället för att uppdateras. Identitetsdatauppsättningen **bör dock aktiveras** för [!DNL Identity Service].

#### Obligatoriska fält i scheman som är associerade med identitetsdatauppsättningen {#identity-dataset-required-fileds}

Om schemat innehåller obligatoriska fält måste verifieringen av datauppsättningen ignoreras för att [!DNL Identity Service] bara ska kunna ta emot identiteterna. Du kan inaktivera valideringen genom att tillämpa värdet `disabled` på parametern `acp_validationContext`. Se exemplet nedan:

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
| `flowId` | Ett unikt ID som identifierar ett dataflöde. Detta dataflödes-ID ska motsvara den källanslutning som skapats med [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] eller [!DNL HTTP API]. Det här dataflödet ska även ha en [!DNL Profile]-aktiverad datauppsättning som måldatauppsättning. **Obs!**: ID:t för den [!DNL Profile]-aktiverade måldatauppsättningen används också som `datasetId` -parameter. |
| `imsOrgId` | Det ID som motsvarar din organisation. |
| `datasetId` | ID för det [!DNL Profile]-aktiverade måldatauppsättningen för ditt dataflöde. **Obs!**: Detta är samma ID som det [!DNL Profile]-aktiverade måldatauppsättnings-ID som finns i ditt dataflöde. |
| `operations` | Den här parametern visar de åtgärder som [!DNL Data Prep] kommer att utföra baserat på den inkommande begäran. |
| `operations.data` | Definierar de åtgärder som måste utföras i [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Definierar de åtgärder som tillåts på data av [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Valfritt) ID:t för identitetsdatauppsättningen som krävs bara om nya identiteter måste länkas. |

#### Åtgärder som stöds

Följande åtgärder stöds av [!DNL Real-Time Customer Profile]:

| Användning | Beskrivning |
| --- | --- | 
| `create` | Standardåtgärden. Detta genererar en XDM-entitetsskapandemetod för [!DNL Real-Time Customer Profile]. |
| `merge` | Detta genererar en XDM-entitetsuppdateringsmetod för [!DNL Real-Time Customer Profile]. |
| `delete` | Detta genererar en XDM-entitetsborttagningsmetod för [!DNL Real-Time Customer Profile] och tar permanent bort data från [!DNL Profile store]. |

Följande åtgärder stöds av [!DNL Identity Service]:

| Användning | Beskrivning |
| --- | --- |
| `create` | Den enda tillåtna åtgärden för den här parametern. Om `create` skickas som ett värde för `operations.identity` genererar [!DNL Data Prep] en XDM-entitetsskapandebegäran för [!DNL Identity Service]. Om identiteten redan finns ignoreras identiteten. **Obs!** Om `operations.identity` är `create` måste även `identityDatasetId` anges. Det XDM-entitetsmeddelande som skapas internt av komponenten [!DNL Data Prep] kommer att genereras för det här datauppsättnings-ID:t. |

### Nyttolast utan identitetskonfiguration {#payload-without-identity-configuration}

Om nya identiteter inte behöver länkas kan du utelämna parametrarna `identity` och `identityDatasetId` i åtgärderna. Om du gör det skickas endast data till [!DNL Real-Time Customer Profile] och [!DNL Identity Service] hoppas över. Se nyttolasten nedan för exempel:

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

För XDM-uppdateringar måste schemat aktiveras för [!DNL Profile] och innehålla en primär identitet. Du kan ange den primära identiteten för ett XDM-schema på två sätt:

* Ange ett statiskt fält som primär identitet i XDM-schemat.
* Ange ett av identitetsfälten som primär identitet via fältgruppen för identitetskarta i XDM-schemat.

### Ange ett statiskt fält som primärt identitetsfält i XDM-schemat

I exemplet nedan har `state`, `homePhone.number` och andra attribut uppdaterats med sina respektive angivna värden till [!DNL Profile] med den primära identiteten `sampleEmail@gmail.com`. Ett uppdateringsmeddelande för en XDM-entitet genereras sedan av den direktuppspelade komponenten [!DNL Data Prep]. [!DNL Real-Time Customer Profile] bekräftar sedan att XDM-uppdateringsmeddelandet ska infoga profilposten.

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

I det här exemplet innehåller rubriken attributet `operations` med egenskaperna `identity` och `identityDatasetId`. Detta gör att data kan sammanfogas med [!DNL Real-Time Customer Profile] och även för identiteter som ska skickas till [!DNL Identity Service].

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

Följande visar en lista med kända begränsningar som ska beaktas när direktuppspelning överförs med [!DNL Data Prep]:

* Metoden för direktuppspelning av överföringar bör bara användas när partiella raduppdateringar skickas till [!DNL Real-Time Customer Profile]. Uppdateringar av partiella rader används **inte** av datavagn.
* Metoden för att skicka direktuppspelning stöder inte uppdatering, ersättning och borttagning av identiteter. Nya identiteter skapas om de inte finns. Därför måste `identity`-åtgärden alltid anges för att skapa. Om en identitet redan finns är åtgärden no-op.
* Metoden för direktuppspelning stöder för närvarande inte [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) och [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Nästa steg

Genom att läsa det här dokumentet bör du nu förstå hur du direktuppspelar överföringar i [!DNL Data Prep] för att skicka uppdateringar av delar av rader till dina [!DNL Real-Time Customer Profile]-data, samtidigt som du skapar och länkar identiteter med en enda API-begäran. Mer information om andra [!DNL Data Prep]-funktioner finns i [[!DNL Data Prep] översikten](./home.md). Läs [[!DNL Data Prep] utvecklarhandboken](./api/overview.md) om du vill lära dig hur du använder mappningsuppsättningar i [!DNL Data Prep]-API:t.
