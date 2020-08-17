---
keywords: Experience Platform;home;popular topics;ingested data
solution: Experience Platform
title: Felsökningsguide för Adobe Experience Platform batchmatning
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---


# Felsökningsguide för batchimport

Den här dokumentationen hjälper dig att besvara vanliga frågor om Adobe Experience Platform API: [!DNL Batch Data Ingestion] er.

## Batch-API-anrop

### Är batchar omedelbart aktiva efter att HTTP 200 OK har tagits emot från CompleteBatch-API:t?

Svaret från API:t innebär att batchen har godkänts för bearbetning - den är inte aktiv förrän den övergår till det slutliga tillståndet, till exempel Aktiv eller Fel. `200 OK`

### Är det säkert att försöka köra API-anropet CompleteBatch igen när det inte fungerar?

Ja - det är säkert att försöka köra API-anropet igen. Trots felet är det möjligt att åtgärden lyckades och att batchen accepterades. Klienter förväntas dock ha återförsöksfunktioner om API-fel uppstår, och de uppmuntras att försöka igen. Om åtgärden lyckades returneras API:t, även efter nya försök.

### När ska API:t för stor filöverföring användas?

Den rekommenderade filstorleken för API:t för stor filöverföring är 256 MB eller större. Mer information om hur du använder API:t för stor filöverföring finns [här](./api-overview.md#ingest-large-parquet-files).

### Varför misslyckas anropet till API:t för slutförd stor fil?

Om segment av en stor fil hittas som överlappar eller saknas svarar servern med en felaktig HTTP 400-begäran. Detta kan inträffa eftersom det är möjligt att överföra överlappande segment, eftersom intervallvalideringar görs när filen slutförs, när filen sammanfogas.

## Inmatningssupport

### Vilka importformat stöds?

För närvarande stöds både Parquet och JSON. CSV stöds i äldre versioner - data kommer att befordras till överordnad och preliminära kontroller, men inga moderna funktioner som konvertering, partitionering eller radvalidering kommer att stödjas.

### Var ska batchindataformatet anges?

Indataformatet ska anges när gruppen skapas i nyttolasten. Ett exempel på hur du anger batchindataformatet finns nedan:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Hur importeras flerradig JSON?

Om du vill importera flerradig JSON måste `isMultiLineJson` flaggan anges när gruppen skapas. Ett exempel på detta visas nedan:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Vad är skillnaden mellan JSON-rader (enradig JSON) och flerradig JSON?

För JSON-rader finns det ett JSON-objekt per rad. Exempel:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

För JSON med flera rader kan ett objekt uppta flera rader, medan alla objekt kapslas in i en JSON-array. Exempel:

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

Som standard [!DNL Batch Data Ingestion] används enkelradig JSON.

### Stöds CSV-förtäring?

CSV-inmatning stöds bara för platta scheman. Inmatning av hierarkiska data i CSV stöds för närvarande inte.

För att få alla dataöverföringsfunktioner måste formaten JSON och Parquet användas.

### Vilka typer av validering utförs på data?

Det finns tre valideringsnivåer för data:

- Schema - Batchmatning säkerställer att schemat för de inmatade data matchar datasetens schema.
- Datatyp - gruppinmatning säkerställer att typen för varje inmatat fält matchar typen som definieras i datasetens schema.
- Begränsningar - Gruppinmatning säkerställer att begränsningar som&quot;Obligatorisk&quot;,&quot;Uppräkning&quot; och&quot;format&quot; definieras korrekt i schemadefinitionen.

### Hur kan en redan skickad batch ersättas?

En inkapslad batch kan ersättas med funktionen Uppspelning i grupp. Mer information om Batch Replay finns [här](./api-overview.md#replay-a-batch).

### Hur övervakas batchintaget?

När en batch har signalerats för batchbefordran kan batchbearbetningsförloppet övervakas med följande begäran:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Med den här förfrågan får du ett svar som liknar detta:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## Batchlägen

### Vilka är de möjliga batchtillstånden?

En batch kan i sin livscykel gå igenom följande lägen:

| Status | Data skrivna till Överordnad | Beskrivning |
| ------ | ---------------------- | ----------- |
| Övergiven |  | Klienten kunde inte slutföra batchen inom den förväntade tidsramen. |
| Avbruten |  | Klienten har via API: [!DNL Batch Data Ingestion] erna explicit anropat en avbrottsåtgärd för den angivna batchen. När en batch är i inläst tillstånd kan gruppen inte avbrytas. |
| Aktiv/Slutförd | x | Batchen har befordrats från fas till överordnad och är nu tillgänglig för nedladdning. **Obs!** Aktiv och Slutfört används omväxlande. |
| Arkiverad |  | Batchen har arkiverats i kylförvaring. |
| Misslyckades/misslyckades |  | Ett terminaltillstånd som antingen beror på felaktig konfiguration och/eller felaktiga data. Ett åtgärdbart fel registreras, tillsammans med gruppen, så att klienter kan korrigera och skicka data igen. **Obs!** Misslyckades och Misslyckades används omväxlande. |
| Inaktiv | x | Batchen befordrades, men har antingen återställts eller gått ut. Batchen kommer inte längre att vara tillgänglig för nedströmsförbrukning, men underliggande data kommer att vara Överordnad tills de har sparats, arkiverats eller på annat sätt tagits bort. |
| Läser in |  | Klienten skriver för närvarande data för gruppen. Batchen är för närvarande **inte** redo för befordran. |
| Inläst |  | Klienten har slutfört skrivningen av data för batchen. Batchen är klar för befordran. |
| Bevarad |  | Data har tagits bort från Överordnad och i ett särskilt arkiv i Adobe Data Lake. |
| Mellanlagring |  | Klienten har signalerat batchen för befordran och data mellanlagras för förbrukning nedströms. |
| Försöker igen |  | Klienten har signalerat batchen för befordran, men på grund av ett fel görs ett nytt försök att bearbeta batchen av en tjänst för batchövervakning. Det här läget kan användas för att tala om för kunderna att det kan dröja med inhämtningen av data. |
| Stängd |  | Klienten har signalerat batchen för befordran, men efter `n` återförsök av en batchövervakningstjänst har batchkampanjen avstannat. |

### Vad betyder &quot;Förproduktion&quot; för batchar?

När en batch är i&quot;Förproduktion&quot; innebär det att batchen har signalerats för befordran och att data mellanlagras för förbrukning nedströms.

### Vad innebär det när en batch är&quot;Försöker igen&quot;?

När en batch är i &quot;Försöker igen&quot; betyder det att batchens dataintag tillfälligt har stoppats på grund av tillfälliga problem. När detta händer behöver kunden inte göra något.

### Vad innebär det när en batch är&quot;förlamad&quot;?

När en sats är i &quot;Staplad&quot; innebär det att det [!DNL Data Ingestion Services] är svårt att få in satsen och alla återförsök har tömts.

### Vad innebär det om en batch fortfarande är&quot;Läser in&quot;?

När en batch är i&quot;Loading&quot; betyder det att API:t CompleteBatch inte har anropats för att befordra gruppen.

### Finns det något sätt att veta om en batch har importerats utan problem?

När batchstatusen är Aktiv har batchen importerats. Följ stegen som beskrivs [tidigare](#how-is-batch-ingestion-monitored)för att ta reda på status för gruppen.

### Vad händer efter att en batch har misslyckats?

När en batch misslyckas kan orsaken till att den inte fungerar identifieras i avsnittet `errors` i nyttolasten. Exempel på fel finns nedan:

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

När felen har korrigerats kan batchen överföras igen.

## Gruppsupport

### Hur ska grupper tas bort?

I stället för att ta bort direkt från [!DNL Catalog]bör batchar tas bort med någon av metoderna nedan:

1. Om batchen pågår bör batchen avbrytas.
2. Om batchen kan mastras bör batchen återställas.

### Vilka batchnivåmätvärden finns tillgängliga?

Följande batchnivåmått är tillgängliga för batchar i tillståndet Aktiv/Slutfört:

| Mått | Beskrivning |
| ------ | ----------- |
| inputByteSize | Det totala antalet byte som mellanlagrats för [!DNL Data Ingestion Services] bearbetningen. |
| inputRecordSize | Det totala antalet rader som mellanlagrats för [!DNL Data Ingestion Services] bearbetning. |
| outputByteSize | Det totala antalet byte som matats ut av [!DNL Data Ingestion Services] till [!DNL Data Lake]. |
| outputRecordSize | Det totala antalet rader som matats ut med [!DNL Data Ingestion Services] till [!DNL Data Lake]. |
| partitionCount | Det totala antalet partitioner som skrivits till [!DNL Data Lake]. |

### Varför är mätvärden inte tillgängliga för vissa batchar?

Det finns två anledningar till att mätvärden kanske inte är tillgängliga i din batch:

1. Batchen kunde aldrig konvertera den till tillståndet Aktiv/Slutfört.
2. Batchen befordrades med en äldre befordringssökväg, till exempel CSV-inmatning.

### Vad betyder de olika statuskoderna?

| Statuskod | Beskrivning |
| ----------- | ----------- |
| 106 | Datauppsättningsfilen är tom. |
| 118 | CSV-filen innehåller en tom rubrikrad. |
| 200 | Batchen har godkänts för bearbetning och kommer att övergå till ett slutligt tillstånd, till exempel Aktiv eller Misslyckad. När batchen har skickats kan den övervakas med hjälp av `GetBatch` slutpunkten. |
| 400 | Felaktig begäran. Returneras om det finns några segment som saknas eller överlappar varandra i en grupp. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
