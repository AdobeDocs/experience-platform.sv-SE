---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3-mål
seo-title: Amazon S3-mål
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
seo-description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
translation-type: tm+mt
source-git-commit: 4c45da353b1deeb66b0dedb37450158f4bdc2a7c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# [!DNL Amazon S3] mål

## Översikt

Skapa en utgående liveanslutning till ditt [!DNL Amazon Web Services] (AWS) S3-lagringsutrymme för att regelbundet exportera tabbavgränsade eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsdestinationer finns [i arbetsflödet för ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)molnlagringsdestinationer, inklusive [!DNL Amazon S3].

Ange följande information i arbetsflödet för att skapa mål för [!DNL Amazon S3] mål:

* **[!DNL Amazon S3]åtkomstnyckel och[!DNL Amazon S3]hemlig nyckel**: Generera [!DNL Amazon S3]i stället ett `access key - secret access key` par som ger CDP-åtkomst i realtid i Adobe till ditt [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>CDP i realtid i Adobe behöver `write` behörigheter för det bucket-objekt där exportfilerna ska levereras.

## Exporterade data {#exported-data}

För [!DNL Amazon S3] mål skapar Adobe Real-time CDP en tabbavgränsad fil `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
