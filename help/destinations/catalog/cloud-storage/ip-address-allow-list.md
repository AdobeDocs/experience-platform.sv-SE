---
title: TILLÅTELSELISTA SFTP-mål för IP-adress
type: Documentation
description: Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till SFTP-servern.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 3d870975593313062d796601f0e19a0a3aec7854
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# IP-adress tillåtelselista för SFTP-mål {#ip-address-allow-list-sftp}

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
