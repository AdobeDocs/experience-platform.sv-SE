---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3-mål
seo-title: Amazon S3-mål
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
seo-description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] mål

## Översikt

Skapa en utgående liveanslutning till ditt [!DNL Amazon Web Services] (AWS) S3-lagringsutrymme för att regelbundet exportera tabbavgränsade eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [för](../../ui/activate-destinations.md#select-attributes)målaktivering.

![Profilbaserad export av Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Koppla mål {#connect-destination}

Mer information om hur du ansluter till molnlagringsdestinationer finns i arbetsflödet för [molnlagringsdestinationer, inklusive ](./workflow.md) [!DNL Amazon S3].

Ange följande information i arbetsflödet för att skapa mål för [!DNL Amazon S3] mål:

* **[!DNL Amazon S3]åtkomstnyckel och [!DNL Amazon S3] hemlig nyckel**: Generera [!DNL Amazon S3]ett `access key - secret access key` par för att ge realtidsåtkomst till ditt [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>CDP i realtid behöver `write` behörigheter för det bucket-objekt där exportfilerna ska levereras.

## Exporterade data {#exported-data}

För [!DNL Amazon S3] mål skapar CDP i realtid en tabbavgränsad fil `.txt` eller `.csv` fil på den lagringsplats som du angav. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.
