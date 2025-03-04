---
keywords: Experience Platform;aktivering;felsökning;skyddsförslag;riktlinjer;limit
title: Standardskyddsutkast för dataaktivering
solution: Experience Platform
product: experience platform
type: Documentation
description: Läs mer om standardanvändning och hastighetsbegränsningar för dataaktivering.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 2d640b282feb783694276c69366b1fccadddfd78
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 1%

---

# Garantier för dataaktivering

>[!IMPORTANT]
>
>Kontrollera dina licensrättigheter i din försäljningsorder och motsvarande [produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions.html) om faktiska användningsbegränsningar, utöver den här sidan med skyddsförslag.

Den här sidan innehåller standardvärden för användning och hastighetsbegränsningar för aktiveringsbeteende. När du granskar följande skyddsutkast antas att du har [anslutit till mål](/help/destinations/ui/connect-destination.md) korrekt.

>[!NOTE]
>
>* De flesta kunder överskrider inte dessa standardgränser. Om du vill veta mer om anpassade begränsningar kontaktar du kundtjänstrepresentanten.
>* De gränser som beskrivs i det här dokumentet förbättras ständigt. Kontrollera regelbundet om det finns uppdateringar.
>* Beroende på vilka begränsningar som gäller i det enskilda senare ledet kan vissa destinationer ha tätare skyddsprofiler än de som finns på den här sidan. Kontrollera även sidan [katalog](/help/destinations/catalog/overview.md) för målet som du ansluter och aktiverar data till.

## Skyddstyper {#limit-types}

Det finns två typer av standardgränser i det här dokumentet:

| Typ av skyddsräcke | Beskrivning |
|----------|---------|
| **Prestandaskydd (mjuk gräns)** | Prestandaskydd är användarbegränsningar som relaterar till omfattningen av dina användningsfall. När du överskrider prestandaskyddet kan du uppleva prestandaförsämringar och fördröjning. Adobe ansvarar inte för sådana prestandaförsämringar. Kunder som genomgående överskrider ett prestandaresäkerhetsskydd kan välja att licensiera ytterligare kapacitet för att undvika prestandaförsämringar. |
| **Systemstyrda skyddsräcken (hård begränsning)** | Systemstyrda skyddsräcken används av Real-Time CDP gränssnitt eller API. Det här är begränsningar som du inte kan överskrida eftersom gränssnittet och API kommer att blockera dig från att göra det eller returnera ett fel. |

{style="table-layout:auto"}


## Aktiveringsbegränsningar {#activation-limits}

Följande skyddsprofiler ger rekommenderade gränser när kundprofildata aktiveras i realtid till destinationer.

### Allmänna aktiveringsskydd {#general-activation-guardrails}

Skyddsritningarna nedan gäller vanligtvis för aktivering via [alla måltyper](/help/destinations/destination-types.md#destination-types).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal målgrupper till ett enda mål | 250 | Prestandaskydd | Rekommendationen är att mappa högst 250 målgrupper till ett enda mål i ett dataflöde. <br><br> Om du behöver aktivera fler än 250 målgrupper till ett mål kan du antingen: <ul><li> Dela upp målgrupper som du inte längre vill aktivera, eller</li><li>Skapa ett nytt dataflöde till önskat mål och mappa målgrupper till det nya dataflödet.</li></ul> <br> Observera att för vissa destinationer kan du vara begränsad till färre än 250 målgrupper mappade till målet. Dessa destinationer beskrivs längre ned på sidan i respektive avsnitt. |
| Maximalt antal attribut som har mappats till ett mål | 50 | Prestandaskydd | Om det finns flera mål- och måltyper kan du välja profilattribut och identiteter att mappa för export. För optimala prestanda bör maximalt 50 attribut mappas i ett dataflöde till ett mål. |
| Högsta antal destinationer | 100 | Systemstyrt skyddsräcke | Du kan skapa högst 100 mål som du kan ansluta och aktivera data till, *per sandbox*. [Edge personaliseringsmål (Anpassad anpassning)](#edge-destinations-activation) kan utgöra högst 10 av de 100 rekommenderade målen. |
| Typ av data som aktiveras för destinationer | Profildata, inklusive identiteter och identitetskarta | Systemstyrt skyddsräcke | För närvarande går det bara att exportera *profilpostattribut* till mål. XDM-attribut som beskriver händelsedata stöds för närvarande inte för export. |
| Typ av data som aktiveras för mål - stöd för matris- och mappattribut | Delvis tillgänglig | Systemstyrt skyddsräcke | Du kan exportera matrisattribut till [filbaserade mål](/help/destinations/destination-types.md#file-based). [Läs mer](/help/destinations/ui/export-arrays-maps-objects.md) om funktionaliteten. |

{style="table-layout:auto"}

### Aktivering av strömning {#streaming-activation}

Skyddsritningarna nedan gäller aktivering via [direktuppspelningsmål](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Antal aktiveringar (HTTP-meddelanden med profilexporter) per sekund | N/A | – | Det finns för närvarande ingen gräns för hur många meddelanden per sekund som skickas från Experience Platform till partnermålens API-slutpunkter. <br> Alla begränsningar eller latenser anges av slutpunkten där Experience Platform skickar data. Kontrollera även sidan [katalog](/help/destinations/catalog/overview.md) för målet som du ansluter och aktiverar data till. |

{style="table-layout:auto"}

### Batchaktivering (filbaserad) {#batch-file-based-activation}

Skyddskisserna nedan gäller aktivering via [gruppbaserade (filbaserade) mål](/help/destinations/ui/activate-batch-profile-destinations.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Aktiveringsfrekvens | En daglig hel export eller mer frekvent stegvis export var 3, 6, 8 eller 12: e timme. | Systemstyrt skyddsräcke | Läs avsnitten om [export av fullständiga filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) och [export av stegvisa filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) om du vill ha mer information om frekvensökningarna för batchexport. |
| Maximalt antal målgrupper som kan exporteras vid en given timme | 100 | Prestandaskydd | Rekommendationen är att lägga till högst 100 målgrupper i batchmåldataflöden. |
| Maximalt antal rader (poster) per fil som ska aktiveras | 5 miljoner | Systemstyrt skyddsräcke | Adobe Experience Platform delar automatiskt upp de exporterade filerna i 5 miljoner poster (rader) per fil. Varje rad representerar en profil. Delade filnamn läggs till med ett nummer som anger att filen är en del av en större export, till exempel: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Mer information finns i [schemaläggningsavsnittet](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) i självstudiekursen om aktivering av batchmål. |

{style="table-layout:auto"}

### Ad hoc-aktivering {#ad-hoc-activation}

Skyddsritningarna nedan gäller metoden [ad hoc-aktivering](/help/destinations/api/ad-hoc-activation-api.md).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Målgrupper aktiverade per ad hoc-aktiveringsjobb | 80 | Systemstyrt skyddsräcke | För närvarande kan varje ad hoc-aktiveringsjobb aktivera upp till 80 målgrupper. Om du försöker aktivera fler än 80 målgrupper per jobb misslyckas jobbet. Detta beteende kan komma att ändras i framtida versioner. |
| Samtidiga ad hoc-aktiveringsjobb per målgrupp | 1 | Systemstyrt skyddsräcke | Kör inte mer än ett samtidiga ad hoc-aktiveringsjobb per målgrupp. |

{style="table-layout:auto"}

### Aktivera Edge personaliseringsmål {#edge-destinations-activation}

Skyddsklippen nedan gäller aktivering via [kantanpassningsmål](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal [anpassade personaliseringsmål](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Prestandaskydd | Du kan konfigurera dataflöden till 10 anpassade mål för personalisering per sandlåda. |
| Maximalt antal attribut som mappats till ett personaliseringsmål per sandlåda | 30 | Systemstyrt skyddsräcke | Högst 30 attribut kan mappas i ett dataflöde till ett personaliseringsmål per sandlåda. |
| Maximalt antal målgrupper som har mappats till ett enda [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)-mål | 50 | Prestandaskydd | Du kan aktivera maximalt 50 målgrupper i ett aktiveringsflöde till ett enda Adobe Target-mål. |

{style="table-layout:auto"}

### Datauppsättningsexporter {#dataset-exports}

Datauppsättningsexporter stöds för närvarande i ett **[!UICONTROL First Full and then Incremental]** [mönster](/help/destinations/ui/export-datasets.md#scheduling). Skyddsutkast som beskrivs i det här avsnittet *gäller för den första fullständiga exporten* som sker efter att ett arbetsflöde för datauppsättningsexport har ställts in.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Datauppsättningstyper {#dataset-types}

Skyddsfilerna för datauppsättningsexport gäller för två typer av datauppsättningar som exporteras från Experience Platform, enligt beskrivningen nedan:

**Datauppsättningar baserade på XDM Experience Events-schemat**
När det gäller datauppsättningar som baseras på XDM Experience Events-schemat innehåller datauppsättningsschemat en *timestamp* -kolumn på den översta nivån. Data importeras endast som tillägg.

**Datauppsättningar baserade på schemat för enskild XDM-profil**
När det gäller datauppsättningar som baseras på XDM-schemat för enskild profil, innehåller datasetet inte en *timestamp* -kolumn på den översta nivån. Data hämtas in på ett sätt som präglas av förändring.

Skyddsutkastet nedan gäller alla datauppsättningar som exporteras från Experience Platform. Granska även de hårda garantierna nedan, som gäller olika datamängder och komprimeringstyper.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Storlek på exporterade datamängder | 5 miljarder poster | Prestandaskydd | Gränsen som beskrivs här för datauppsättningsexport är en *mjuk garanti*. Även om användargränssnittet inte hindrar dig från att exportera datauppsättningar som är större än 5 miljarder poster, är beteendet oförutsägbart och exporten kan antingen misslyckas eller ha mycket lång exportfördröjning. |

{style="table-layout:auto"}

#### Gardrader för schemalagda datauppsättningsexporter

För schemalagda eller återkommande datauppsättningsexporter är skyddsritningarna nedan identiska för de två formaten för den exporterade filen (JSON eller parquet) och grupperas efter datamängdstyp.

>[!WARNING]
>
>Export till JSON-filer stöds endast i komprimerat läge.

| Datauppsättningstyp | Guardrail | Typ av skyddsräcke | Beskrivning |
---------|----------|---------|-------|
| Datauppsättningar baserade på **XDM Experience Events-schemat** | De senaste 365 dagarna | Systemstyrt skyddsräcke | Data från det senaste kalenderåret exporteras. |
| Datauppsättningar baserade på schemat **XDM för enskild profil** | Tio miljarder poster i alla exporterade filer i ett dataflöde | Systemstyrt skyddsräcke | Antalet poster i datauppsättningen måste vara mindre än tio miljarder för komprimerade JSON- eller parquet-filer och en miljon för okomprimerade parquet-filer, annars misslyckas exporten. Minska storleken på datauppsättningen som du försöker exportera om den är större än det tillåtna tröskelvärdet. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

Läs mer om [att exportera datauppsättningar](/help/destinations/ui/export-datasets.md).


### Destination SDK skyddsräcken {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till slutpunkten, baserat på vilka data- och autentiseringsformat du väljer. Skyddsritningarna nedan gäller de mål som du konfigurerar med Destination SDK.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal [privata anpassade mål](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Prestandaskydd | Du kan skapa högst 5 privata anpassade direktuppspelnings- eller gruppmål med Destination SDK. Kontakta en kundtjänstrepresentant om du behöver skapa fler än fem sådana destinationer. |
| Profilexportpolicy för Destination SDK | <ul><li>`maxBatchAgeInSecs` (minst 1 800 och högst 3 600)</li><li>`maxNumEventsInBatch` (minst 1 000 och högst 10 000)</li></ul> | Systemstyrt skyddsräcke | När du använder alternativet [konfigurerbar aggregering](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) för ditt mål bör du tänka på minimi- och maximivärdena som avgör hur ofta HTTP-meddelanden skickas till ditt API-baserade mål och hur många profiler meddelandena ska innehålla. |

{style="table-layout:auto"}

### Princip för målbegränsning och återförsök {#destination-throttling-and-retry-policy}

Uppgifter om begränsningströsklar eller begränsningar för angivna destinationer. I det här avsnittet finns även information om återförsökspolicyn för destinationer.

| Typ av mål | Beskrivning |
| --- | --- |
| Företagsmål (HTTP API, Amazon Kinesis, Azure EventHubs) | På 95 % av tiden försöker Experience Platform erbjuda en genomströmningslatens på mindre än 10 minuter för meddelanden som skickats utan fel med en hastighet på mindre än 10 000 förfrågningar per sekund för varje dataflöde till en företagsdestination. <br> Om det uppstår misslyckade begäranden till ditt företagsmål, lagrar Experience Platform de misslyckade förfrågningarna och försöker skicka dem till din slutpunkt två gånger. |

{style="table-layout:auto"}

## Nästa steg

I följande dokumentation finns mer information om andra Experience Platform servicemarginaler, om total latenstid och licensieringsinformation från Real-Time CDP produktbeskrivningsdokument:

* [Real-Time CDP skyddsräcken](/help/rtcdp/guardrails/overview.md)
* [Avancerade latensdiagram](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.
* [Real-Time Customer Data Platform (B2C Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
