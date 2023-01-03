---
keywords: Experience Platform;hemmabruk;populära ämnen;segmentutvärdering;segmenteringstjänst;segmentering;segmentering;utvärdera ett segment;nå segmentresultat;utvärdera och ge åtkomst till segment;
solution: Experience Platform
title: Utvärdera och få åtkomst till segmentresultat
topic-legacy: tutorial
type: Tutorial
description: Följ den här självstudiekursen för att lära dig hur du utvärderar segment och får åtkomst till segmentresultat med Adobe Experience Platform Segmenteringstjänstens API.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# Utvärdera och få tillgång till segmentresultaten

I det här dokumentet finns en självstudiekurs för att utvärdera segment och komma åt segmentresultat med [[!DNL Segmentation API]](../api/getting-started.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för de olika [!DNL Adobe Experience Platform] tjänster som används för att skapa målgruppssegment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Gör att ni kan skapa målgruppssegment utifrån [!DNL Real-Time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Obligatoriska rubriker

Den här självstudiekursen kräver även att du har slutfört [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att kunna ringa [!DNL Platform] API:er. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla förfrågningar från POST, PUT och PATCH kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Utvärdera ett segment {#evaluate-a-segment}

När du har utvecklat, testat och sparat din segmentdefinition kan du sedan utvärdera segmentet med hjälp av en schemalagd utvärdering eller on-demand-utvärdering.

[Schemalagd utvärdering](#scheduled-evaluation) (kallas även&quot;schemalagd segmentering&quot;) kan du skapa ett återkommande schema för att köra ett exportjobb vid en viss tidpunkt, medan [on demand-utvärdering](#on-demand-evaluation) innebär att skapa ett segmentjobb för att omedelbart bygga upp målgruppen. Stegen för varje steg beskrivs nedan.

Om du ännu inte har slutfört [skapa ett segment med segmenterings-API](./create-a-segment.md) självstudiekurs eller skapa en segmentdefinition med [Segment Builder](../ui/overview.md)gör du det innan du fortsätter med kursen.

## Schemalagd utvärdering {#scheduled-evaluation}

Med hjälp av schemalagd utvärdering kan din IMS-organisation skapa ett återkommande schema som automatiskt kör exportjobb.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanfogningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem samkörningspolicyer för [!DNL XDM Individual Profile] i en enda sandlådemiljö kommer du inte att kunna använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en POST-förfrågan till `/config/schedules` kan du skapa ett schema och inkludera den specifika tidpunkt då schemat ska utlösas.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandbok för scheman](../api/schedules.md#create)

### Aktivera ett schema

Som standard är ett schema inaktivt när det skapas såvida inte `state` egenskapen är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en begäran från PATCH till `/config/schedules` slutpunkten och inklusive ID för schemat i sökvägen.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandbok för scheman](../api/schedules.md#update-state)

### Uppdatera schematiden

Tidsplaneringen kan uppdateras genom att PATCH begär `/config/schedules` slutpunkten och inklusive ID för schemat i sökvägen.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandbok för scheman](../api/schedules.md#update-schedule)

## On-demand-utvärdering

Med On-demand-utvärdering kan ni skapa ett segmentjobb för att generera ett målgruppssegment när ni behöver det. Till skillnad från schemalagd utvärdering kommer detta endast att ske när det begärs och inte är återkommande.

### Skapa ett segmentjobb

Ett segmentjobb är en asynkron process som skapar ett målgruppssegment på begäran. Det refererar till en segmentdefinition samt eventuella sammanfogningsprinciper som styr hur [!DNL Real-Time Customer Profile] sammanfogar överlappande attribut i dina profilfragment. När ett segmentjobb har slutförts kan du samla in olika typer av information om segmentet, t.ex. eventuella fel som kan ha inträffat under bearbetningen och målgruppens slutliga storlek. Ett segmentjobb måste köras varje gång du vill uppdatera den målgrupp som för närvarande är kvalificerad för segmentdefinitionen.

Du kan skapa ett nytt segmentjobb genom att göra en POST-förfrågan till `/segment/jobs` slutpunkt i [!DNL Real-Time Customer Profile] API.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktsguide för segmentjobb](../api/segment-jobs.md#create)

### Sök efter jobbstatus för segment

Du kan använda `id` för ett specifikt segmentjobb att utföra en sökbegäran (GET) för att visa jobbets aktuella status.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktsguide för segmentjobb](../api/segment-jobs.md#get)

## Tolka segmentresultat

När segmentjobben har körts `segmentMembership` kartan uppdateras för varje profil som ingår i segmentet. `segmentMembership` lagrar även alla förutvärderade målgruppssegment som är inkapslade i [!DNL Platform], vilket möjliggör integrering med andra lösningar som [!DNL Adobe Audience Manager].

I följande exempel visas vad `segmentMembership` för varje enskild profilpost ser attributet ut så här:

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

Om du vet vilken profil du vill använda kan du göra det med [!DNL Real-Time Customer Profile] API. De fullständiga stegen för att komma åt enskilda profiler finns i [Få åtkomst till kundprofildata i realtid med profils-API](../../profile/api/entities.md) självstudiekurs.

## Exportera ett segment {#export}

När ett segmenteringsjobb har slutförts (värdet på `status` -attributet är &quot;SUCCEEDED&quot;), kan du exportera målgruppen till en datauppsättning där den kan nås och hanteras.

Följande steg krävs för att exportera målgruppen:

- [Skapa en måldatauppsättning](#create-a-target-dataset) - Skapa datauppsättningen för målgruppsmedlemmar.
- [Generera målgruppsprofiler i datauppsättningen](#generate-profiles) - Fyll i datauppsättningen med enskilda XDM-profiler baserat på resultatet av ett segmentjobb.
- [Övervaka exportförlopp](#monitor-export-progress) - Kontrollera exportförloppet.
- [Läs målgruppsdata](#next-steps) - Hämta de resulterande enskilda XDM-profilerna som representerar medlemmarna i din publik.

### Skapa en måldatauppsättning {#create-dataset}

När du exporterar en målgrupp måste du först skapa en måldatauppsättning. Det är viktigt att datauppsättningen är korrekt konfigurerad för att exporten ska lyckas.

Ett av de viktigaste övervägandena är schemat som datauppsättningen baseras på (`schemaRef.id` i API-exempelbegäran nedan). För att kunna exportera ett segment måste datauppsättningen baseras på [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar in fält i scheman som delar samma klass, i det här fallet klassen XDM Individual Profile. Mer information om unionens vyscheman finns i [Avsnittet Kundprofil i realtid i utvecklarhandboken för schemaregistret](../../xdm/api/getting-started.md).

Det finns två sätt att skapa den nödvändiga datauppsättningen:

- **Använda API:er:** Stegen som följer i den här självstudiekursen visar hur du skapar en datauppsättning som refererar till [!DNL XDM Individual Profile Union Schema] med [!DNL Catalog] API.
- **Använda gränssnittet:** Så här använder du [!DNL Adobe Experience Platform] om du vill skapa en datauppsättning som refererar till unionsschemat följer du stegen i [Självstudiekurs om användargränssnitt](../ui/overview.md) och sedan gå tillbaka till den här självstudiekursen för att fortsätta [generera målgruppsprofiler](#generate-profiles).

Om du redan har en kompatibel datauppsättning och känner till dess ID kan du fortsätta direkt till steget för [generera målgruppsprofiler](#generate-profiles).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Ett beskrivande namn för datauppsättningen. |
| `schemaRef.id` | ID för den unionsvy (schema) som datauppsättningen ska kopplas till. |

**Svar**

Ett lyckat svar returnerar en array som innehåller det skrivskyddade, systemgenererade unika ID:t för den nya datauppsättningen. Ett korrekt konfigurerat datauppsättnings-ID krävs för att målgruppsmedlemmar ska kunna exporteras.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generera profiler för målgruppsmedlemmar {#generate-profiles}

När du har en enhetlig datauppsättning som är beständig kan du skapa ett exportjobb som behåller målgruppsmedlemmarna i datauppsättningen genom att göra en begäran om POST till `/export/jobs` slutpunkt i [!DNL Real-Time Customer Profile] API och ange datauppsättnings-ID och segmentinformation för de segment som du vill exportera.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktsguide för exportjobb](../api/export-jobs.md#create)

### Övervaka exportförlopp

Som en exportjobbsprocess kan du övervaka dess status genom att göra en GET-förfrågan till `/export/jobs` slutpunkt och inklusive `id` av exportjobbet i sökvägen. Exportjobbet är klart när `status` returnerar värdet &quot;SUCCEEDED&quot;.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktsguide för exportjobb](../api/export-jobs.md#get)

## Nästa steg

När exporten är klar är dina data tillgängliga i [!DNL Data Lake] in [!DNL Experience Platform]. Du kan sedan använda [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) för att få åtkomst till data med `batchId` som är kopplad till exporten. Beroende på segmentets storlek kan data vara i segment och gruppen kan bestå av flera filer.

Stegvisa instruktioner om hur du använder [!DNL Data Access] API för att få tillgång till och ladda ned batchfiler, följ [Dataåtkomst, genomgång](../../data-access/tutorials/dataset-data.md).

Du kan också komma åt exporterade segmentdata med [!DNL Adobe Experience Platform Query Service]. Använda gränssnittet eller RESTful API, [!DNL Query Service] kan du skriva, validera och köra frågor på data i [!DNL Data Lake].

Mer information om hur man hämtar information finns i dokumentationen om [[!DNL Query Service]](../../query-service/home.md).
