---
keywords: Experience Platform;aktivering;felsökning;skyddsförslag;riktlinjer;gräns
title: Standardskyddsutkast för aktiveringsdata
solution: Experience Platform
product: experience platform
type: Documentation
description: Läs mer om standardanvändning och hastighetsbegränsningar för dataaktivering.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 0835021523a7eb1642a6dbcb24334eac535aaa6d
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 1%

---

# Garantier för aktiveringsdata

Den här sidan innehåller standardvärden för användning och hastighetsbegränsningar för aktiveringsbeteende. När du granskar följande skyddsutkast antas du ha rätt [anslutna till destinationer](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* De flesta kunder överskrider inte dessa standardgränser. Om du vill veta mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.
>* De gränser som beskrivs i det här dokumentet förbättras ständigt. Kontrollera regelbundet om det finns uppdateringar.
>* Beroende på vilka begränsningar som gäller i det enskilda senare ledet kan vissa destinationer ha tätare skyddsprofiler än de som finns på den här sidan. Se även till att kontrollera [katalog](/help/destinations/catalog/overview.md) målsidan som du ansluter och aktiverar data till.

## Begränsningstyper {#limit-types}

Det finns två typer av standardgränser i det här dokumentet:

* **Mjuk gräns:** Det går att gå längre än en mjuk gräns, men mjuka gränser ger en rekommenderad vägledning för systemprestanda.
* **Hård gräns:** En hård gräns ger ett absolut maximum. Gränssnittet eller API:t i Experience Platform tillåter inte att du överskrider den här gränsen, eller så returneras ett fel om du överskrider den här gränsen.


## Aktiveringsbegränsningar {#activation-limits}

Följande skyddsprofiler ger rekommenderade gränser när kundprofildata aktiveras i realtid till destinationer.

### Allmänna aktiveringsskydd {#general-activation-guardrails}

Skyddskassorna nedan gäller vanligtvis aktivering via [alla måltyper](/help/destinations/destination-types.md#destination-types).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal målgrupper till ett enda mål | 250 | Mjuk | Rekommendationen är att mappa högst 250 målgrupper till ett enda mål i ett dataflöde. <br><br> Om du behöver aktivera fler än 250 målgrupper till ett mål kan du antingen: <ul><li> Dela upp målgrupper som du inte längre vill aktivera, eller</li><li>Skapa ett nytt dataflöde till önskat mål och mappa målgrupper till det nya dataflödet.</li></ul> <br> Observera att för vissa destinationer kan du vara begränsad till färre än 250 målgrupper mappade till destinationen. Dessa destinationer beskrivs längre ned på sidan i respektive avsnitt. |
| Maximalt antal attribut som har mappats till ett mål | 50 | Mjuk | Om det finns flera mål- och måltyper kan du välja profilattribut och identiteter att mappa för export. För optimala prestanda bör maximalt 50 attribut mappas i ett dataflöde till ett mål. |
| Högsta antal destinationer | 100 | Hård | Du kan skapa högst 100 destinationer som du kan ansluta och aktivera data till, *per sandlåda*. [Destinationer för kantanpassning (anpassad personalisering)](#edge-destinations-activation) kan utgöra högst 10 av de 100 rekommenderade destinationerna. |
| Typ av data som aktiveras för destinationer | Profildata, inklusive identiteter och identitetskarta | Hård | För närvarande går det bara att exportera *profilpostattribut* till destinationer. XDM-attribut som beskriver händelsedata stöds för närvarande inte för export. |
| Typ av data som aktiveras för mål - stöd för matris- och mappattribut | Inte tillgängligt | Hård | För närvarande är det **not** kan exporteras *matris- eller mappattribut* till destinationer. Undantaget till den här regeln är [identitetskarta](/help/xdm/field-groups/profile/identitymap.md), som exporteras både i direktuppspelande och filbaserade aktiveringar. |

{style="table-layout:auto"}

### Aktivering av strömning {#streaming-activation}

Skyddskassorna nedan gäller aktivering via [mål för direktuppspelning](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Antal aktiveringar (HTTP-meddelanden med profilexporter) per sekund | Ej tillämpligt | – | Det finns för närvarande ingen gräns för hur många meddelanden per sekund som skickas från Experience Platform till partnermålens API-slutpunkter. <br> Eventuella begränsningar eller latenser bestäms av slutpunkten där Experience Platform skickar data. Se även till att kontrollera [katalog](/help/destinations/catalog/overview.md) målsidan som du ansluter och aktiverar data till. |

{style="table-layout:auto"}

### Batchaktivering (filbaserad) {#batch-file-based-activation}

Skyddskassorna nedan gäller aktivering via [batchvis (filbaserat) mål](/help/destinations/ui/activate-batch-profile-destinations.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Aktiveringsfrekvens | En daglig hel export eller mer frekvent stegvis export var 3, 6, 8 eller 12: e timme. | Hård | Läs [exportera fullständiga filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) och [exportera inkrementella filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) dokumentationsavsnitt för mer information om frekvensökningar för batchexport. |
| Maximalt antal målgrupper som kan exporteras vid en given timme | 100 | Mjuk | Rekommendationen är att lägga till högst 100 målgrupper i batchmåldataflöden. |
| Maximalt antal rader (poster) per fil som ska aktiveras | 5 miljoner | Hård | Adobe Experience Platform delar automatiskt upp de exporterade filerna i 5 miljoner poster (rader) per fil. Varje rad representerar en profil. Delade filnamn läggs till med en siffra som anger att filen är en del av en större export: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Mer information finns i [schemaläggningsavsnitt](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) av självstudiekursen om aktivering av batchdestinationer. |

{style="table-layout:auto"}

### Ad hoc-aktivering {#ad-hoc-activation}

Skyddsritningarna nedan gäller för [ad hoc-aktivering](/help/destinations/api/ad-hoc-activation-api.md) -metod.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Målgrupper aktiverade per ad hoc-aktiveringsjobb | 80 | Hård | För närvarande kan varje ad hoc-aktiveringsjobb aktivera upp till 80 målgrupper. Om du försöker aktivera fler än 80 målgrupper per jobb misslyckas jobbet. Detta beteende kan komma att ändras i framtida versioner. |
| Samtidiga ad hoc-aktiveringsjobb per målgrupp | 1 | Hård | Kör inte mer än ett samtidiga ad hoc-aktiveringsjobb per målgrupp. |

{style="table-layout:auto"}

### Aktivering av mål för kantanpassning {#edge-destinations-activation}

Skyddskassorna nedan gäller aktivering via [mål för kantanpassning](/help/destinations/destination-types.md#streaming-profile-export).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal [Anpassad personalisering](/help/destinations/catalog/personalization/custom-personalization.md) mål | 10 | Mjuk | Du kan konfigurera dataflöden till 10 anpassade mål för personalisering per sandlåda. |
| Maximalt antal attribut som mappats till ett personaliseringsmål per sandlåda | 30 | Hård | Högst 30 attribut kan mappas i ett dataflöde till ett personaliseringsmål per sandlåda. |
| Maximalt antal målgrupper mappade till en enda [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) mål | 50 | Mjuk | Du kan aktivera maximalt 50 målgrupper i ett aktiveringsflöde till ett enda Adobe Target-mål. |

{style="table-layout:auto"}

### [!BADGE Beta]{type=Informative} Datauppsättningsexport {#dataset-exports}

Datauppsättningsexporter stöds för närvarande i en **[!UICONTROL First Full and then Incremental]** [mönster](/help/destinations/ui/export-datasets.md#scheduling). Skyddskisserna som beskrivs i det här avsnittet gäller för den första fullständiga exporten som sker efter att ett arbetsflöde för datauppsättningsexport har ställts in.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Storlek på exporterade datamängder | 5 miljarder poster | Mjuk | Gränsen som beskrivs här för datauppsättningsexport är en *mjukt skyddsräcke*. Även om användargränssnittet inte hindrar dig från att exportera datauppsättningar som är större än 5 miljarder poster, är beteendet oförutsägbart och exporten kan antingen misslyckas eller ha mycket lång exportfördröjning. |

{style="table-layout:auto"}

<!--

### Dataset Types {#dataset-types}

Datasets exported from Experience Platform can be of two types, as described below:

**Timeseries**
Timeseries datasets are also known as *XDM Experience Events* datasets in Experience Platform terminology.
The dataset schema includes a top level *timestamp* column. Data is ingested in an append-only fashion.

**Record** 
Record datasets are also known as *XDM Individual Profile* datasets in Experience Platform terminology.
The dataset schema does not include a top level *timestamp* column. Data is ingested in upsert fashion.

The guardrails below are grouped by the format of the exported file, and then further by dataset type.

**Parquet output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| Record | N/A | Five billion records per file | Only the data from the last seven days is exported. |

{style="table-layout:auto"}

**JSON output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| <p>Record</p> | <p><ul><li>Yes</li><li>No</li></ul></p> | <p><ul><li>Five billion records per compressed file</li><li>One million records per uncompressed file</li></ul></p> | <p>The record count of the dataset must be less than five billion for compressed files and one million for uncompressed files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</p> |

{style="table-layout:auto"}

-->

<!--

<table>
<thead>
  <tr>
    <th>Output format</th>
    <th>Dataset type</th>
    <th>Compression</th>
    <th>Guardrail</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Parquet</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td>Record</td>
    <td>-</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td rowspan="3">JSON</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td rowspan="2">Record</td>
    <td>Yes</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td>No</td>
    <td>One million records per file</td>
    <td>The record count of the dataset must be less than one million, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
</tbody>
</table>

-->

### Destinationens SDK skyddsräcken {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster för Experience Platform så att målgrupps- och profildata kan skickas till slutpunkten, baserat på valfritt data- och autentiseringsformat. Skyddsritningarna nedan gäller de mål som du konfigurerar med Destination SDK.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal [privata anpassade destinationer](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Mjuk | Du kan skapa högst 5 privata anpassade direktuppspelnings- eller gruppmål med hjälp av Destination SDK. Kontakta en kundtjänstrepresentant om du behöver skapa fler än fem sådana destinationer. |
| Profilexportpolicy för Destination SDK | <ul><li>`maxBatchAgeInSecs` (minst 1 800 och högst 3 600)</li><li>`maxNumEventsInBatch` (minst 1 000, högst 10 000)</li></ul> | Hård | När du använder [konfigurerbar aggregering](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) för ditt mål bör du tänka på de lägsta och högsta värden som avgör hur ofta HTTP-meddelanden skickas till ditt API-baserade mål och hur många profiler meddelandena ska innehålla. |

{style="table-layout:auto"}

### Princip för målbegränsning och återförsök {#destination-throttling-and-retry-policy}

Uppgifter om begränsningströsklar eller begränsningar för angivna destinationer. I det här avsnittet finns även information om återförsökspolicyn för destinationer.

| Typ av mål | Beskrivning |
| --- | --- |
| Företagsmål (HTTP API, Amazon Kinesis, Azure EventHubs) | På 95 % av tiden försöker Experience Platform att erbjuda en genomströmningslatens på mindre än 10 minuter för meddelanden som skickats utan fel med en hastighet på mindre än 10 000 förfrågningar per sekund för varje dataflöde till en företagsdestination. <br> Om det uppstår fel på begäranden till ditt företags mål, lagrar Experience Platform de misslyckade förfrågningarna och försöker skicka dem till din slutpunkt två gånger. |

{style="table-layout:auto"}

## Gardrutor för andra Experience Platform-tjänster {#guardrails-other-services}

Visa skyddsinformation för andra Experience Platform-tjänster:

* Guardrails för [dataintag](/help/ingestion/guardrails.md)
* Guardrails för [[!DNL Identity Service] data](/help/identity-service/guardrails.md)
* Guardrails för [[!DNL Real-Time Customer Profile] data](/help/profile/guardrails.md)
* Guardrails för [[!DNL Query Service] data](/help/query-service/guardrails.md)
