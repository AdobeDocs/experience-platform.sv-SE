---
keywords: Experience Platform;aktivering;felsökning;skyddsförslag;riktlinjer;gräns
title: Standardskyddsutkast för aktiveringsdata
solution: Experience Platform
product: experience platform
type: Documentation
description: Läs mer om standardanvändning och hastighetsbegränsningar för dataaktivering.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 1132c5166f1271f1b8eb0c618b83d028b413b991
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# Garantier för aktiveringsdata

Den här sidan innehåller standardvärden för användning och hastighetsbegränsningar för aktiveringsbeteende. När du granskar följande skyddsutkast förutsätts det att du har rätt [anslutna till destinationer](/help/destinations/ui/connect-destination.md).

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
| Maximalt antal segment till ett enda mål | 250 | Mjuk | Rekommendationen är att mappa högst 250 segment till ett enda mål i ett dataflöde. <br><br> Om du behöver aktivera fler än 250 segment till ett mål kan du antingen: <ul><li> Dela upp segment som du inte längre vill aktivera, eller</li><li>Skapa ett nytt dataflöde till önskat mål och mappa segment till det nya dataflödet.</li></ul> <br> Observera att för vissa destinationer kan du vara begränsad till färre än 250 segment som är mappade till målet. Dessa destinationer beskrivs längre ned på sidan i respektive avsnitt. |
| Högsta antal destinationer | 100 | Mjuk | Rekommendationen är att skapa högst 100 destinationer som du kan ansluta och aktivera data till *per sandlåda*. [Destinationer för kantanpassning (anpassad personalisering)](#edge-destinations-activation) kan utgöra högst 10 av de 100 rekommenderade destinationerna. |
| Maximalt antal attribut som har mappats till ett mål | 50 | Mjuk | Om det finns flera mål- och måltyper kan du välja profilattribut och identiteter att mappa för export. För optimala prestanda bör maximalt 50 attribut mappas i ett dataflöde till ett mål. |
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
| Aktiveringsfrekvens | En daglig fullständig export eller mer frekvent stegvis export var 3, 6, 8 eller 12 timme. | Hård | Läs [exportera fullständiga filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) och [exportera inkrementella filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) dokumentationsavsnitt för mer information om frekvensökningar för batchexport. |
| Maximalt antal segment som kan exporteras vid en given timme | 100 | Mjuk | Rekommendationen är att lägga till högst 100 segment i batchmåldataflöden. |
| Maximalt antal rader (poster) per fil som ska aktiveras | 5 miljoner | Hård | Adobe Experience Platform delar automatiskt upp de exporterade filerna i 5 miljoner poster (rader) per fil. Varje rad representerar en profil. Delade filnamn läggs till med en siffra som anger att filen är en del av en större export: `filename.csv`, `filename_2.csv`, `filename_3.csv`. Mer information finns i [planeringsavsnitt](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) av självstudiekursen om aktivering av batchdestinationer. |

{style="table-layout:auto"}

### Ad hoc-aktivering {#ad-hoc-activation}

Skyddsritningarna nedan gäller för [ad hoc-aktivering](/help/destinations/api/ad-hoc-activation-api.md) -metod.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Aktiverade segment per ad hoc-aktiveringsjobb | 80 | Hård | För närvarande kan varje ad hoc-aktiveringsjobb aktivera upp till 80 segment. Om du försöker aktivera fler än 80 segment per jobb misslyckas jobbet. Detta beteende kan komma att ändras i framtida versioner. |
| Samtidiga ad hoc-aktiveringsjobb per segment | 1 | Hård | Kör inte mer än ett samtidiga ad hoc-aktiveringsjobb per segment. |

{style="table-layout:auto"}

### Aktivering av mål för kantanpassning {#edge-destinations-activation}

Skyddskassorna nedan gäller aktivering via [mål för kantanpassning](/help/destinations/destination-types.md#streaming-profile-export).

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal [Anpassad personalisering](/help/destinations/catalog/personalization/custom-personalization.md) mål | 10 | Mjuk | Du kan konfigurera dataflöden till 10 anpassade mål för personalisering per sandlåda. |
| Maximalt antal attribut som mappats till ett personaliseringsmål per sandlåda | 30 | Hård | Högst 30 attribut kan mappas i ett dataflöde till ett personaliseringsmål per sandlåda. |
| Maximalt antal segment mappade till ett enskilt [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) mål | 50 | Mjuk | Du kan aktivera maximalt 50 segment i ett aktiveringsflöde till ett enda Adobe Target-mål. |

{style="table-layout:auto"}

### Destinationens SDK skyddsräcken {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) är en uppsättning konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster för Experience Platform så att målgrupps- och profildata kan skickas till slutpunkten, baserat på valfritt data- och autentiseringsformat. Skyddsritningarna nedan gäller de mål som du konfigurerar med Destination SDK.

| Guardrail | Gräns | Begränsa typ | Beskrivning |
| --- | --- | --- | --- |
| Maximalt antal [privata anpassade destinationer](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Mjuk | Du kan skapa högst 5 privata anpassade direktuppspelnings- eller gruppmål med hjälp av Destination SDK. Kontakta en kundtjänstrepresentant om du behöver skapa fler än fem sådana destinationer. |
| Profilexportpolicy för Destination SDK | <ul><li>`maxBatchAgeInSecs` (minst 1 800 och högst 3 600)</li><li>`maxNumEventsInBatch` (minimum 1.000, max 10.000)</li></ul> | Hård | När du använder [konfigurerbar aggregering](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) för ditt mål bör du tänka på de lägsta och högsta värden som avgör hur ofta HTTP-meddelanden skickas till ditt API-baserade mål och hur många profiler meddelandena ska innehålla. |

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
