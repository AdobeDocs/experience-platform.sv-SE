---
title: IP-adress tillåtelselista för filbaserade molnlagringsmål
type: Documentation
description: På den här sidan finns IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till molnlagringsplatser.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 7cf15550d7619e247052efc4d9b4c72c5d32641a
workflow-type: tm+mt
source-wordcount: '284'
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

## Kunder i USA som kör på AWS {#aws}

IP-intervallet nedan gäller för Experience Platform-kunder som använder Amazon Web Services (AWS). Mer information finns i [Experience Platform Multi-Cloud-översikt](../../../landing/multi-cloud.md).

>[!NOTE]
>
>Det här IP-intervallet stöds inte för kunder som använder filbaserade destinationer i AWS för att exportera data till Amazon S3.

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
