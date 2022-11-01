---
keywords: molnlagringsmål;molnlagring
title: Översikt över destinationer för molnlagring
description: Adobe Experience Platform kan leverera dina segment som datafiler till dina Amazon S3-, AWS Kinesis-, Azure Event Hubs- eller SFTP-molnlagringsplatser.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 4a4c82cc4528fe07bbdb75ae9f795bdbab48c089
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Översikt över destinationer för molnlagring {#cloud-storage-destinations}

## Översikt {#overview}

Adobe Experience Platform kan leverera dina segment som datafiler till dina molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV-filer för [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage]och SFTP. För [!DNL Amazon Kinesis] och [!DNL Azure Event Hubs] mål, data direktuppspelas från Experience Platform in [!DNL JSON] format.

![Adobe molnlagringsdestinationer](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Molnlagringsmål som stöds {#supported-destinations}

Adobe Experience Platform stöder följande molnlagringsmål:

* [Amazon Kinesis-anslutning](amazon-kinesis.md)
* [Amazon S3-anslutning](amazon-s3.md)
* [Azure Blob-anslutning](azure-blob.md)
* [(Beta) Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure Event Hubs-anslutning](azure-event-hubs.md)
* [(Beta) Data Landing Zone](data-landing-zone.md)
* [(Beta) Google Cloud-lagring](google-cloud-storage.md)
* [SFTP-anslutning](sftp.md)

## Ansluta till ett nytt molnlagringsmål {#connect-destination}

Om du vill skicka segment till molnlagringsmål för dina kampanjer måste plattformen först ansluta till målet. Se [självstudiekurs om att skapa mål](../../ui/connect-destination.md) för detaljerad information om hur du konfigurerar ett nytt mål.


## Använd makron för att skapa en mapp på lagringsplatsen {#use-macros}

>[!NOTE]
>
> Funktionerna som beskrivs i det här avsnittet är för närvarande tillgängliga för [Amazon S3](amazon-s3.md) endast destinationer.

Om du vill skapa en anpassad mapp per segmentfil på lagringsplatsen kan du använda makron i mappsökvägsfältet. Infoga makrona i slutet av inmatningsfältet, vilket visas nedan.

![Så här använder du makron för att skapa en mapp i ditt lagringsutrymme](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Exemplen nedan refererar till ett exempelsegment `Luxury Audience` med ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Makro 1:`%SEGMENT_NAME%`**

Indata: `acme/campaigns/2021/%SEGMENT_NAME%`
Mappsökväg i lagringsplatsen: `acme/campaigns/2021/Luxury Audience`

**Makro 2:`%SEGMENT_ID%`**

Indata: `acme/campaigns/2021/%SEGMENT_ID%`
Mappsökväg i lagringsplatsen: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Makro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Indata: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Mappsökväg i lagringsplatsen: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Dataexporttyp {#export-type}

Stöd för molnlagringsdestinationer **Profilbaserad export**. Det innebär att du exporterar information om personerna i målgruppen. Den här informationen behövs för personalisering och kan innehålla attribut, händelser, segmentmedlemskap med mera.