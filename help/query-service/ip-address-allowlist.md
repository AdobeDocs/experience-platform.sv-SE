---
keywords: IP-adress, IP-intervall, tillåtelselista, tillåtelselista, frågetjänst, nätverksåtkomst
title: IP-adressen Tillåtelselista för frågetjänsten
description: Den här sidan innehåller uppdaterade IP-intervall som du kan lägga till på tillåtelselista för säker åtkomst till frågetjänsten.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 029d0ad63460a71770e5ba3cd75a29cb04c0cb9c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# IP-adress tillåtelselista {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.
> * Adobe stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].
> * Från 15 oktober 2024 har nya IP-intervall ersatt de befintliga. Se till att både gamla och nya IP-adresser läggs till i tillåtelselista före detta datum för att undvika avbrott i tjänsten.

## Översikt {#overview}

Den här sidan innehåller IP-adresser som du kan lägga till på tillåtelselista för att på ett säkert sätt exportera data från Experience Platform till din [SFTP-server](../destinations/catalog/cloud-storage/sftp.md).

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för dataöverföringstjänsten.

Som en del av de pågående förbättringarna har Adobe uppdaterat IP-intervallen som används för nätverksåtkomst till frågetjänsten den 15 oktober 2024. De befintliga IP-adresserna kommer att bli inaktuella och nya IP-adresser kommer att ersätta dem. Det är viktigt att lägga till både det gamla och nya IP-intervallet på tillåtelselista under övergångsperioden för att säkerställa oavbruten service.

Adobe rekommenderar att du lägger till följande regionspecifika IP-intervall i en tillåtelselista beroende på din region. Om du inte lägger till dina regionspecifika IP-intervall i tillåtelselista kan det leda till fel eller sämre prestanda.

## VA7: Kunder i USA och Amerika {#us-americas}

**Gammal IP:** 20.14.241.153\
**Ny IP:** 4.152.211.251

## NLD2: EMEA-kunder {#emea}

**Gammal IP:** 20.101.233.128\
**Ny IP:** 108.141.12.47

## AUS5: APAC-kunder {#apac}

**Gammal IP:** 20.248.220.69\
**Ny IP:** 40.82.220.111

## CAN2: Kanadensiska kunder {#can2}

**Gammal IP:** 4.172.1.139\
**Ny IP:** 4.172.28.20

## GBR9: Kunder i Storbritannien {#gbr9}

**Gammal IP:** 20.108.200.9\
**Ny IP:** 20.254.80.141

