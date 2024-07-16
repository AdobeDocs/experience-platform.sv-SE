---
solution: Experience Platform
title: Utvärdera och få åtkomst till segmentresultat
type: Tutorial
description: Följ den här självstudiekursen för att lära dig hur du utvärderar segmentdefinitioner och får tillgång till segmenteringsresultat med Adobe Experience Platform Segmentation Service API.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 0%

---

# Utvärdera och få tillgång till segmentdefinitionsresultat

Det här dokumentet innehåller en självstudiekurs för att utvärdera segmentdefinitioner och få tillgång till dessa resultat med [[!DNL Segmentation API]](../api/getting-started.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av de olika [!DNL Adobe Experience Platform]-tjänster som används för att skapa målgrupper. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Gör att du kan skapa målgrupper från [!DNL Real-Time Customer Profile]-data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata. För att du ska kunna använda segmentering bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Obligatoriska rubriker

Den här självstudien kräver också att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa [!DNL Platform] API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Begäranden till [!DNL Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla förfrågningar från POST, PUT och PATCH kräver ytterligare en rubrik:

- Content-Type: application/json

## Utvärdera en segmentdefinition {#evaluate-a-segment}

När du har utvecklat, testat och sparat din segmentdefinition kan du sedan utvärdera segmentdefinitionen genom en schemalagd utvärdering eller on-demand-utvärdering.

[Schemalagd utvärdering](#scheduled-evaluation) (kallas även schemalagd segmentering) gör att du kan skapa ett återkommande schema för att köra ett exportjobb vid en viss tidpunkt, medan [on demand-utvärdering](#on-demand-evaluation) innebär att du skapar ett segmentjobb för att skapa målgruppen direkt. Stegen för varje steg beskrivs nedan.

Om du ännu inte har slutfört [skapa en segmentdefinition med hjälp av självstudiekursen Segmentering-API](./create-a-segment.md) eller skapat en segmentdefinition med [Segmentbyggaren](../ui/segment-builder.md) gör du det innan du fortsätter med den här självstudiekursen.

## Schemalagd utvärdering {#scheduled-evaluation}

Med schemalagd utvärdering kan din organisation skapa ett återkommande schema för att automatiskt köra exportjobb.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanslagningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem sammanfogningsprinciper för [!DNL XDM Individual Profile] i en enda sandlådemiljö kommer du inte att kunna använda schemalagd utvärdering.

### Skapa ett schema

Genom att göra en schemaförfrågan till slutpunkten `/config/schedules` kan du skapa ett schema och inkludera den POST då schemat ska utlösas.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för scheman](../api/schedules.md#create)

### Aktivera ett schema

Som standard är ett schema inaktivt när det skapas, såvida inte egenskapen `state` är inställd på `active` i texten för skapandebegäran (POST). Du kan aktivera ett schema (ange `state` till `active`) genom att göra en PATCH-begäran till `/config/schedules`-slutpunkten och inkludera ID:t för schemat i sökvägen.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för scheman](../api/schedules.md#update-state)

### Uppdatera schematiden

Tidsplaneringen kan uppdateras genom att en PATCH-begäran görs till slutpunkten `/config/schedules` och med ID:t för schemat i sökvägen.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för scheman](../api/schedules.md#update-schedule)

## On-demand-utvärdering

Med On-demand-utvärdering kan ni skapa ett segmentjobb för att generera en målgrupp när ni behöver det. Till skillnad från schemalagd utvärdering kommer detta endast att ske när det begärs och inte är återkommande.

### Skapa ett segmentjobb

Ett segmentjobb är en asynkron process som skapar ett målgruppssegment på begäran. Den refererar till en segmentdefinition samt eventuella sammanfogningsprinciper som styr hur [!DNL Real-Time Customer Profile] sammanfogar överlappande attribut i dina profilfragment. När ett segmentjobb har slutförts kan du samla in olika information om segmentdefinitionen, t.ex. eventuella fel som kan ha inträffat under bearbetningen och målgruppens slutliga storlek. Ett segmentjobb måste köras varje gång du vill uppdatera målgruppen som är kvalificerad för segmentdefinitionen.

Du kan skapa ett nytt segmentjobb genom att göra en POST-förfrågan till `/segment/jobs`-slutpunkten i [!DNL Real-Time Customer Profile] API:t.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för segmentjobb](../api/segment-jobs.md#create)

### Sök efter jobbstatus för segment

Du kan använda `id` för ett specifikt segmentjobb för att utföra en sökbegäran (GET) för att visa jobbets aktuella status.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för segmentjobb](../api/segment-jobs.md#get)

## Tolka segmentjobbresultat

När segmentjobben har körts uppdateras kartan `segmentMembership` för varje profil som ingår i segmentdefinitionen. `segmentMembership` lagrar även alla förutvärderade målgrupper som är inkapslade i [!DNL Platform], vilket möjliggör integrering med andra lösningar som [!DNL Adobe Audience Manager].

I följande exempel visas hur attributet `segmentMembership` ser ut för varje enskild profilpost:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
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
| `lastQualificationTime` | Tidsstämpeln när kontrollen av segmentmedlemskap gjordes och profilen angavs eller avslutades i segmentdefinitionen. |
| `status` | Segmentdefinitionens deltagarstatus som en del av den aktuella begäran. Måste vara lika med ett av följande kända värden: <ul><li>`realized`: Entiteten kvalificerar sig för segmentdefinitionen.</li><li>`exited`: Entiteten avslutar segmentdefinitionen.</li></ul> |

>[!NOTE]
>
>Alla segmentmedlemskap som har statusen `exited` i mer än 30 dagar, baserat på `lastQualificationTime`, kan tas bort.

## Åtkomst till segmentjobbresultat

Resultatet av ett segmentjobb kan nås på ett av två sätt: du kan komma åt enskilda profiler eller exportera en hel publik till en datauppsättning.

I följande avsnitt beskrivs dessa alternativ mer ingående.

## Söka efter en profil

Om du vet vilken profil du vill använda kan du göra det med API:t [!DNL Real-Time Customer Profile]. De fullständiga stegen för att komma åt enskilda profiler finns i självstudiekursen [Åtkomst till kundprofildata i realtid med profils-API](../../profile/api/entities.md).

## Exportera ett segment {#export}

När ett segmenteringsjobb har slutförts (värdet för attributet `status` är &quot;SUCCEEDED&quot;) kan du exportera målgruppen till en datauppsättning där den kan nås och hanteras.

Följande steg krävs för att exportera målgruppen:

- [Skapa en måldatauppsättning](#create-a-target-dataset) - Skapa datauppsättningen för målgruppsmedlemmar.
- [Generera målgruppsprofiler i datauppsättningen](#generate-profiles) - Fyll i datauppsättningen med enskilda XDM-profiler baserat på resultatet av ett segmentjobb.
- [Övervaka exportförloppet](#monitor-export-progress) - Kontrollera exportförloppet.
- [Läs målgruppsdata](#next-steps) - Hämta de resulterande enskilda XDM-profilerna som representerar medlemmarna i din målgrupp.

### Skapa en måldatauppsättning {#create-dataset}

När du exporterar en målgrupp måste du först skapa en måldatauppsättning. Det är viktigt att datauppsättningen är korrekt konfigurerad för att exporten ska lyckas.

Ett av de viktigaste övervägandena är schemat som datauppsättningen baseras på (`schemaRef.id` i API-exempelbegäran nedan). Om du vill exportera en segmentdefinition måste datauppsättningen baseras på [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar in fält i scheman som delar samma klass, i det här fallet klassen XDM Individual Profile. Mer information om unionsvyscheman finns i avsnittet [Kundprofil i realtid i utvecklarhandboken för schemaregister](../../xdm/api/getting-started.md).

Det finns två sätt att skapa den nödvändiga datauppsättningen:

- **Använda API:er:** I den här självstudiekursen beskrivs hur du skapar en datauppsättning som refererar till [!DNL XDM Individual Profile Union Schema] med API:t [!DNL Catalog].
- **Använd användargränssnittet:** Om du vill använda användargränssnittet [!DNL Adobe Experience Platform] för att skapa en datauppsättning som refererar till unionsschemat följer du stegen i [användargränssnittet](../ui/overview.md) och går sedan tillbaka till den här självstudiekursen för att fortsätta med stegen för att [generera målgruppsprofiler](#generate-profiles).

Om du redan har en kompatibel datauppsättning och känner till dess ID kan du fortsätta direkt till steget för att [generera målgruppsprofiler](#generate-profiles).

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
| `schemaRef.id` | ID:t för den unionsvy (schema) som datauppsättningen ska kopplas till. |

**Svar**

Ett lyckat svar returnerar en array som innehåller det skrivskyddade, systemgenererade unika ID:t för den nya datauppsättningen. Ett korrekt konfigurerat datauppsättnings-ID krävs för att målgruppsmedlemmar ska kunna exporteras.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generera profiler för målgruppsmedlemmar {#generate-profiles}

När du har en unionskonstanterad datauppsättning kan du skapa ett exportjobb som behåller målgruppsmedlemmarna i datauppsättningen genom att göra en POST till `/export/jobs`-slutpunkten i [!DNL Real-Time Customer Profile] API:t och ange datauppsättnings-ID:t och segmentdefinitionsinformationen för de segmentdefinitioner som du vill exportera.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för exportjobb](../api/export-jobs.md#create)

### Övervaka exportförlopp

Som en exportjobbsprocess kan du övervaka dess status genom att göra en GET-förfrågan till slutpunkten `/export/jobs` och inkludera `id` för exportjobbet i sökvägen. Exportjobbet slutförs när fältet `status` returnerar värdet &quot;SUCCEEDED&quot;.

Mer detaljerad information om hur du använder den här slutpunkten finns i [slutpunktshandboken för exportjobb](../api/export-jobs.md#get)

## Nästa steg

När exporten har slutförts är dina data tillgängliga i [!DNL Data Lake] i [!DNL Experience Platform]. Du kan sedan använda [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) för att komma åt data med hjälp av `batchId` som är associerad med exporten. Beroende på segmentdefinitionens storlek kan data vara i segment och gruppen kan bestå av flera filer.

Följ [Dataåtkomstsjälvstudiekursen](../../data-access/tutorials/dataset-data.md) om du vill ha stegvisa anvisningar om hur du använder [!DNL Data Access]-API:t för att få åtkomst till och hämta gruppfiler.

Du kan också komma åt exporterade segmentdefinitionsdata med [!DNL Adobe Experience Platform Query Service]. Med API:t UI eller RESTful kan du med [!DNL Query Service] skriva, validera och köra frågor på data i [!DNL Data Lake].

Mer information om hur du frågar efter målgruppsdata finns i dokumentationen om [[!DNL Query Service]](../../query-service/home.md).
