---
keywords: IP-adress, IP-intervall, tillåtelselista, tillåtelselista
title: IP-adressen Tillåtelselista för frågetjänsten
description: Den här sidan innehåller IP-intervall som du kan lägga till i tillåtelselista.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 3a00f98b7463f7fb35aa53f703d67193f18400cf
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# IP-adress tillåtelselista {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.
> * Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Översikt {#overview}

Den här sidan innehåller IP-adresser som du kan lägga till på tillåtelselista för att exportera data från Experience Platform till [SFTP-servern](../destinations/catalog/cloud-storage/sftp.md) på ett säkert sätt.

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för dataöverföringstjänsten.

Adobe rekommenderar att du lägger till följande IP-intervall i en tillåtelselista beroende på din region. Om du inte lägger till ditt regionspecifika IP-intervall i tillåtelselista kan det leda till fel eller sämre prestanda.

## VA7: Kunder i USA och Amerika {#us-americas}

* 20.14.241.153

## NLD2: EMEA-kunder {#emea}

* 20.101.233.128

## AUS5: APAC-kunder {#apac}

* 20.248.220.69

## CAN2: Kanadensiska kunder {#can2}

* 4.172.1.139

## GBR9: United Kingdon-kunder {#gbr9}

* 20.108.200.9

