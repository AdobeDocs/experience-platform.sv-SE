---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmentmatchning;segmentmatchning
solution: Experience Platform
title: Vanliga frågor om segmentmatchning (beta)
description: Segmentmatchning är en segmentdelningstjänst i Adobe Experience Platform som gör det möjligt för två eller flera plattformsanvändare att utbyta segmentdata på ett säkert, styrt och sekretessvänligt sätt.
source-git-commit: 81ef2030ff26d2aee146316fcdab41d9311e84c7
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# [!DNL Segment Match] Frågor och svar (beta)

>[!IMPORTANT]
>
>Segmentmatchning är för närvarande en betaversion och din organisation har kanske inte åtkomst till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

Den här guiden ger svar på frågor om sekretess och juridik som ofta ställs om Adobe Experience Platform Segment Match.

## Vilka data delas vid uppskattningen och hur kan Adobe säkerställa att dessa data hämtas på ett säkert sätt?

![overlap-report.png](./images/overlap-report.png)

Inga kund- eller segmentdata flyttas över sandlådor för att få fram dessa uppskattningar av överlappning. De på förhand valda användbara identiteterna som kunden valt i en viss sandlåda läggs till i en sannolik datastruktur där själva ID:n representeras i ett hash-format.

Detta är en envägsprocess, vilket innebär att de ursprungliga förhasrade identifierarna inte visas och inte kan bakåtkompileras.

Dessa datastrukturer har unika egenskaper som gör det möjligt för ingenjörer att utföra union- och skärningsåtgärder mellan dem, även om den kodade informationen är kraftigt komprimerad eller hash-kodad. Dessa åtgärder tillåter [!DNL Segment Match] för att få den uppskattade skärningspunkten mellan två datastrukturer som består av ID:n från två olika sandlådor utan att behöva jämföra de faktiska värdena. Sedan [!DNL Segment Match] endast använder datastrukturerna, lämnar ID:n aldrig sina respektive IMS-organisationers profillager för uppskattningsändamål. På så sätt kan Adobe uppfylla kundernas sekretess- och säkerhetskrav och samtidigt erbjuda mycket exakta beräkningsverktyg som vägleder datasamarbetsavtalen.

## Hur ser det ut när du anger vilka identiteter som ska ta emot ID:n för det delade segmentet?

[!DNL Segment Match] ger kunderna ett alternativ för att konfigurera vilka namnutrymmen som ska användas i tjänsten. Detta val används både för den uppskattningsprocess som beskrivs i föregående fråga och dataöverföringsprocessen, om kunden skulle besluta att publicera flödet till en partnersandlåda.

Dataöverföringsprocessen mellan de krypterade identiteterna i två olika organisationer utförs i en neutral datormiljö. Dataöverföringsjobbet ägs av Adobe, och de organisationer som deltar i partnerskapet har inte tillgång till den här miljön och de får inte heller tillgång till några loggar som kan vara ett resultat av dataöverföringsjobbet.

Det enda segmentmedlemskapet är inkapslat i IMS-organisationens överlappande profilfragment för en mottagare och ingen ytterligare identitet överförs från den avsändande IMS-organisationen till den mottagande IMS-organisationen. Ingen vanlig text, personligt identifierbar information (PII) läses av dataöverföringsjobbet eftersom [!DNL Segment Match] tillåter endast överlappningar på SHA256-krypterade namnutrymmen (e-post/telefon) när data är PII. Resultaten lagras aldrig i datormiljön.