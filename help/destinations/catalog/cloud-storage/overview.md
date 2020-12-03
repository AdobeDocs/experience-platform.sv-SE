---
keywords: cloud storage destination;cloud storage
title: Lagringsmål i molnet
seo-title: Lagringsmål i molnet
description: CDP kan leverera era segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser i realtid.
seo-description: CDP kan leverera era segment som datafiler till Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP:s molnlagringsplatser i realtid.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Lagringsmål i molnet {#cloud-storage-destinations}

CDP kan leverera era segment som datafiler till era molnlagringsplatser i realtid. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer för [!DNL Amazon S3] och SFTP. För [!DNL AWS Kinesis] och [!DNL Azure Event Hubs] för destinationer direktuppspelas data från Experience Platform i JSON-format.

![Lagringsmål för Adobe Cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Mer information om hur du ansluter till molnlagringsmål finns i [Arbetsflöde för att skapa molnlagringsmål](./workflow.md).

## Dataexporttyp

**Profilbaserad export** - du exporterar information om individerna i målgruppen. Den här informationen behövs för personalisering och kan innehålla attribut, händelser, segmentmedlemskap osv.

## Tillgängliga molnlagringsmål

- [Amazon S3-mål](./amazon-s3.md)
- [SFTP-mål](./sftp.md)

## Tillgängliga direktuppspelningsmål för molnlagring

- [Amazon Kinesis](./amazon-kinesis.md)
- [Azure Event Hubs-mål](./azure-event-hubs.md)