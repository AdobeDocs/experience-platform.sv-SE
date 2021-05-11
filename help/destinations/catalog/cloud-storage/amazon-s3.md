---
keywords: Amazon S3;S3-mål;s3;amazon s3
title: Amazon S3-anslutning
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
translation-type: tm+mt
source-git-commit: 7780a2b3b518ab976ec14531892e0734a6342e4c
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# [!DNL Amazon S3] anslutning  {#s3-connection}

## Översikt {#overview}

Skapa en utgående liveanslutning till ditt [!DNL Amazon Web Services] (AWS) S3-lagringsutrymme för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-fack.

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

![Profilbaserad export av Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Anslutningsmål {#connect-destination}

Mer information om hur du ansluter till molnlagringsplatserna finns i [Arbetsflödet ](./workflow.md) för molnlagringsmål, inklusive [!DNL Amazon S3].

För [!DNL Amazon S3]-mål anger du följande information i arbetsflödet för att skapa mål:

* **[!DNL Amazon S3]åtkomstnyckel och  [!DNL Amazon S3] hemlig nyckel**: Generera  [!DNL Amazon S3]ett  `access key - secret access key` par som ger plattformsåtkomst till ditt  [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

## Nödvändiga [!DNL Amazon S3]-behörigheter {#required-s3-permission}

Om du vill ansluta och exportera data till din [!DNL Amazon S3]-lagringsplats skapar du en IAM-användare för [!DNL Platform] i [!DNL Amazon S3] och tilldelar behörigheter för följande åtgärder:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Exporterade data {#exported-data}

För [!DNL Amazon S3]-mål skapar [!DNL Platform] en tabbavgränsad `.txt`- eller `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.
