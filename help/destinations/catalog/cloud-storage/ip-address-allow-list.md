---
keywords: IP-adress, IP-intervall, tillåtelselista-mål
title: 'IP-adress tillåtelselista för molnlagringsmål '
type: Dokumentation
description: Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till din SFTP-server, Amazon S3 eller Azure Blob-lagring.
translation-type: tm+mt
source-git-commit: 648be489aa77870f67564ee350c4d85885673832
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# IP-adress tillåtelselista för molnlagringsmål {#ip-address-allow-list}

>[!IMPORTANT]
>
> Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.

Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till din [SFTP-server](./sftp.md), [Amazon S3](./amazon-s3.md) eller [Azure Blob](./azure-blob.md)-lagring.

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för dataöverföringstjänsten.

Du kan lägga till följande IP-intervall till en tillåtelselista innan du arbetar med målanslutningar för molnlagring. Om du inte lägger till ditt regionspecifika IP-intervall i tillåtelselista kan det leda till fel eller sämre prestanda när du använder målanslutningarna för molnlagring.

## Kunder i USA

* `52.252.71.64/29`

## EMEA-kunder

* `51.137.8.208/29`

## APAC-kunder

* `20.53.201.168/29`