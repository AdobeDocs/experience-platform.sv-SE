---
keywords: Experience Platform;hemmabruk;populära ämnen;segmentutvärdering;segmenteringstjänst;segmentering;segmentering;utvärdera ett segment;nå segmentresultat;utvärdera och ge åtkomst till segment;
solution: Experience Platform
title: Utvärdera och få åtkomst till segmentresultat
topic: självstudiekurs
type: Tutorial
description: Följ den här självstudiekursen för att lära dig hur du utvärderar segment och får åtkomst till segmentresultat med Adobe Experience Platform Segmenteringstjänstens API.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# Utvärdera och få tillgång till segmentresultaten

I det här dokumentet finns en självstudiekurs för att utvärdera segment och komma åt segmentresultat med [[!DNL Segmentation API]](../api/getting-started.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänsterna som används för att skapa målgruppssegment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Gör att ni kan skapa målgruppssegment utifrån  [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
- [Sandlådor](../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Obligatoriska rubriker

I den här självstudien måste du också ha slutfört [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa [!DNL Platform] API:er. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Begäranden till [!DNL Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla förfrågningar från POST, PUT och PATCH kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Utvärdera ett segment

När du har utvecklat, testat och sparat din segmentdefinition kan du sedan utvärdera segmentet med hjälp av en schemalagd utvärdering eller on-demand-utvärdering.

[Med schemalagd utvärdering](#scheduled-evaluation)  (även kallat schemalagd segmentering) kan du skapa ett återkommande schema för att köra ett exportjobb vid en viss tidpunkt, medan  [on-demand-](#on-demand-evaluation) utvärdering innebär att du skapar ett segmentjobb för att skapa målgruppen direkt. Stegen för varje steg beskrivs nedan.

Om du ännu inte har slutfört [skapa ett segment med hjälp av självstudiekursen Segmentering-API](./create-a-segment.md) eller skapat en segmentdefinition med [Segmentbyggare](../ui/overview.md), gör du det innan du fortsätter med den här självstudiekursen.

## Schemalagd utvärdering {#scheduled-evaluation}

Med hjälp av schemalagd utvärdering kan din IMS-organisation skapa ett återkommande schema som automatiskt kör exportjobb.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanslagningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem sammanfogningsprinciper för [!DNL XDM Individual Profile] i en enda sandlådemiljö kan du inte använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en begäran om POST till `/config/schedules`-slutpunkten kan du skapa ett schema och inkludera den tidpunkt då schemat ska utlösas.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för scheman](../api/schedules.md#create)

### Aktivera ett schema

Som standard är ett schema inaktivt när det skapas såvida inte egenskapen `state` är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en PATCH-begäran till `/config/schedules`-slutpunkten och inkludera ID:t för schemat i sökvägen.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för scheman](../api/schedules.md#update-state)

### Uppdatera schematiden

Tidsplaneringen kan uppdateras genom att en PATCH-begäran görs till `/config/schedules`-slutpunkten och med ID:t för schemat i sökvägen.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för scheman](../api/schedules.md#update-schedule)

## On-demand-utvärdering

Med On-demand-utvärdering kan ni skapa ett segmentjobb för att generera ett målgruppssegment när ni behöver det. Till skillnad från schemalagd utvärdering kommer detta endast att ske när det begärs och inte är återkommande.

### Skapa ett segmentjobb

Ett segmentjobb är en asynkron process som skapar ett nytt målgruppssegment. Det refererar till en segmentdefinition samt eventuella sammanfogningsprinciper som styr hur [!DNL Real-time Customer Profile] sammanfogar överlappande attribut i dina profilfragment. När ett segmentjobb har slutförts kan du samla in olika typer av information om segmentet, t.ex. eventuella fel som kan ha inträffat under bearbetningen och målgruppens slutliga storlek.

Du kan skapa ett nytt segmentjobb genom att göra en POST-förfrågan till `/segment/jobs`-slutpunkten i API:t [!DNL Real-time Customer Profile].

Mer detaljerad information om hur du använder den här slutpunkten finns i [segmentjobbslutpunktsguiden](../api/segment-jobs.md#create)


### Sök efter jobbstatus för segment

Du kan använda `id` för ett specifikt segmentjobb för att utföra en sökbegäran (GET) för att visa jobbets aktuella status.

Mer detaljerad information om hur du använder den här slutpunkten finns i [segmentjobbslutpunktsguiden](../api/segment-jobs.md#get)

## Tolka segmentresultat

När segmentjobben körs uppdateras mappningen `segmentMembership` för varje profil som ingår i segmentet. `segmentMembership` lagrar också alla förutvärderade målgruppssegment som är inkapslade i  [!DNL Platform]och som kan integreras med andra lösningar som  [!DNL Adobe Audience Manager].

I följande exempel visas hur attributet `segmentMembership` ser ut för varje enskild profilpost:

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

Om du vet vilken profil du vill använda kan du göra det med API:t [!DNL Real-time Customer Profile]. De fullständiga stegen för att komma åt enskilda profiler finns i [Åtkomst till kundprofildata i realtid med hjälp av självstudiekursen för profil-API](../../profile/api/entities.md).

## Exportera ett segment {#export}

När ett segmenteringsjobb har slutförts (värdet för attributet `status` är &quot;SUCCEEDED&quot;) kan du exportera målgruppen till en datauppsättning där den kan nås och hanteras.

Följande steg krävs för att exportera målgruppen:

- [Skapa en måldatauppsättning](#create-a-target-dataset)  - Skapa datauppsättningen för målgruppsmedlemmar.
- [Generera målgruppsprofiler i datauppsättningen](#generate-profiles-for-audience-members)  - Fyll i datauppsättningen med enskilda XDM-profiler baserat på resultatet av ett segmentjobb.
- [Övervaka exportförloppet](#monitor-export-progress)  - Kontrollera exportförloppet.
- [Läs målgruppsdata](#next-steps)  - Hämta de resulterande XDM-individuella profilerna som representerar medlemmarna i din publik.

### Skapa en måldatauppsättning

När du exporterar en målgrupp måste du först skapa en måldatauppsättning. Det är viktigt att datauppsättningen är korrekt konfigurerad för att exporten ska lyckas.

Ett av de viktigaste övervägandena är schemat som datauppsättningen baseras på (`schemaRef.id` i API-exempelbegäran nedan). För att kunna exportera ett segment måste datauppsättningen baseras på [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar in fält i scheman som delar samma klass, i det här fallet klassen XDM Individual Profile. Mer information om unionsvyscheman finns i avsnittet [Kundprofil i realtid i Utvecklarhandbok för schemaregister](../../xdm/api/getting-started.md).

Det finns två sätt att skapa den nödvändiga datauppsättningen:

- **Använda API:er:** De steg som följer i den här självstudiekursen visar hur du skapar en datauppsättning som refererar till  [!DNL XDM Individual Profile Union Schema] med  [!DNL Catalog] API:t.
- **Använda användargränssnittet:** Om du vill använda  [!DNL Adobe Experience Platform] användargränssnittet för att skapa en datauppsättning som refererar till unionsschemat följer du stegen i  [användargränssnittets ](../ui/overview.md) självstudiekurs och går sedan tillbaka till den här självstudiekursen för att fortsätta med stegen för att  [generera målgruppsprofiler](#generate-xdm-profiles-for-audience-members).

Om du redan har en kompatibel datauppsättning och känner till dess ID kan du fortsätta direkt till steget för [att generera målgruppsprofiler](#generate-xdm-profiles-for-audience-members).

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
        "persisted": true
    }
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Ett beskrivande namn för datauppsättningen. |
| `schemaRef.id` | ID för den unionsvy (schema) som datauppsättningen ska kopplas till. |
| `fileDescription.persisted` | Ett booleskt värde som när det anges som `true` gör att datauppsättningen kan finnas kvar i unionsvyn. |

**Svar**

Ett lyckat svar returnerar en array som innehåller det skrivskyddade, systemgenererade unika ID:t för den nya datauppsättningen. Ett korrekt konfigurerat datauppsättnings-ID krävs för att målgruppsmedlemmar ska kunna exporteras.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generera profiler för målgruppsmedlemmar {#generate-profiles}

När du har en unionskonstanterad datauppsättning kan du skapa ett exportjobb som behåller målgruppsmedlemmarna i datauppsättningen genom att göra en POST till `/export/jobs`-slutpunkten i [!DNL Real-time Customer Profile]-API:t och ange datauppsättnings-ID och segmentinformationen för de segment som du vill exportera.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktsguiden för exportjobb](../api/export-jobs.md#create)

### Övervaka exportförlopp

Som en exportjobbsprocess kan du övervaka dess status genom att göra en GET-förfrågan till `/export/jobs`-slutpunkten och inkludera `id` för exportjobbet i sökvägen. Exportjobbet slutförs när fältet `status` returnerar värdet &quot;SUCCEEDED&quot;.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktsguiden för exportjobb](../api/export-jobs.md#get)

## Nästa steg

När exporten är klar är dina data tillgängliga i [!DNL Data Lake] i [!DNL Experience Platform]. Du kan sedan använda [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) för att komma åt data med `batchId` som är associerad med exporten. Beroende på segmentets storlek kan data vara i segment och gruppen kan bestå av flera filer.

Följ självstudiekursen ](../../data-access/tutorials/dataset-data.md) om du vill ha stegvisa instruktioner om hur du använder API:t [!DNL Data Access] för att komma åt och hämta gruppfiler.[

Du kan också komma åt exporterade segmentdata med [!DNL Adobe Experience Platform Query Service]. Med API:t UI eller RESTful kan du med [!DNL Query Service] skriva, validera och köra frågor på data i [!DNL Data Lake].

Mer information om hur du frågar efter målgruppsdata finns i dokumentationen om [[!DNL Query Service]](../../query-service/home.md).
