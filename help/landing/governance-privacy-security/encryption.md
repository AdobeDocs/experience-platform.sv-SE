---
title: Datakryptering i Adobe Experience Platform
description: Läs om hur data krypteras under överföring och i vila i Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: fd31d54339b8d87b80799a9c0fa167cc9a07a33f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Datakryptering i Adobe Experience Platform

Adobe Experience Platform är ett kraftfullt och utbyggbart system som centraliserar och standardiserar kundupplevelsedata för alla företagslösningar. Alla data som används av Platform krypteras under överföring och i vila för att skydda dina data. I det här dokumentet beskrivs plattformens krypteringsprocesser på en hög nivå.

I följande processflödesdiagram visas hur Experience Platform importerar, krypterar och bevarar data:

![Ett diagram som illustrerar hur data importeras, krypteras och bevaras av Experience Platform.](../images/governance-privacy-security/encryption/flow.png)

## Uppgifter under transport {#in-transit}

Alla data som överförs mellan plattformen och alla externa komponenter utförs via säkra, krypterade anslutningar med HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

I allmänhet hämtas data till plattformen på tre sätt:

- [Datainsamling](../../collection/home.md) gör det möjligt för webbplatser och mobilappar att skicka data till Platform Edge Network för mellanlagring och förberedelse för förtäring.
- [Källkopplingar](../../sources/home.md) strömma data direkt till plattformen från Adobe Experience Cloud-program och andra företagsdatakällor.
- ETL-verktyg som inte är Adobe (extrahera, omforma, läsa in) skickar data till [API för gruppinmatning](../../ingestion/batch-ingestion/overview.md) för konsumtion.

När data har hämtats in i systemet och [krypterad i vila](#at-rest), plattformstjänster förbättrar och exporterar data på följande sätt:

- [Destinationer](../../destinations/home.md) gör att du kan aktivera data för Adobe-program och partnerprogram.
- Applikationer för olika plattformar som [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) och [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home) kan också använda data.

### Stöd för mTLS-protokoll {#mtls-protocol-support}

Nu kan du använda mTLS (Mutual Transport Layer Security) för att förbättra säkerheten för utgående anslutningar till HTTP API-mål och anpassade Adobe Journey Optimizer-åtgärder. mTLS är en heltäckande säkerhetsmetod för ömsesidig autentisering som ser till att båda parter delar information är de som gör anspråk på att vara innan data delas. mTLS innehåller ytterligare ett steg jämfört med TLS, där servern också frågar efter klientens certifikat och verifierar det i slutet.

#### mTLS i Adobe Journey Optimizer {#mtls-in-adobe-journey-optimizer}

I Adobe Journey Optimizer används mTLS tillsammans med [anpassade åtgärder](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). Ingen ytterligare [konfiguration för Adobe Journey Optimizer anpassade åtgärder](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) krävs från din sida för att aktivera mTLS. När slutpunkten för en anpassad åtgärd är mTLS-aktiverad hämtar systemet certifikatet från Adobe Experience Platform nyckelbehållare och skickar det automatiskt till slutpunkten (vilket krävs för mTLS-anslutningar).

Om du vill använda mTLS med dessa Adobe Journey Optimizer och Experience Platform HTTP API-målarbetsflöden måste den serveradress som du placerar i Adobe Journey Optimizer kundåtgärdsgränssnitt eller målgränssnittet ha TLS-protokoll inaktiverade och endast mTLS aktiverade. Om TLS 1.2-protokollet fortfarande är aktiverat på den slutpunkten skickas inget certifikat för klientautentisering. Det innebär att om du vill använda mTLS med dessa arbetsflöden måste den&quot;mottagande&quot; serverslutpunkten vara en mTLS **endast** aktiverad slutpunkt för anslutning.

>[!IMPORTANT]
>
>Ingen ytterligare konfiguration krävs i din anpassade Adobe Journey Optimizer-åtgärd eller -resa för att aktivera mTLS. Den här processen sker automatiskt när en mTLS-aktiverad slutpunkt identifieras. Det gemensamma namnet (CN) och SAN (Subject Alternative Names) för varje certifikat finns i dokumentationen som en del av certifikatet och kan användas som ett ytterligare lager av ägarskapsvalidering om du vill.
>
>RFC 2818, som publicerades i maj 2000, tar bort användningen av fältet Gemensamt namn (CN) i HTTPS-certifikat för verifiering av ämnesnamn. Du bör i stället använda tillägget&quot;Alternativt ämnesnamn&quot; (SAN) av typen&quot;DNS-namn&quot;.

### Hämta certifikat {#download-certificates}

Om du vill kontrollera KN eller SAN för att göra ytterligare validering från tredje part, kan ladda ned relevanta certifikat här:

- [Adobe Journey Optimizer offentliga certifikat](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [Det offentliga certifikatet för destinationstjänsten](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

## Vilande uppgifter {#at-rest}

Data som importeras och används av Platform lagras i datasjön, ett mycket detaljerat datalager som innehåller alla data som hanteras av systemet, oavsett ursprung eller filformat. Alla data som lagras i datasjön krypteras, lagras och hanteras i en isolerad [[!DNL Microsoft Azure Data Lake] Lagring](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) instans som är unik för din organisation.

Mer information om hur vilande data krypteras i Azure Data Lake Storage finns i [officiell Azure-dokumentation](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Nästa steg

Det här dokumentet innehåller en översikt på hög nivå över hur data krypteras i Platform. Mer information om säkerhetsprocedurer i Platform finns i översikten om [styrning, integritet och säkerhet](./overview.md) på Experience League, eller ta en titt på [Informationsdokument om plattformssäkerhet](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
