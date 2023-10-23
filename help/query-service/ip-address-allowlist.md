---
keywords: IP-adress, IP-intervall, tillåtelselista, tillåtelselista
title: IP-adressen Tillåtelselista för frågetjänsten
description: Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista.
source-git-commit: 89d04a98e983b5dc9f353a831cdbe21c7c7aaf36
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# IP-adress tillåtelselista {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.
> * Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Översikt {#overview}

Den här sidan innehåller IP-adresser som du kan lägga till i tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till [SFTP-server](../destinations/catalog/cloud-storage/sftp.md).

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för dataöverföringstjänsten.

Adobe rekommenderar att du lägger till följande IP-intervall i en tillåtelselista beroende på din region. Om du inte lägger till ditt regionspecifika IP-intervall i tillåtelselista kan det leda till fel eller sämre prestanda.

## VA7: Kunder i USA och Amerika {#us-americas}

* 52.138.119.167

## NLD2: EMEA-kunder {#emea}

* 51.124.70.4

## AUS5: APAC-kunder {#apac}

* 20.193.36.37

## CAN2: Kanadensiska kunder {#can2}

* 20.104.5.248
