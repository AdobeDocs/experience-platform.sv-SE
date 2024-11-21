---
keywords: IP-adress, IP-intervall, tillåtelselista, tillåtelselista, frågetjänst, nätverksåtkomst
title: IP-adressen Tillåtelselista för frågetjänsten
description: Den här sidan innehåller uppdaterade IP-intervall som du kan lägga till på tillåtelselista för säker åtkomst till frågetjänsten.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: ac29d10d3774a736d1e54255508ba244ff72f278
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# IP-adress tillåtelselista {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe rekommenderar att du bokmärker den här sidan och går tillbaka till den var tredje månad för att kontrollera de senaste IP-adresserna. Adobe meddelar inte om nya IP-intervall.
> * Från och med 15 oktober 2024 är bara de nya IP-intervallen giltiga för åtkomst till frågetjänsten. Inaktuella IP-adresser fungerar inte längre. Se till att ditt tillåtelselista endast innehåller de nya IP-adresserna för att undvika avbrott i tjänsten.

## Översikt {#overview}

Du kan definiera nätverksåtkomstkontroller via nätverkets brandvägg. Genom att ange rätt IP-intervall kan du tillåta trafik för åtkomst till frågetjänsten.

Som en del av de pågående förbättringarna har Adobe uppdaterat IP-intervallen för nätverksåtkomst till frågetjänsten. De tidigare IP-adresserna är nu inaktuella och endast de nya IP-adresserna är giltiga. Det är viktigt att du uppdaterar ditt tillåtelselista så att det omfattar följande nya IP-intervall för att kunna behålla tjänsten utan avbrott.

Adobe rekommenderar att du lägger till följande regionspecifika IP-intervall i en tillåtelselista beroende på din region. Om du inte lägger till dessa regionspecifika IP-intervall kan det leda till fel eller tjänstavbrott.

## VA7: Kunder i USA och Amerika {#us-americas}

**Ny IP:** 4.152.211.251

## NLD2: EMEA-kunder {#emea}

**Ny IP:** 108.141.12.47

## AUS5: APAC-kunder {#apac}

**Ny IP:** 40.82.220.111

## CAN2: Kanadensiska kunder {#can2}

**Ny IP:** 4.172.28.20

## GBR9: Kunder i Storbritannien {#gbr9}

**Ny IP:** 20.254.80.141

## Konfigurera IP-baserade begränsningar {#set-ip-restrictions}

Använd [API-guiderna för dataauktorisering](./auth-api/overview.md) för att konfigurera IP-baserade begränsningar. Dessa IP-baserade begränsningar säkerställer att endast godkända nätverk och klientdatorer har åtkomst till data via SQL i Adobe Experience Platform. Lär dig hur du konfigurerar, tillämpar och övervakar IP-begränsningar för att upprätthålla höga säkerhetsstandarder, med funktioner för åtkomstspårning i realtid och larm.

* [Guiden Komma igång](./auth-api/getting-started.md)
* [Slutpunktshandbok för IP-åtkomst](./auth-api/ip-access.md)
* [Guiden Slutpunkt för IP-validering](./auth-api/validate.md)
