---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvärdera ett segment
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 0%

---


# Utvärdera och få tillgång till segmentresultaten

I det här dokumentet finns en självstudiekurs för att utvärdera segment och komma åt segmentresultat med hjälp av [Segmenterings-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används för att skapa målgruppssegment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
- [Segmenteringstjänsten](../home.md)Adobe Experience Platform: Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.
- [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Obligatoriska rubriker

Den här självstudiekursen kräver även att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna ringa anrop till Platform API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla POST-, PUT- och PATCH-begäranden kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Utvärdera ett segment

När du har utvecklat, testat och sparat din segmentdefinition kan du sedan utvärdera segmentet med hjälp av en schemalagd utvärdering eller on-demand-utvärdering.

[Med schemalagd utvärdering](#scheduled-evaluation) (även kallat schemalagd segmentering) kan du skapa ett återkommande schema för körning av ett exportjobb vid en viss tidpunkt, medan [on demand-utvärdering](#on-demand-evaluation) innebär att du skapar ett segmentjobb för att skapa målgruppen direkt. Stegen för varje steg beskrivs nedan.

Om du ännu inte har slutfört [Skapa ett segment med hjälp av självstudiekursen för kundprofils-API](./create-a-segment.md) i realtid eller skapat en segmentdefinition med hjälp av [Segment Builder](../ui/overview.md)gör du det innan du fortsätter med den här självstudiekursen.

## Schemalagd utvärdering {#scheduled-evaulation}

Med hjälp av schemalagd utvärdering kan din IMS-organisation skapa ett återkommande schema som automatiskt kör exportjobb.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanslagningsprinciper för den enskilda XDM-profilen. Om din organisation har fler än fem sammanfogningsprinciper för den enskilda XDM-profilen i en enda sandlådemiljö, kommer du inte att kunna använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en POST-begäran till `/config/schedules` slutpunkten kan du skapa ett schema och inkludera den specifika tid då schemat ska utlösas.

**API-format**

```http
POST /config/schedules
```

**Begäran**

Följande begäran skapar ett nytt schema baserat på specifikationerna i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | **(Obligatoriskt)** Schemats namn. Måste vara en sträng. |
| `type` | **(Obligatoriskt)** Jobbtypen i strängformat. De typer som stöds är `batch_segmentation` och `export`. |
| `properties` | **(Obligatoriskt)** Ett objekt som innehåller ytterligare egenskaper som är relaterade till schemat. |
| `properties.segments` | **(Krävs när`type`är lika med`batch_segmentation`)** Om du använder `["*"]` inkluderas alla segment. |
| `schedule` | **(Obligatoriskt)** En sträng som innehåller jobbschemat. Jobb kan bara schemaläggas att köras en gång om dagen, vilket innebär att du inte kan schemalägga ett jobb att köras mer än en gång under en 24-timmarsperiod. Det exempel som visas (`0 0 1 * * ?`) innebär att jobbet utlöses varje dag kl. 1:00:00 UTC. Mer information finns i dokumentationen för [cron expression](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . |
| `state` | *(Valfritt)* Sträng som innehåller schemat. Tillgängliga värden: `active` och `inactive`. Standardvärdet är `inactive`. En IMS-organisation kan bara skapa ett schema. Steg för att uppdatera schemat är tillgängliga senare i den här självstudiekursen. |

**Svar**

Ett lyckat svar returnerar information om det nya schemat.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### Aktivera ett schema

Som standard är ett schema inaktivt när det skapas, såvida inte `state` egenskapen är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en PATCH-begäran till `/config/schedules` slutpunkten och inkludera ID:t för schemat i sökvägen.

**API-format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Begäran**

Följande begäran använder [JSON Patch-formatering](http://jsonpatch.com/) för att uppdatera `state` schemat till `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Svar**

En lyckad uppdatering returnerar en tom svarstext och HTTP-status 2004 (inget innehåll).

Samma åtgärd kan användas för att inaktivera ett schema genom att ersätta värdet i föregående begäran med inaktivt.

### Uppdatera schematiden

Tidsplaneringen kan uppdateras genom att en PATCH-begäran görs till `/config/schedules` slutpunkten och med ID:t för schemat i sökvägen.

**API-format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Begäran**

Följande begäran använder [JSON Patch-formatering](http://jsonpatch.com/) för att uppdatera [cron-uttrycket](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) för schemat. I det här exemplet utlöses schemat 10:15:00 UTC.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**Svar**

En lyckad uppdatering returnerar en tom svarstext och HTTP-status 2004 (inget innehåll).

## On-demand-utvärdering

Med On-demand-utvärdering kan ni skapa ett segmentjobb för att generera ett målgruppssegment när ni behöver det. Till skillnad från schemalagd utvärdering kommer detta endast att ske när det begärs och inte är återkommande.

### Skapa ett segmentjobb

Ett segmentjobb är en asynkron process som skapar ett nytt målgruppssegment. Det refererar till en segmentdefinition samt eventuella sammanfogningsprinciper som styr hur kundprofilen i realtid sammanfogar överlappande attribut i dina profilfragment. När ett segmentjobb har slutförts kan du samla in olika typer av information om segmentet, t.ex. eventuella fel som kan ha inträffat under bearbetningen och målgruppens slutliga storlek.

Du kan skapa ett nytt segmentjobb genom att göra en POST-begäran till `/segment/jobs` slutpunkten i kundprofils-API:t i realtid.

**API-format**

```http
POST /segment/jobs
```

**Begäran**

Följande begäran skapar ett nytt segmentjobb baserat på de två segmentdefinitionerna som finns i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segmentId` | Identifieraren för en segmentdefinition som målgruppen ska baseras på. Minst ett segment-ID måste anges i nyttolastmatrisen. |

**Svar**

Ett lyckat svar returnerar information om det nyligen skapade segmentjobbet, inklusive dess `id`, ett skrivskyddat systemgenererat värde som är unikt för segmentjobbet.

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Identifieraren för det nya segmentjobbet, som används i sökningssyfte. |
| `status` | Segmentjobbets aktuella status. Kommer att &quot;BEARBETAS&quot; tills bearbetningen är klar, och då blir den &quot;LYCKAD&quot; eller &quot;MISSLYCKAD&quot;. |

### Sök efter jobbstatus för segment

Du kan använda `id` för ett specifikt segmentjobb för att utföra en sökbegäran (GET) för att visa jobbets aktuella status.

**API-format**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | The `id` of the segment job you want to access. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar information om segmenteringsjobbet och ger olika information beroende på jobbets aktuella status. Du kan upprepa sökningen tills `status` &quot;LYCKADES&quot; nås. Då kan du exportera segmentet till en datauppsättning.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segmentedProfileCounter` | Det totala antalet sammanfogade profiler som är kvalificerade för segmentet. |
| `segmentedProfileByNamespaceCounter` | En uppdelning av de profiler som är kvalificerade för segmentet efter ID-namnområdeskod. En lista med identitetsnamnutrymmeskoder finns i [namnutrymmesöversikten](../../identity-service/namespaces.md). |

## Tolka segmentresultat

När segmentjobben körs uppdateras kartan för varje profil som ingår i segmentet `segmentMembership` . `segmentMembership` lagrar också alla förutvärderade målgruppssegment som är inkapslade i Platform, vilket möjliggör integrering med andra lösningar som Adobe Audience Manager.

I följande exempel visas hur attributet ser ut `segmentMembership` för varje enskild profilpost:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `lastQualificationTime` | Tidsstämpeln när kontrollen av segmentmedlemskapet gjordes och profilen angavs eller avslutades. |
| `status` | Status för segmentdeltagande som en del av den aktuella begäran. Måste vara lika med ett av följande kända värden: <ul><li>`existing`: Enheten fortsätter att vara i segmentet.</li><li>`realized`: Enheten går in i segmentet.</li><li>`exited`: Enheten avslutar segmentet.</li></ul> |

## Åtkomst till segmentresultat

Resultatet av ett segmentjobb kan nås på ett av två sätt: kan du komma åt enskilda profiler eller exportera en hel publik till en datauppsättning.

I följande avsnitt beskrivs dessa alternativ mer ingående.

## Söka efter en profil

Om du vet vilken profil du vill använda kan du göra det med kundprofils-API:t i realtid. De fullständiga stegen för att komma åt enskilda profiler finns i [Access-kundprofildata i realtid med hjälp av API](../../profile/api/entities.md) -självstudiekursen för profiler.

## Exportera ett segment {#export}

När ett segmenteringsjobb har slutförts (värdet för `status` attributet är &quot;SUCCEEDED&quot;) kan du exportera målgruppen till en datauppsättning där den kan nås och hanteras.

Följande steg krävs för att exportera målgruppen:

- [Skapa en måldatauppsättning](#create-a-target-dataset) - Skapa datauppsättningen för målgruppsmedlemmar.
- [Generera målgruppsprofiler i datauppsättningen](#generate-profiles-for-audience-members) - Fyll i datauppsättningen med enskilda XDM-profiler baserat på resultatet av ett segmentjobb.
- [Övervaka exportförloppet](#monitor-export-progress) - Kontrollera exportförloppet.
- [Läs målgruppsdata](#next-steps) - Hämta de resulterande XDM-individuella profilerna som representerar medlemmarna i din publik.

### Skapa en måldatauppsättning

När du exporterar en målgrupp måste du först skapa en måldatauppsättning. Det är viktigt att datauppsättningen är korrekt konfigurerad för att exporten ska lyckas.

En av de viktigaste sakerna att tänka på är det schema som datauppsättningen baseras på (`schemaRef.id` i API-exempelbegäran nedan). För att kunna exportera ett segment måste datauppsättningen baseras på XDM Individual Profile Union Schema (`https://ns.adobe.com/xdm/context/profile__union`). Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar in fält i scheman som delar samma klass, i det här fallet klassen XDM Individual Profile. Mer information om unionsvyscheman finns i avsnittet Kundprofil i [realtid i Utvecklarhandbok](../../xdm/api/getting-started.md)för schemaregister.

Det finns två sätt att skapa den nödvändiga datauppsättningen:

- **Använda API:er:** De steg som följer i den här självstudien beskriver hur du skapar en datauppsättning som refererar till XDM-schemat för enskilda profiler med hjälp av katalog-API:t.
- **Använda gränssnittet:** Om du vill använda användargränssnittet i Adobe Experience Platform för att skapa en datauppsättning som refererar till unionsschemat, följer du stegen i [användargränssnittet](../ui/overview.md) och går sedan tillbaka till den här självstudiekursen för att fortsätta med stegen för att [generera målgruppsprofiler](#generate-xdm-profiles-for-audience-members).

Om du redan har en kompatibel datauppsättning och känner till dess ID kan du fortsätta direkt till steget för att [generera målgruppsprofiler](#generate-xdm-profiles-for-audience-members).

**API-format**

```http
POST /dataSets
```

**Begäran**

Följande begäran skapar en ny datauppsättning med konfigurationsparametrar i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Ett beskrivande namn för datauppsättningen. |
| `schemaRef.id` | ID för den unionsvy (schema) som datauppsättningen ska kopplas till. |
| `fileDescription.persisted` | Ett booleskt värde som, när det anges till `true`, gör att datauppsättningen kan finnas kvar i unionsvyn. |

**Svar**

Ett lyckat svar returnerar en array som innehåller det skrivskyddade, systemgenererade unika ID:t för den nya datauppsättningen. Ett korrekt konfigurerat datauppsättnings-ID krävs för att målgruppsmedlemmar ska kunna exporteras.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generera profiler för målgruppsmedlemmar

När du har en enhetlig datauppsättning som är beständig kan du skapa ett exportjobb som behåller målgruppsmedlemmarna i datauppsättningen genom att göra en POST-begäran till `/export/jobs` slutpunkten i kundprofils-API:t i realtid och ange datauppsättnings-ID och segmentinformationen för de segment som du vill exportera.

**API-format**

```http
POST /export/jobs
```

**Begäran**

Följande begäran skapar ett nytt exportjobb med konfigurationsparametrar i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `fields` | *(Valfritt)* Begränsar datafälten som ska inkluderas i exporten till endast de som anges i den här parametern. Samma parameter är också tillgänglig när du skapar ett segment, och därför kan fälten i segmentet redan ha filtrerats. Om du utelämnar det här värdet inkluderas alla fält i exporterade data |
| `mergePolicy` | *(Valfritt)* Anger vilken sammanfogningsprincip som ska styra exporterade data. Inkludera den här parametern när det finns flera segment som exporteras. Om det här värdet utelämnas används den sammanslagningsprincip som tillhandahålls av segmentet. |
| `mergePolicy.id` | ID för sammanfogningsprincipen |
| `mergePolicy.version` | Den specifika versionen av sammanfogningsprincipen som ska användas. Om du utelämnar det här värdet används den senaste versionen som standard. |
| `filter` | *(Valfritt)* Anger ett eller flera av följande filter som ska användas på segmentet före export: |
| `filter.segments` | *(Valfritt)* Anger vilka segment som ska exporteras. Om du utelämnar det här värdet exporteras alla data från alla profiler. Accepterar en array med segmentobjekt, där vart och ett innehåller följande fält: |
| `filter.segments.segmentId` | **(Krävs om du använder`segments`)** Segment-ID för profiler som ska exporteras. |
| `filter.segments.segmentNs` | *(Valfritt)* Segmentnamnutrymme för angiven `segmentID`. |
| `filter.segments.status` | *(Valfritt)* En array med strängar som tillhandahåller ett statusfilter för `segmentID`. Som standard `status` har det värde `["realized", "existing"]` som representerar alla profiler som faller inom segmentet vid den aktuella tidpunkten. Möjliga värden är: `"realized"`, `"existing"`och `"exited"`. |
| `filter.segmentQualificationTime` | *(Valfritt)* Filtrera baserat på segmentets kvalificeringstid. Starttid och/eller sluttid kan anges. |
| `filter.segmentQualificationTime.startTime` | *(Valfritt)* Starttid för segmentkvalificering för ett segment-ID för en viss status. Det anges inte, det kommer inte att finnas något filter på starttiden för ett segment-ID-kvalificering. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. |
| `filter.segmentQualificationTime.endTime` | *(Valfritt)* Sluttid för segmentkvalificering för ett segment-ID för en viss status. Det anges inte, det kommer inte att finnas något filter på sluttiden för ett segment-ID-kvalificering. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. |
| `filter.fromIngestTimestamp` | *(Valfritt)* Begränsar exporterade profiler till att endast omfatta de som har uppdaterats efter den här tidsstämpeln. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. |
| `filter.fromIngestTimestamp` för **profiler**, om sådana finns | Inkluderar alla sammanfogade profiler där den sammanfogade, uppdaterade tidsstämpeln är större än den angivna tidsstämpeln. Stöder `greater_than` operand. |
| `filter.fromTimestamp` för händelser | Alla händelser som har importerats efter den här tidsstämpeln exporteras, vilket motsvarar det resulterande profilresultatet. Detta är inte själva händelseläget utan själva intagningstiden för händelserna. |
| `filter.emptyProfiles` | *(Valfritt)* Boolean. Profiler kan innehålla profilposter, ExperienceEvent-poster eller båda. Profiler utan profilposter och bara ExperienceEvent-poster kallas&quot;emptyProfiles&quot;. Om du vill exportera alla profiler i profilarkivet, inklusive &quot;emptyProfiles&quot;, anger du värdet för `emptyProfiles` till `true`. Om `emptyProfiles` är inställt på `false`exporteras bara profiler med profilposter i butiken. Som standard exporteras bara profiler som innehåller profilposter om attributet inte ingår `emptyProfiles` . |
| `additionalFields.eventList` | *(Valfritt)* Styr tidsseriens händelsefält som exporteras för underordnade eller associerade objekt genom att ange en eller flera av följande inställningar: |
| `additionalFields.eventList.fields` | Styr fälten som ska exporteras. |
| `additionalFields.eventList.filter` | Anger villkor som begränsar resultaten från associerade objekt. Förväntar ett minimivärde som krävs för export, vanligtvis ett datum. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | Filtrerar händelser för tidsserier till händelser som har importerats efter den angivna tidsstämpeln. Detta är inte själva händelseläget utan själva intagningstiden för händelserna. |
| `destination` | **(Obligatoriskt)** Målinformation för exporterade data |
| `destination.datasetId` | **(Obligatoriskt)** ID:t för datauppsättningen där data ska exporteras. |
| `destination.segmentPerBatch` | *(Valfritt)* Ett booleskt värde som, om det inte anges, är som standard `false`. Värdet för `false` exporterar alla segment-ID:n till ett enda batch-ID. Värdet för `true` exporterar ett segment-ID till ett batch-ID. Observera att om du anger värdet som ska `true` påverkas batchexportens prestanda. |
| `schema.name` | **(Obligatoriskt)** Namnet på schemat som är associerat med datauppsättningen där data ska exporteras. |

**Svar**

Ett lyckat svar returnerar en datauppsättning ifylld med profiler som är kvalificerade för den senaste slutförda körningen av segmentjobbet. Alla profiler som tidigare fanns i datauppsättningen men inte var kvalificerade för segmentet under den senaste slutförda körningen av segmentjobbet har tagits bort.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Om `destination.segmentPerBatch` inte hade tagits med i begäran (om den inte fanns, var den som standard `false`) eller om värdet hade angetts till `false`, skulle `destination` objektet i svaret ovan inte ha någon `batches` array och i stället bara innehålla en `batchId`, vilket visas nedan. Den enskilda batchen skulle innehålla alla segment-ID, medan svaret ovan visar ett enda segment-ID per batch-ID.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### Visa alla exportjobb

Du kan returnera en lista över alla exportjobb för en viss IMS-organisation genom att utföra en GET-begäran till `export/jobs` slutpunkten. Begäran stöder också frågeparametrarna `limit` och `offset`enligt nedan.

**API-format**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `limit` | Ange antalet poster som ska returneras. |
| `offset` | Förskjut resultatsidan som ska returneras av det angivna numret. |


**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller ett `records` objekt som innehåller de exportjobb som har skapats av IMS-organisationen.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### Övervaka exportförlopp

Som exportjobbsprocesser kan du övervaka dess status genom att göra en GET-begäran till `/export/jobs` slutpunkten och inkludera `id` exportjobbets status i sökvägen. Exportjobbet slutförs när `status` fältet returnerar värdet &quot;SUCCEEDED&quot;.

**API-format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to access. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `batchId` | Identifieraren för de batchar som har skapats från en lyckad export och som ska användas för sökning när målgruppsdata läses. |

## Nästa steg

När exporten är klar är dina data tillgängliga i Data Lake i Experience Platform. Du kan sedan använda API:t [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dataåtkomst för att komma åt data med hjälp av de `batchId` som är kopplade till exporten. Beroende på segmentets storlek kan data vara i segment och gruppen kan bestå av flera filer.

Följ självstudiekursen ( [Data Access) om du vill ha stegvisa anvisningar om hur du använder API:t för dataåtkomst för att få åtkomst till och hämta gruppfiler](../../data-access/tutorials/dataset-data.md).

Du kan också komma åt exporterade segmentdata med Adobe Experience Platform Query Service. Med API:t UI eller RESTful kan du med Query Service skriva, validera och köra frågor på data i Data Lake.

Mer information om hur du frågar efter målgruppsdata finns i dokumentationen [för](../../query-service/home.md)frågetjänsten.
