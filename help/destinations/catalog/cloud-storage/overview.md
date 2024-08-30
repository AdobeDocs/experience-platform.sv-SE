---
keywords: molnlagringsmål;molnlagring
title: Översikt över destinationer för molnlagring
description: Adobe Experience Platform kan leverera dina målgrupper som datafiler till dina lagringsplatser i Amazon S3, AWS Kinesis, Azure Event Hubs eller SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 9c1699471d5b3c3c725e46581e256a0c07f08a49
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Översikt över destinationer för molnlagring {#cloud-storage-destinations}

## Översikt {#overview}

Adobe Experience Platform kan leverera era målgrupper som datafiler till era molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV-filer för [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] och SFTP. För [!DNL Amazon Kinesis]- och [!DNL Azure Event Hubs]-mål direktuppspelas data från Experience Platform i [!DNL JSON]-format.

![Adobe molnlagringsmål](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Molnlagringsmål som stöds {#supported-destinations}

Adobe Experience Platform stöder dataexport till följande molnlagringsmål:

* [Amazon Kinesis-anslutning](amazon-kinesis.md)
* [Amazon S3-anslutning](amazon-s3.md)
* [Azure Blob-anslutning](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure Event Hubs-anslutning](azure-event-hubs.md)
* [Datallandningszon](data-landing-zone.md)
* [Google Cloud-lagring](google-cloud-storage.md)
* [SFTP-anslutning](sftp.md)

## Ansluta till ett nytt molnlagringsmål {#connect-destination}

För att kunna skicka målgrupper till molnlagringsmål för era kampanjer måste plattformen först ansluta till destinationen. Se självstudiekursen [för att skapa mål](../../ui/connect-destination.md) för mer information om hur du konfigurerar ett nytt mål.


## Använd makron för att skapa en mapp på lagringsplatsen {#use-macros}

>[!NOTE]
>
> Funktionen som beskrivs i det här avsnittet är för närvarande endast tillgänglig för [Amazon S3](amazon-s3.md) -mål.

Om du vill skapa en anpassad mapp per målgruppsfil på din lagringsplats kan du använda makron i mappsökvägsindatafältet. Infoga makrona i slutet av inmatningsfältet, vilket visas nedan.

![Använda makron för att skapa en mapp i ditt lagringsutrymme](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Exemplen nedan refererar till en exempelmålgrupp `Luxury Audience` med ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Makro 1:`%SEGMENT_NAME%`**

Indata: `acme/campaigns/2021/%SEGMENT_NAME%`
Mappsökväg på lagringsplatsen: `acme/campaigns/2021/Luxury Audience`

**Makro 2:`%SEGMENT_ID%`**

Indata: `acme/campaigns/2021/%SEGMENT_ID%`
Mappsökväg på lagringsplatsen: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Makro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Indata: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Mappsökväg på lagringsplatsen: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**Fler makron**

På samma sätt som i exemplen ovan kan du använda ytterligare makron för att skapa en anpassad mappstruktur på mapplatsen:

* `%DATETIME%` eller `%TIMESTAMP%` om du vill lägga till ett anpassat mappnamn baserat på filernas exporttid. Formatet för det första makrot är `MMDDYYYY_HHMMSS` och ett UNIX 10-siffrigt format för det andra makrot.
* `%DESTINATION_NAME%` om du vill lägga till en anpassad mapp baserat på namnet på måldataflödet.

## Dataexporttyp {#export-type}

Molnlagringsdestinationer har stöd för följande exporttyper:
* **Profilbaserad export**. Det innebär att du exporterar information om personerna i målgruppen. Dessa uppgifter behövs för personalisering och kan omfatta attribut, event, medlemskap för målgrupper med mera.
* **Datauppsättningsexport**. Med den här funktionen kan du exportera hela datauppsättningar till molnlagringsmål. [Läs mer](/help/destinations/ui/export-datasets.md) om funktionerna.

## Nästa steg {#next-steps}

När du har valt vilket av de [molnmål som stöds](#supported-destinations) som du vill använda läser du självstudiekursen [Ansluta till mål](/help/destinations/ui/connect-destination.md) för att lära dig hur du upprättar en anslutning till målet. Läs sedan självstudiekursen om aktivering för filbaserade mål för att lära dig hur du börjar [exportera](/help/destinations/ui/activate-batch-profile-destinations.md) data till molnlagringsmålet.
