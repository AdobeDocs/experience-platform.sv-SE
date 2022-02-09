---
keywords: Amazon S3;S3-mål;s3;amazon s3
title: Amazon S3-anslutning
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagringsplats för att regelbundet exportera CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: e6dc0fb136a6f5199153630a20e8809c2c040107
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# [!DNL Amazon S3] anslutning {#s3-connection}

## Översikt {#overview}

Skapa en utgående liveanslutning till din [!DNL Amazon Web Services] (AWS) S3-lagring för att regelbundet exportera CSV-datafiler från Adobe Experience Platform till dina egna S3-bucket.

## Exporttyp {#export-type}

**Profilbaserad** - du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (till exempel: e-postadress, telefonnummer, efternamn), som du väljer på skärmen Välj attribut på [arbetsflöde för målaktivering](../../ui/activate-segment-streaming-destinations.md#mapping).

![Profilbaserad export av Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Bucketnamn"
>abstract="Måste vara mellan 3 och 63 tecken långt. Måste börja och sluta med en bokstav eller siffra. Får endast innehålla gemena bokstäver, siffror eller bindestreck ( - ). Får inte formateras som en IP-adress (till exempel 192.100.1.1)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Mappsökväg"
>abstract="Får endast innehålla tecknen A-Z, a-z, 0-9 och kan innehålla följande specialtecken: `/!-_.'()"^[]+$%.*"`. Om du vill skapa en mapp per segmentfil infogar du makrot /%SEGMENT_NAME% eller /%SEGMENT_ID% eller /%SEGMENT_NAME%/%SEGMENT_ID% i textfältet. Makron kan bara infogas i slutet av mappsökvägen. Visa makroexempel i dokumentationen."
>text="Learn more in documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#use-macros" text="Använd makron för att skapa en mapp på lagringsplatsen"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Den offentliga nyckeln måste skrivas som en Base64-kodad sträng."
>text="Learn more in documentation"

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!DNL Amazon S3]åtkomstnyckel** och **[!DNL Amazon S3]hemlig nyckel**: I [!DNL Amazon S3], generera ett `access key - secret access key` två för att ge plattformsåtkomst till din [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Bucket name]**: ange namnet på [!DNL Amazon S3] bucket som ska användas för detta mål.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.

Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Din offentliga nyckel måste skrivas som en [!DNL Base64] kodad sträng.

>[!TIP]
>
>I arbetsflödet för anslutningsmål kan du skapa en anpassad mapp i din Amazon S3-lagring per exporterad segmentfil. Läs [Använd makron för att skapa en mapp på lagringsplatsen](overview.md#use-macros) för instruktioner.

### Obligatoriskt [!DNL Amazon S3] behörigheter {#required-s3-permission}

Ansluta och exportera data till [!DNL Amazon S3] lagringsplats, skapa en IAM-användare (Identity and Access Management) för [!DNL Platform] in [!DNL Amazon S3] och tilldela behörigheter för följande åtgärder:

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

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

För [!DNL Amazon S3] destinationer, [!DNL Platform] skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i segmentaktiveringssjälvstudiekursen.
