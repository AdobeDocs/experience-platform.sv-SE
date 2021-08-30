---
keywords: Experience Platform;hem;populära ämnen;datumintervall
title: Standardvarningsregler
description: 'Detta dokument innehåller de fördefinierade varningsreglerna från Experience Platform. '
source-git-commit: de8d8d92622abc75f2d09f4bb771dbe4268d0b38
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 8%

---


# Standardvarningsregler

Adobe Experience Platform innehåller flera fördefinierade varningsregler som du kan aktivera för din organisation. Tabellen nedan innehåller uppgifter om dessa varningsregler som tillhandahålls av Adobe. Mer allmän information om varningar i Experience Platform finns i [varningsöversikten](./overview.md).

| Regel | Beskrivning | Utvärderingsfrekvens | Upprepa fönster |
| --- | --- | --- | --- |
| Källflöde har körts | Den här varningen utlöses när data har importerats från en källanslutning. | Ej tillämpligt | Ej tillämpligt |
| Körningsfel för källflöde | Den här varningen utlöses när ett fel inträffar när data hämtas från en källanslutning. | Ej tillämpligt | Ej tillämpligt |
| Fördröjning för segmentjobb | Den här varningen utlöses när det tar längre tid än 150 minuter att slutföra ett segmentjobb. | 30 sekunder | 3 timmar |
| Segmentdefinition inaktiverad | Den här varningen utlöses när en segmentdefinition är inaktiverad. | Ej tillämpligt | Ej tillämpligt |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
