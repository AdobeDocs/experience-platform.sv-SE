---
keywords: Amazon S3;S3-mål;s3;amazon s3
title: Amazon S3-mål
seo-title: Amazon S3-mål
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
seo-description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Amazon S3] mål

## Översikt

Skapa en utgående liveanslutning till ditt [!DNL Amazon Web Services] (AWS) S3-lagringsutrymme för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-fack.

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-destinations.md#select-attributes)målaktivering.

![Profilbaserad export av Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Anslutningsmål {#connect-destination}

Mer information om hur du ansluter till molnlagringsplatserna finns i [Arbetsflödet ](./workflow.md) för molnlagringsmål, inklusive [!DNL Amazon S3].

För [!DNL Amazon S3]-mål anger du följande information i arbetsflödet för att skapa mål:

* **[!DNL Amazon S3]åtkomstnyckel och  [!DNL Amazon S3] hemlig nyckel**: Generera  [!DNL Amazon S3]ett  `access key - secret access key` par som ger plattformsåtkomst till ditt  [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>Plattformen behöver `write` behörigheter för det bucket-objekt där exportfilerna ska levereras.

## Exporterade data {#exported-data}

För [!DNL Amazon S3]-mål skapar Platform en tabbavgränsad `.txt`- eller `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [E-postmarknadsföringsmål och molnlagringsmål](../../ui/activate-destinations.md#esp-and-cloud-storage) i självstudiekursen om segmentaktivering.
