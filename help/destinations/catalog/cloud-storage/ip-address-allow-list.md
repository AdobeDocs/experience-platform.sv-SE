---
title: IP-adress tillåtelselista för filbaserade molnlagringsmål
type: Documentation
description: På den här sidan finns IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till molnlagringsplatser.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: ee4c42a2298c588590b1535524ed8f3dfe13b603
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# IP-adress tillåtelselista för filbaserade molnlagringsmål {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.
> * Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Tillämplighet {#applicability}

IP-intervallinformationen på den här sidan gäller följande filbaserade molnlagringskontakter i målkatalogen:

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google Cloud Storage]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>IP-intervallen som dokumenteras på den här sidan stöds *inte* för följande filbaserade molnlagringsmål: [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2] och [!UICONTROL Data Landing Zone].

## Översikt {#overview}

På den här sidan finns IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till flera molnlagringsplatser.

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för dataöverföringstjänsten.

Adobe rekommenderar att du lägger till följande IP-intervall till en tillåtelselista innan du arbetar med molnlagringsmålanslutningar. Om du inte lägger till ditt regionspecifika IP-intervall i tillåtelselista kan det leda till fel eller prestandafel när du använder målanslutningarna för molnlagring.

## Krävs för alla kunder {#all-customers}

* `52.247.108.70`
<!-- 
## US customers running on AWS {#aws}

The IP range below applies to Experience Platform customers running on Amazon Web Services (AWS). See the [Experience Platform Multi-Cloud overview](../../../landing/multi-cloud.md) for more information.

>[!NOTE]
>
>This IP range is not supported for customers running on AWS who use file-based destinations to export data to Amazon S3. -->

* `66.117.18.0/24`

## Kunder i USA {#us-customers}

* `52.252.71.64/29`

## Kanada-kunder {#canada-customers}

* `20.220.135.16/29`

## EMEA-kunder {#emea-customers}

* `51.137.8.208/29`

## Storbritannien {#uk-customers}

* `20.26.133.96/29`

## APAC-kunder {#apac-customers}

* `20.53.201.168/29`
