---
title: API-guide för dataauktorisering i Distiller
description: Lär dig hur du använder API:t för dataauktorisering i Distiller för att framtvinga nätverksbaserade IP-begränsningar för säkra anslutningar via SQL. Använd detta API för att förbättra dataåtkomstkontrollen för dina Adobe Experience Platform-data.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---

# API-guide för dataauktorisering i Distiller

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Data Distiller-tillägget. Kontakta din Adobe-representant om du vill veta mer.

Använd Data Distiller Authorization API för att tillämpa IP-baserade begränsningar. Genom att tillämpa dessa åtgärder kan endast godkända nätverk och klientdatorer få åtkomst till data via SQL i Adobe Experience Platform. Dessa kontroller hjälper er att uppfylla strikta säkerhetsstandarder och samtidigt tillhandahålla åtkomstövervakning och larm i realtid.

Med detta API kan du konfigurera, tillämpa och övervaka IP-begränsningar för åtkomst av data via SQL-gränssnittet. Det här dokumentet innehåller en översikt på hög nivå över API:ts kärnfunktioner, slutpunktsfunktioner och framtida funktioner.

## Viktiga funktioner

Följande funktioner gör att du kan definiera IP-baserade åtkomstbegränsningar, övervaka åtkomstförsök och anpassa säkerhetsinställningar för nätverket för Query Service:

- **Definiera nätverksbaserade dataåtkomstkontroller**: Ange tillåtna IP-intervall för åtkomst till frågetjänsten. Den här begränsningen gäller specifikt för SQL-databasanslutningar, inklusive sådana som har gjorts via Business Intelligence (BI)-verktyg, databasklienter eller programmeringsgränssnitt som JDBC.
- **Aktivera omfattande övervakning och aviseringar**: Alla åtkomstförsök, inklusive nekade anslutningar, loggas och skickas till [Adobe Experience Platform granskningsloggar](../../landing/governance-privacy-security/audit-logs/overview.md) för realtidsspårning. Använd den här funktionen för att övervaka åtkomstmönster och upptäcka potentiella säkerhetsintrång.
- **Konfigurera flexibla IP-begränsningar**: Ange tillåtna IP-adresser i både enskilda IP- och CIDR-blockformat. Dessa inställningar gäller för varje sandlåda, vilket gör att du kan anpassa nätverksbegränsningar efter dina specifika säkerhetsbehov.

## Gransknings- och övervakningsfunktioner

För att ge stöd åt säkra dataåtkomstrutiner loggar Query Service alla klient-IP:n som har åtkomst till eller försöker få åtkomst till Experience Platform. Granskningshändelser, inklusive nekade anslutningar, skickas till Experience Platform granskningsloggar. Detta gör att:

- **Realtidsövervakning**: Spåra IP-baserade åtkomstmönster för att säkerställa regelefterlevnad.
- **Varning vid obehörig åtkomst**: Identifiera och svara på åtkomstförsök från obehöriga IP-adresser.

Mer information finns i [Översikt över granskningsloggar](../../landing/governance-privacy-security/audit-logs/overview.md).

## Nästa steg

Kom igång med Data Distiller Authorization API genom att läsa [Komma igång-guiden](./getting-started.md) för viktiga konfigurationssteg, inklusive obligatoriska huvuden och API-anropskonventioner. Utforska sedan de slutpunktsspecifika guiderna för [IP-åtkomst](./ip-access.md) och [IP-validering](./validate.md) för att konfigurera och hantera säker dataåtkomst.

Se [Data Distiller Authorization OpenAPI-referensdokumentation](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) om du vill visa ett standardiserat, maskinläsbart format för enklare integrering, testning och utforskning.

Mer information om de olika svarsparametrarna för varje returnerad datauppsättning finns i [API-utvecklardokumentationen för datauppsättningar](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).
