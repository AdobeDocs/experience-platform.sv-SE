---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Standardvarningsregler
description: 'Detta dokument innehåller de fördefinierade varningsreglerna från Experience Platform. '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 10%

---


# Standardvarningsregler

Adobe Experience Platform innehåller flera fördefinierade varningsregler som du kan aktivera för din organisation. Tabellen nedan innehåller uppgifter om dessa varningsregler som tillhandahålls av Adobe. Mer allmän information om varningar i Experience Platform finns i [varningsöversikten](./overview.md).

| Regel | Beskrivning | Utvärderingsfrekvens | Upprepa fönster |
| --- | --- | --- | --- |
| Tröskelvärdet för berättigandet har överskridits | Den här varningen utlöses när antalet skapade profiler överstiger 80 % av organisationens berättigande. | 30 sekunder | Ej tillämpligt |
| Ingen intagsaktivitet de senaste 24 timmarna | Denna varning utlöses när inga nya data har importerats under den senaste 24-timmarsperioden. | 1 dag | 1 dag |
| SFTP-källan har inga inkapslade data | Den här varningen utlöses när en [SFTP-källa](../../sources/connectors/cloud-storage/sftp.md) inte har importerat några data inom en viss tidsperiod. | 1 dag | 1 dag |
| Inmatningsfel har överskridits | Den här varningen utlöses när felfrekvensen för datainmatning överstiger 20 %. | 30 sekunder | 30 sekunder |
| Feed-meddelande | Den här varningen när ett identitetsdelningsfeed-meddelande har skickats till en användare med [Segmentmatchning](../../segmentation/ui/segment-match.md). | Ej tillämpligt | Ej tillämpligt |
| Feed Access har återkallats | Den här varningen utlöses när en annan plattformsanvändare återkallar åtkomsten till en identitetsdelningsfeed med [Segmentmatchning](../../segmentation/ui/segment-match.md). | Ej tillämpligt | Ej tillämpligt |
| Feed ändrad | Den här varningen utlöses när en identitetsdelningsfeed ändras av en användare med [Segmentmatchning](../../segmentation/ui/segment-match.md). | Ej tillämpligt | Ej tillämpligt |
| Feed Shared | Den här varningen utlöses när en användare delar en ny feed i [Segmentmatchning](../../segmentation/ui/segment-match.md). | Ej tillämpligt | Ej tillämpligt |
| Länkbegäran | Den här varningen utlöses när en användare begär anslutning för partnerdelning. | Ej tillämpligt | Ej tillämpligt |
| Länkåtgärd | Den här varningen utlöses när en användare accepterar en anslutningsbegäran för partnerdelning. | Ej tillämpligt | Ej tillämpligt |
| Segmentdefinition inaktiverad | Den här varningen utlöses när en segmentdefinition är inaktiverad. | Ej tillämpligt | Ej tillämpligt |
| Fördröjning för segmentjobb | Den här varningen utlöses när det tar längre tid än 150 minuter att slutföra ett segmentjobb. | 30 sekunder | 3 timmar |
| Körningsfel för källflöde | Den här varningen utlöses när ett fel inträffar när data hämtas från en källanslutning. | Ej tillämpligt | Ej tillämpligt |
| Källflöde har körts | Den här varningen utlöses när data har importerats från en källanslutning. | Ej tillämpligt | Ej tillämpligt |

{style=&quot;table-layout:auto&quot;}