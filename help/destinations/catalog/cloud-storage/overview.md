---
keywords: molnlagringsmål;molnlagring
title: Översikt över destinationer för molnlagring
description: Adobe Experience Platform kan leverera dina segment som datafiler till dina Amazon S3-, AWS Kinesis-, Azure Event Hubs- eller SFTP-molnlagringsplatser.
translation-type: tm+mt
source-git-commit: 48c5f6d6a45de5f7982543f7a43cb4ece8cf3a9f
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Översikt över mål för molnlagring {#cloud-storage-destinations}

Adobe Experience Platform kan leverera dina segment som datafiler till dina molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer för [!DNL Amazon S3] och SFTP. För [!DNL AWS Kinesis]- och [!DNL Azure Event Hubs]-mål direktuppspelas data från Experience Platform i JSON-format.

![Adobe molnlagringsdestinationer](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Mer information om hur du ansluter till molnlagringsmål finns i [Arbetsflöde för att skapa molnlagringsmål](./workflow.md).

## Dataexporttyp

**Profilbaserad export**  - du exporterar information om individerna i målgruppen. Den här informationen behövs för personalisering och kan innehålla attribut, händelser, segmentmedlemskap osv.

## Tillgängliga molnlagringsdestinationer

- [Amazon S3-anslutning](./amazon-s3.md)
- [Azure Blob-anslutning](./azure-blob.md)
- [SFTP-anslutning](./sftp.md)

## Tillgängliga direktuppspelningsmål för molnlagring

- [Amazon Kinesis-anslutning](./amazon-kinesis.md)
- [Azure Event Hubs-anslutning](./azure-event-hubs.md)