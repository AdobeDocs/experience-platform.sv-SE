---
title: Datakryptering i Adobe Experience Platform
description: Läs om hur data krypteras under överföring och i vila i Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Datakryptering i Adobe Experience Platform

Adobe Experience Platform är ett kraftfullt och utbyggbart system som centraliserar och standardiserar kundupplevelsedata för alla företagslösningar. Alla data som används av Experience Platform krypteras under överföring och i vila för att skydda dina data. I det här dokumentet beskrivs Experience Platform krypteringsprocesser på en hög nivå.

Följande processflödesdiagram visar hur Experience Platform importerar, krypterar och bevarar data:

![Ett diagram som illustrerar hur data importeras, krypteras och bevaras av Experience Platform.](../images/governance-privacy-security/encryption/flow.png)

## Uppgifter under transport {#in-transit}

Alla data som överförs mellan Experience Platform och alla externa komponenter utförs över säkra, krypterade anslutningar med HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

I allmänhet hämtas data till Experience Platform på tre sätt:

- [Funktionerna för datainsamling](../../collection/home.md) gör att webbplatser och mobilprogram kan skicka data till Experience Platform Edge Network för mellanlagring och förberedelse för förtäring.
- [Source kopplar](../../sources/home.md) strömma data direkt till Experience Platform från Adobe Experience Cloud-program och andra företagsdatakällor.
- Icke-Adobe ETL-verktyg (extrahera, omforma, läsa in) skickar data till [API:t för gruppinläsning](../../ingestion/batch-ingestion/overview.md) för konsumtion.

När data har hämtats till systemet och [krypterats i viloläge](#at-rest) förbättrar och exporterar Experience Platform-tjänster data på följande sätt:

- Med [Destinationer](../../destinations/home.md) kan du aktivera data för Adobe-program och partnerprogram.
- Inbyggda Experience Platform-program som [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=sv-SE) och [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/ajo-home) kan också använda data.

### Stöd för mTLS-protokoll {#mtls-protocol-support}

Nu kan du använda mTLS (Mutual Transport Layer Security) för att förbättra säkerheten i utgående anslutningar till [HTTP API-målet](../../destinations/catalog/streaming/http-destination.md) och Adobe Journey Optimizer [anpassade åtgärder](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). mTLS är en heltäckande säkerhetsmetod för ömsesidig autentisering som ser till att båda parter delar information är de som gör anspråk på att vara innan data delas. mTLS innehåller ytterligare ett steg jämfört med TLS, där servern också frågar efter klientens certifikat och verifierar det i slutet.

Om du vill [använda mTLS med Adobe Journey Optimizer anpassade åtgärder](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) och Experience Platform HTTP API-målarbetsflöden, måste den serveradress som du anger i Adobe Journey Optimizer kundåtgärdsgränssnitt eller målgränssnittet ha TLS-protokoll inaktiverade och endast mTLS aktiverade. Om TLS 1.2-protokollet fortfarande är aktiverat på den slutpunkten skickas inget certifikat för klientautentisering. Det innebär att om du vill använda mTLS med de här arbetsflödena måste den &quot;mottagande&quot; serverslutpunkten vara en mTLS **only** -aktiverad anslutningsslutpunkt.

>[!IMPORTANT]
>
>Ingen ytterligare konfiguration krävs i din anpassade Adobe Journey Optimizer-åtgärd eller i HTTP API-målet för att aktivera mTLS. Den här processen sker automatiskt när en mTLS-aktiverad slutpunkt identifieras. Det gemensamma namnet (CN) och SAN (Subject Alternative Names) för varje certifikat finns i dokumentationen som en del av certifikatet och kan användas som ett ytterligare lager av ägarskapsvalidering om du vill.
>
>RFC 2818, som publicerades i maj 2000, tar bort användningen av fältet Gemensamt namn (CN) i HTTPS-certifikat för verifiering av ämnesnamn. Du bör i stället använda tillägget&quot;Alternativt ämnesnamn&quot; (SAN) av typen&quot;DNS-namn&quot;.

### Hämta certifikat {#download-certificates}

>[!NOTE]
>
>Du ansvarar för att se till att dina system använder ett giltigt offentligt certifikat. Granska dina certifikat regelbundet, särskilt när utgångsdatumet närmar sig. Använd API för att hämta och uppdatera certifikat innan de upphör att gälla.

Direktnedladdningslänkar för offentliga mTLS-certifikat tillhandahålls inte längre. Använd i stället [slutpunkten för det offentliga certifikatet](../../data-governance/mtls-api/public-certificate-endpoint.md) för att hämta certifikat. Det här är den enda metod som stöds för att komma åt aktuella offentliga certifikat. Det ser till att du alltid får giltiga, aktuella certifikat för dina integreringar.

Integrationer som förlitar sig på certifikatbaserad kryptering måste uppdatera sina arbetsflöden för att stödja automatisk certifikathämtning med API:t. Om du förlitar dig på statiska länkar eller manuella uppdateringar kan det leda till att certifikat som har upphört att gälla eller har återkallats används, vilket leder till misslyckade integreringar.

#### Automatisering av certifikatets livscykel {#certificate-lifecycle-automation}

Adobe automatiserar nu certifikatets livscykel för mTLS-integreringar för att förbättra tillförlitligheten och förhindra avbrott i tjänsten. Offentliga certifikat:

- Återutfärdad 60 dagar före utgångsdatum.
- Återkallad 30 dagar innan utgångsdatum.

Dessa intervall kommer att fortsätta förkortas i enlighet med [kommande riktlinjer för CA/B-forum](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days) som syftar till att minska certifikatets livstid till högst 47 dagar.

Om du tidigare har använt länkar på den här sidan för att hämta certifikat uppdaterar du processen så att de hämtas exklusivt via API:t.

## Vilande uppgifter {#at-rest}

Data som importeras och används av Experience Platform lagras i datasjön, ett mycket detaljerat datalager som innehåller alla data som hanteras av systemet, oavsett ursprung eller filformat. Alla data som lagras i datasjön krypteras, lagras och hanteras i en isolerad [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) -instans som är unik för din organisation.

Mer information om hur vilande data krypteras i Azure Data Lake Storage finns i den [officiella Azure-dokumentationen](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Nästa steg

Det här dokumentet innehåller en översikt över hur data krypteras i Experience Platform. Mer information om säkerhetsprocedurer i Experience Platform finns i översikten om [styrning, sekretess och säkerhet](./overview.md) på Experience League, eller i [Experience Platform säkerhetsrapport](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
