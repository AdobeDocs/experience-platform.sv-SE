---
keywords: Experience Platform;mål-API;ad hoc-aktivering;aktivera segment ad hoc
solution: Experience Platform
title: (Beta) Aktivera målgruppssegment till batchmål via ad hoc-aktiverings-API
description: I den här artikeln beskrivs hela arbetsflödet för aktivering av målgruppssegment via ad hoc-aktiverings-API:t, inklusive segmenteringsjobben som utförs före aktiveringen.
topic-legacy: tutorial
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# (Beta) Aktivera målgruppssegment till batchmål via ad hoc-aktiverings-API

>[!IMPORTANT]
>
>The [!DNL ad-hoc activation API] in Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

Med API:t för ad hoc-aktivering kan marknadsförare programmässigt aktivera målgruppssegment till destinationer på ett snabbt och effektivt sätt i situationer där omedelbar aktivering krävs.

Bilden nedan visar det kompletta arbetsflödet för aktivering av segment via API:t för ad hoc-aktivering, inklusive segmenteringsjobben som äger rum i Platform var 24:e timme.

![ad hoc-aktivering](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Ad hoc-målgruppsaktivering stöds endast av [gruppfilsbaserade mål](../destination-types.md#file-based).

## Användningsfall {#use-cases}

### Försäljning eller kampanjer i Flash

En webbutik förbereder en begränsad försäljning och vill meddela kunderna med kort varsel. Via Experience Platform ad hoc-aktiverings-API kan marknadsföringsteamet exportera segment on-demand och snabbt skicka e-postreklam till kundbasen.


### Aktuella event eller senaste nytt

Ett hotell förväntar sig ett infallsväder de kommande dagarna och teamet vill snabbt informera de ankommande gästerna så att de kan planera därefter. Marknadsföringsteamet kan använda Experience Platform ad hoc-aktiverings-API för att exportera segment on-demand och meddela gästerna.

### Integrationstestning

IT-chefer kan använda Experience Platform ad hoc-aktiverings-API för att exportera segment on-demand, så att de kan testa sin anpassade integrering med Adobe Experience Platform och se till att allt fungerar som det ska.


## Guardrails {#guardrails}

Tänk på följande skyddsutkast när du använder API:t för ad hoc-aktivering.

* För närvarande kan varje ad hoc-aktiveringsjobb aktivera upp till 20 segment. Om du försöker aktivera fler än 20 segment per jobb misslyckas jobbet. Detta beteende kan komma att ändras i framtida versioner.
* Ad hoc-aktiveringsjobb kan inte köras parallellt med schemalagda [segmentexportjobb](../../segmentation/api/export-jobs.md). Innan du kör ett ad hoc-aktiveringsjobb kontrollerar du att det schemalagda segmentexportjobbet har slutförts. Se [övervakning av måldataflöde](../../dataflows/ui/monitor-destinations.md) för information om hur man övervakar status för aktiveringsflöden. Om t.ex. aktiveringsdataflödet visar en **[!UICONTROL Processing]** status, vänta tills den är klar innan du kör ad hoc-aktiveringsjobbet.
* Kör inte mer än ett samtidiga ad hoc-aktiveringsjobb per segment.

## Segmentering {#segmentation-considerations}

Adobe Experience Platform kör schemalagda segmenteringsjobb en gång var 24:e timme. API:t för ad hoc-aktivering körs baserat på de senaste segmenteringsresultaten.

## Steg 1: Förutsättningar {#prerequisites}

Innan du kan ringa anrop till Adobe Experience Platform API:er måste du kontrollera att du uppfyller följande krav:

* Du har ett IMS-organisationskonto med tillgång till Adobe Experience Platform.
* Ditt Experience Platform-konto har `developer` och `user` roller har aktiverats för Adobe Experience Platform API-produktprofilen. Kontakta [Admin Console](../../access-control/home.md) administratör för att aktivera de här rollerna för ditt konto.
* Du har en Adobe ID. Om du inte har någon Adobe ID går du till [Adobe Developer Console](https://developer.adobe.com/console) och skapa ett nytt konto.

## Steg 2: Samla in inloggningsuppgifter {#credentials}

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Resurser i Experience Platform kan isoleras till specifika virtuella sandlådor. I förfrågningar till plattforms-API:er kan du ange namnet och ID:t för sandlådan som åtgärden ska utföras i. Dessa är valfria parametrar.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Experience Platform finns i [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* Innehållstyp: `application/json`

## Steg 3: Skapa aktiveringsflöde i plattformsgränssnittet {#activation-flow}

Innan du kan aktivera segment via API:t för ad hoc-aktivering måste du först ha ett aktiveringsflöde konfigurerat i plattformsgränssnittet för det valda målet.

Detta innefattar att starta aktiveringsarbetsflödet, välja segment, konfigurera ett schema och aktivera dem.

I följande självstudiekurs finns detaljerade anvisningar om hur du konfigurerar ett aktiveringsflöde för dina gruppmål: [Aktivera målgruppsdata för att batchprofilera exportmål](../ui/activate-batch-profile-destinations.md).

## Steg 4: Hämta det senaste segmentexportjobb-ID:t {#segment-export-id}

När du har konfigurerat ett aktiveringsflöde för batchdestinationen börjar schemalagda segmenteringsjobb automatiskt att köras var 24:e timme.

Innan du kan köra ad hoc-aktiveringsjobbet måste du hämta ID:t för det senaste segmentexportjobbet. Du måste skicka detta ID i ad hoc-aktiveringsjobbbegäran.

Följ instruktionerna som beskrivs [här](../../segmentation/api/export-jobs.md#retrieve-list) om du vill hämta en lista över alla segmentexportjobb.

I svaret söker du efter den första posten som innehåller schemaegenskapen nedan.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

Segmentets exportjobb-ID finns i `id` -egenskap, enligt nedan.

![ID för segmentexportjobb](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Steg 5: Kör ad hoc-aktiveringsjobbet {#activation-job}

Adobe Experience Platform kör schemalagda segmenteringsjobb en gång var 24:e timme. API:t för ad hoc-aktivering körs baserat på de senaste segmenteringsresultaten.

Innan du kör ett ad hoc-aktiveringsjobb kontrollerar du att det schemalagda segmentexportjobbet för dina segment har slutförts. Se [övervakning av måldataflöde](../../dataflows/ui/monitor-destinations.md) för information om hur man övervakar status för aktiveringsflöden. Om t.ex. aktiveringsdataflödet visar en **[!UICONTROL Processing]** status, vänta tills den är klar innan du kör ad hoc-aktiveringsjobbet.

När segmentexportjobbet är klart kan du aktivera det.

>[!NOTE]
>
>För närvarande kan varje ad hoc-aktiveringsjobb aktivera upp till 20 segment. Om du försöker aktivera fler än 20 segment per jobb misslyckas jobbet. Detta beteende kan komma att ändras i framtida versioner.

### Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | ID:n för de målinstanser som du vill aktivera segment för. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | ID:n för de segment som du vill aktivera till det valda målet. |
| <ul><li>`exportId1`</li></ul> | Det ID som returnerades i svaret från [segmentexport](../../segmentation/api/export-jobs.md#retrieve-list) jobb. Se [Steg 4: Hämta det senaste segmentexportjobb-ID:t](#segment-export-id) för instruktioner om hur du hittar detta ID. |

### Svar

Ett lyckat svar returnerar HTTP-status 200.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segment` | ID för det aktiverade segmentet. |
| `order` | ID:t för det mål som segmentet aktiverades till. |
| `statusURL` | Status-URL för aktiveringsflödet. Du kan följa flödets förlopp med [API för flödestjänst](../../sources/tutorials/api/monitor.md). |


## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.
