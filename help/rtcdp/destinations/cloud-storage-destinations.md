---
title: Lagringsmål i molnet
seo-title: Lagringsmål i molnet
description: Adobe CDP kan i realtid leverera era segment som datafiler till Amazon S3- eller SFTP-molnlagringsplatser. Vi kommer att lägga till fler destinationer för molnlagring i kommande versioner.
seo-description: Adobe CDP kan i realtid leverera era segment som datafiler till Amazon S3- eller SFTP-molnlagringsplatser. Vi kommer att lägga till fler destinationer för molnlagring i kommande versioner.
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342

---


# Lagringsmål i molnet {#cloud-storage-destinations}

Adobe CDP kan i realtid leverera era segment som datafiler till Amazon S3- eller SFTP-molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer.

![Lagringsmål för Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Adobe CDP stöder för närvarande två molnlagringsdestinationer i realtid - [Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) och [SFTP](/help/rtcdp/destinations/sftp-destination.md). Vi kommer att lägga till fler destinationer för molnlagring i kommande versioner.

Mer information om hur du ansluter till molnlagringsmål finns i [Arbetsflöde för att skapa molnlagringsmål](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## Dataexporttyp

**Profilbaserad export** - du exporterar information om individerna i målgruppen. Den här informationen behövs för personalisering och kan innehålla attribut, händelser, segmentmedlemskap osv.

