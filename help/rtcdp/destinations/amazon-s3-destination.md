---
title: Amazon S3-mål
seo-title: Amazon S3-mål
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
seo-description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
translation-type: tm+mt
source-git-commit: acd3865be4994a478048d317060c55b7e0d9914c

---


# Amazon S3-mål

## Översikt

Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsdestinationer, inklusive Amazon S3, finns [i arbetsflödet för ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)molnlagringsdestinationer.

För Amazon S3-mål anger du följande information i arbetsflödet för att skapa mål:

* **Åtkomstnyckel till Amazon S3 och hemlig nyckel** till Amazon S3: Generera en åtkomstnyckel - nyckelpar för hemlig åtkomst i Amazon S3 för att ge Adobe CDP-åtkomst i realtid till ditt Amazon S3-konto.
* **Amazon S3-sökväg**: Detta är den plats i Amazon S3-bucket där Adobe Real-time CDP levererar exportfiler.


>[!IMPORTANT]
>
>Adobe CDP i realtid behöver `write` behörigheter för det bucket-objekt där exportfilerna ska levereras.
