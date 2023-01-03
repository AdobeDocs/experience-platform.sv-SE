---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Standardvarningsregler
description: Detta dokument innehåller de fördefinierade varningsreglerna från Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# Standardvarningsregler

Adobe Experience Platform innehåller flera fördefinierade varningsregler som du kan aktivera för din organisation. Detta dokument innehåller uppgifter om dessa varningsregler som tillhandahålls av Adobe. Mer allmän information om varningar i Experience Platform finns i [varningsöversikt](./overview.md).

När [visa varningsregler i plattformsgränssnittet](./ui.md)kan du prenumerera på varje regel separat. När du prenumererar på aviseringar via [I/O-händelsemeddelanden](./subscribe.md)Men varningsreglerna är ordnade i olika prenumerationspaket. I tabellerna nedan visas varje regel med sitt motsvarande I/O Event-prenumerationsnamn.

## Dataintag

Följande varningsregler gäller [Dataintag](../../ingestion/home.md) och  [källor](../../sources/home.md):

| Prenumeration på I/O-händelse | Varningsregel | Beskrivning |
| --- | --- | --- |
| Körningsinformation för källflöde | Kör källflöde | Den här varningen utlöses när en källanslutning börjar bearbeta data. |
| Körningsinformation för källflöde | Källflöde har körts | Den här varningen utlöses när data har importerats från en källanslutning. |
| Körningsfördröjningar för källflöde, fel och fel | Körningsfel för källflöde | Den här varningen utlöses när ett fel inträffar när data hämtas från en källanslutning. |
| Körningsfördröjningar för källflöde, fel och fel | Fördröjning av intag | Den här varningen utlöses när ett batchmatningsflöde tar längre tid än 150 minuter att bearbeta. |
| Körningsfördröjningar för källflöde, fel och fel | Inmatningsfel | Den här varningen utlöses när förhållandet mellan misslyckade poster och alla poster överstiger ett tröskelvärde på 0,5 %. |

{style=&quot;table-layout:auto&quot;}

Om du tidigare har prenumererat på följande larmtyp får du inte längre några varningar eftersom den här varningen har tagits bort:

| Prenumeration på I/O-händelse | Varningsregel | Beskrivning |
| --- | --- | --- |
| Körningsfördröjningar för källflöde, fel och fel | Brist på intag | Den här varningen skickar ett meddelande om importen fördröjs med mer än sju timmar och inga data hämtas till Platform. |

{style=&quot;table-layout:auto&quot;}

## Identitetstjänst

Följande varningsregler gäller [Identitetstjänst](../../identity-service/home.md):

| Prenumeration på I/O-händelse | Varningsregel | Beskrivning |
| --- | --- | --- |
| Information om identitetsregistrering | Start för Identity Service Flow Run | Den här varningen utlöses när en körning av en identitetstjänst börjar bearbeta data. Med andra ord läses importerade data in från datasjön till identitetstjänsten. |
| Information om identitetsregistrering | Identitetstjänstens flöde har körts | Den här varningen utlöses när data har lästs in från datasjön till identitetstjänsten. |
| Fördröjningar för identitetsmatning, fel och fel | Körningsfördröjning för identitetstjänstens flöde | Den här varningen utlöses när en körning av en identitetstjänst tar längre tid än 150 minuter att bearbeta. |
| Fördröjningar för identitetsmatning, fel och fel | Körningsfel för identitetstjänstens flöde | Den här varningen utlöses när ett fel inträffar när data hämtas till identitetstjänsten. |

{style=&quot;table-layout:auto&quot;}

## Kundprofil i realtid

Följande varningsregler gäller [Kundprofil i realtid](../../profile/home.md):

| Prenumeration på I/O-händelse | Varningsregel | Beskrivning |
| --- | --- | --- |
| Information om profilinmatning | Körning av profilflöde | Den här varningen utlöses när en profilflödeskörning börjar bearbeta data. |
| Information om profilinmatning | Körning av profilflöde lyckades | Den här varningen utlöses när data har lästs in till profilen från Data Lake. |
| Fördröjningar för profilinmatning, fel och fel | Körningsfördröjning för profilflöde | Den här varningen utlöses när det tar längre tid än 150 minuter att läsa in data från datasjön till profilen. |
| Fördröjningar för profilinmatning, fel och fel | Körningsfel för profilflöde | Den här varningen utlöses när ett fel inträffar när data hämtas till profilen. |

{style=&quot;table-layout:auto&quot;}

## Segmentering

Följande varningsregler gäller [Segmenteringstjänst](../../segmentation/home.md):

| Prenumeration på I/O-händelse | Varningsregel | Beskrivning |
| --- | --- | --- |
| Information om utvärderingsjobb för segment | Start för segmentjobb | Den här varningen utlöses när ett segmentutvärderingsjobb börjar bearbeta data. |
| Information om utvärderingsjobb för segment | Segmentjobb lyckades | Den här varningen utlöses när ett segmentutvärderingsjobb har slutförts. |
| Förseningar, fel och fel i segmentutvärderingsjobb | Fördröjning för segmentjobb | Den här varningen utlöses när det tar längre tid än 150 minuter att slutföra ett segmentutvärderingsjobb. |
| Förseningar, fel och fel i segmentutvärderingsjobb | Fel i segmentjobb | Den här varningen utlöses när ett segmentutvärderingsjobb resulterar i ett fel. |
| Förseningar, fel och fel i segmentutvärderingsjobb | Segmentdefinition inaktiverad | Den här varningen utlöses när en segmentdefinition inaktiveras på grund av ett internt fel. Detta ger automatiskt ett krigsrum för en Adobe-tekniker att undersöka problemet. Denna varning är endast avsedd att vara informativ och kräver inga åtgärder från dig. |

{style=&quot;table-layout:auto&quot;}

## Mål 

Följande varningsregler gäller [mål](../../destinations/home.md):

| Prenumeration på I/O-händelse | Varningsregel | Beskrivning |
| --- | --- | --- |
| Körningsinformation för målflöde | Start för målflödeskörning | Den här varningen utlöses när en målflödeskörning börjar aktivera ett segment. |
| Körningsinformation för målflöde | Målflödet har körts | Den här varningen utlöses när ett segment har aktiverats till ett mål. |
| Körningsfördröjningar för målflöde, fel och fel | Körningsfördröjning för målflöde | Den här varningen utlöses när ett målflöde tar längre tid än 150 minuter att aktivera ett segment. |
| Körningsfördröjningar för målflöde, fel och fel | Körningsfel för målflöde | Den här varningen utlöses när ett fel inträffar när ett segment aktiveras till ett mål. |
| Körningsfördröjningar för målflöde, fel och fel | Överskridningsgraden överskrider tröskelvärdet | Den här varningen utlöses när förhållandet mellan överhoppade ID:n och totalt ID:n överskrider ett tröskelvärde. |

{style=&quot;table-layout:auto&quot;}

## Frågetjänst

Följande varningsregler gäller [Frågetjänst](../../query-service/home.md):

| Prenumeration på I/O-händelse | Varningsregel | Beskrivning |
| --- | --- | --- |
| Information om schemalagd fråga för frågetjänst | Start av schemalagd fråga för frågetjänst | Den här varningen utlöses när en schemalagd fråga börjar köras. |
| Information om schemalagd fråga för frågetjänst | Frågan har planerats för frågetjänsten | Den här varningen utlöses när ett schemalagt frågejobb slutförs. |
| Schemalagda frågefördröjningar, fel och fel för frågetjänsten | schemalagd frågefel för frågetjänsten | Den här varningen utlöses när ett schemalagt frågejobb misslyckas. |

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
