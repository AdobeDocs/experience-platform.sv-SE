---
title: Amazon S3-mål
seo-title: Amazon S3-mål
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-fack.
seo-description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-fack.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# [!DNL Amazon S3] mål

## Översikt

Skapa en utgående liveanslutning till ditt [!DNL Amazon Web Services] (AWS) S3-lagringsutrymme för att regelbundet exportera tabbavgränsade eller CSV-datafiler från Adobe Experience Platform till dina egna S3-fack.

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsdestinationer finns [i arbetsflödet för ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)molnlagringsdestinationer, inklusive [!DNL Amazon S3].

Ange följande information i arbetsflödet för att skapa mål för [!DNL Amazon S3] mål:

* **[!DNL Amazon S3]åtkomstnyckel och[!DNL Amazon S3]hemlig nyckel **: Generera[!DNL Amazon S3]i stället en åtkomstnyckel - nyckelpar för hemlig åtkomst som ger Adobe CDP-åtkomst i realtid till ditt[!DNL Amazon S3]konto.



>[!IMPORTANT]
>
>Adobe CDP i realtid behöver `write` behörigheter för det bucket-objekt där exportfilerna ska levereras.
