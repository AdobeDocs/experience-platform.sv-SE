---
keywords: cloud storage destination;cloud storage
title: Lagringsmål i molnet
seo-title: Lagringsmål i molnet
description: CDP i realtid i Adobe kan leverera dina segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser.
seo-description: CDP i realtid i Adobe kan leverera dina segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Lagringsmål i molnet {#cloud-storage-destinations}

Adobe CDP i realtid kan leverera era segment som datafiler till era molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer för [!DNL Amazon S3] och SFTP. För [!DNL AWS Kinesis] och [!DNL Azure Event Hubs] för destinationer direktuppspelas data från Experience Platform i JSON-format.

![Lagringsmål för Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Mer information om hur du ansluter till molnlagringsmål finns i [Arbetsflöde för att skapa molnlagringsmål](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## Dataexporttyp

**Profilbaserad export** - du exporterar information om individerna i målgruppen. Den här informationen behövs för personalisering och kan innehålla attribut, händelser, segmentmedlemskap osv.

## Tillgängliga molnlagringsmål

* [Amazon S3-mål](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP-mål](/help/rtcdp/destinations/sftp-destination.md)

## Tillgängliga direktuppspelningsmål för molnlagring

* [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azure Event Hubs-mål](/help/rtcdp/destinations/azure-event-hubs-destination.md)