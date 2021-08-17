---
keywords: Amazon S3;S3-mål;s3;amazon s3
title: Amazon S3-anslutning
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagring för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# [!DNL Amazon S3] anslutning {#s3-connection}

## Översikt {#overview}

Skapa en utgående liveanslutning till ditt [!DNL Amazon Web Services] (AWS) S3-lagringsutrymme för att regelbundet exportera tabbavgränsade filer eller CSV-datafiler från Adobe Experience Platform till dina egna S3-fack.

## Exporttyp {#export-type}

**Profilbaserat**  - du exporterar alla medlemmar i ett segment tillsammans med önskade schemafält (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut i arbetsflödet [ för ](../../ui/activate-segment-streaming-destinations.md#mapping)målaktivering.

![Profilbaserad export av Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!DNL Amazon S3]åtkomstnyckel** och  **[!DNL Amazon S3]hemlig nyckel**: Generera  [!DNL Amazon S3]ett  `access key - secret access key` par som ger plattformsåtkomst till ditt  [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Bucket name]**: Ange namnet på den  [!DNL Amazon S3] bucket som ska användas för detta mål.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.

Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64]-kodad sträng.

>[!TIP]
>
>I arbetsflödet för anslutningsmål kan du skapa en anpassad mapp i din Amazon S3-lagring per exporterad segmentfil. Läs [Använd makron för att skapa en mapp på din lagringsplats](overview.md#use-macros) för instruktioner.

### Nödvändiga [!DNL Amazon S3]-behörigheter {#required-s3-permission}

Om du vill ansluta och exportera data till din [!DNL Amazon S3]-lagringsplats skapar du en IAM-användare (Identity and Access Management) för [!DNL Platform] i [!DNL Amazon S3] och tilldelar behörigheter för följande åtgärder:

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

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata för att batchprofilens exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

För [!DNL Amazon S3]-mål skapar [!DNL Platform] en tabbavgränsad `.csv`-fil på den angivna lagringsplatsen. Mer information om filerna finns i [Aktivera målgruppsdata till exportmål för gruppprofiler](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringsjälvstudiekursen.
