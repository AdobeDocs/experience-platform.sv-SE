---
title: Lagringsmål i molnet
seo-title: Lagringsmål i molnet
description: Adobe CDP kan i realtid leverera era segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser.
seo-description: Adobe CDP kan i realtid leverera era segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Lagringsmål i molnet {#cloud-storage-destinations}

Adobe CDP kan leverera era segment som datafiler till era molnlagringsplatser i realtid. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer för [!DNL Amazon S3] och SFTP. För [!DNL AWS Kinesis] och [!DNL Azure Event Hubs] för destinationer direktuppspelas data från Experience Platform i JSON-format.

![Lagringsmål för Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Mer information om hur du ansluter till molnlagringsmål finns i [Arbetsflöde för att skapa molnlagringsmål](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## Dataexporttyp

**Profilbaserad export** - du exporterar information om individerna i målgruppen. Den här informationen behövs för personalisering och kan innehålla attribut, händelser, segmentmedlemskap osv.

## Tillgängliga molnlagringsmål

* [Amazon S3-mål](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP-mål](/help/rtcdp/destinations/sftp-destination.md)

## Tillgängliga direktuppspelningsmål för molnlagring

* [Amazon Kinesis-mål](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azure Event Hubs-mål](/help/rtcdp/destinations/azure-event-hubs-destination.md)