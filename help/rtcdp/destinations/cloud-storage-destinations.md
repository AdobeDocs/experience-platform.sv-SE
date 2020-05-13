---
title: Lagringsmål i molnet
seo-title: Lagringsmål i molnet
description: Adobe CDP kan i realtid leverera era segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser.
seo-description: Adobe CDP kan i realtid leverera era segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Lagringsmål i molnet {#cloud-storage-destinations}

Adobe CDP kan leverera era segment som datafiler till era molnlagringsplatser i realtid. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer för Amazon S3 och SFTP. För AWS Kinesis- och Azure Event Hubs-mål strömmas data ut från Experience Platform i JSON-format.

![Lagringsmål för Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Mer information om hur du ansluter till molnlagringsmål finns i [Arbetsflöde för att skapa molnlagringsmål](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## Dataexporttyp

**Profilbaserad export** - du exporterar information om individerna i målgruppen. Den här informationen behövs för personalisering och kan innehålla attribut, händelser, segmentmedlemskap osv.

## Tillgängliga molnlagringsmål

* [Amazon S3-mål](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP-mål](/help/rtcdp/destinations/sftp-destination.md)

## Tillgängliga direktuppspelningsmål för molnlagring

* [Amazon Kinesis-mål](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azure EventHubs-mål](/help/rtcdp/destinations/azure-event-hubs-destination.md)