---
keywords: IP-adress, IP-intervall, tillåtelselista destinationer, tillåtelselista
title: IP-adress tillåtelselista för molnlagringsmål
type: Documentation
description: Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till din SFTP-server, Amazon S3 eller Azure Blob-lagring.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# IP-adress tillåtelselista för molnlagringsmål {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.
> * Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].


## Översikt {#overview}

Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till [SFTP-server](./sftp.md).

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för dataöverföringstjänsten.

Adobe rekommenderar att du lägger till följande IP-intervall till en tillåtelselista innan du arbetar med molnlagringsmålanslutningar. Om du inte lägger till ditt regionspecifika IP-intervall i tillåtelselista kan det leda till fel eller prestandafel när du använder målanslutningarna för molnlagring.

## Krävs för alla kunder

* `52.247.108.70`

## Kunder i USA

* `52.252.71.64/29`

## EMEA-kunder

* `51.137.8.208/29`

## APAC-kunder

* `20.53.201.168/29`
