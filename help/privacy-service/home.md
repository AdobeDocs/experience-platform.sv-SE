---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Integritetstjänst för Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364

---


# Adobe Experience Platform - översikt över sekretessgraden

För att kunna leverera bättre kundupplevelser måste ni samla in och lagra kundernas personuppgifter. När du använder dessa data är det viktigt att förstå och respektera dina kunders integritet. Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran.

Integritetstjänsten för Adobe Experience Platform tillhandahåller ett RESTful API och användargränssnitt som hjälper er att hantera dessa dataförfrågningar från era kunder. Med Integritetstjänsten kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

## Varför Integritetstjänst?

Integritetstjänsten utvecklades som svar på en grundläggande förändring i hur företag måste hantera sina kunders personuppgifter. Det centrala syftet med integritetstjänsten är att automatisera efterlevnaden av datasekretessregler som, när de överträds, kan leda till allvarliga böter och störa datahanteringen för ert företag.

### Integritetstjänst och GDPR

I den [allmänna dataskyddsförordningen](https://eugdpr.org/) (GDPR) infördes flera nya integritetsrättigheter för EU-medlemmar, bland annat **rätten till tillgång** och **rätten att bli glömd**. Detta innebär att alla EU-medborgare vars personuppgifter har samlats in av ert företag när som helst kan begära att få tillgång till eller radera sina uppgifter. Om dessa förfrågningar inte uppfylls inom 30 dagar kan det leda till böter på flera miljoner dollar för din organisation.

Integritetstjänsten stöder förfrågningar om åtkomst och radering för GDPR och spårar dem separat från förfrågningar enligt CCPA-förordningen. Mer information finns i Vanliga frågor [och](gdpr/faq.md) terminologer [för](gdpr/terminology.md) GDPR.

### Integritetstjänst och CCPA

CCPA ( [California Consumer Privacy Act](https://www.caprivacy.org/about) ) förbättrar sekretessen och konsumentskyddet för personer bosatta i Kalifornien. CCPA ger personer bosatta i Kalifornien nya integritetsrättigheter, inklusive rätten att få tillgång till och radera sina personuppgifter, att få veta om deras personuppgifter säljs eller offentliggörs (och till vem) samt rätten att avanmäla sig från att få sina uppgifter sålda till tredje part.

Integritetstjänsten stöder förfrågningar om åtkomst och radering av CCPA-förordningen och spårar dem separat från GDPR-förfrågningar. Integritetstjänsten har också stöd för att skicka begäran om att avanmäla dig från försäljning för Experience Cloud-program som stöder dem. Mer information finns i Vanliga frågor om [CCPA](ccpa/faq.md) .

## Hur man hanterar förfrågningar om sekretessjobb med Integritetstjänst

Integritetstjänsten innehåller ett RESTful-API och användargränssnitt som gör att du kan hantera dina kunders förfrågningar om åtkomst till/borttagning av privata data eller avanmäla dig från försäljning (kallas även **sekretessjobb**). Tjänsten tillhandahåller också en central gransknings- och loggningsmekanism som gör att du kan visa status och resultat för sekretessjobb som innefattar Experience Cloud-program.

>[!NOTE] Avanmälningsbegäranden stöds för närvarande bara av sekretesstjänstens API.

### Använda API

Med API:t [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) sekretesstjänsten kan du skapa och hantera sekretessjobb med RESTful API-anrop, vilket gör att du kan programmässigt hantera kompatibilitetsregler för dina Experience Cloud-program. Detaljerade anvisningar om hur du använder API:t finns i utvecklarhandboken [för API:t för](api/getting-started.md)sekretesstjänster.

### Använda gränssnittet

Med sekretessgränssnittet kan du skapa och övervaka sekretessjobb med ett grafiskt gränssnitt. Användargränssnittet innehåller en **statusrapportwidget** som ger en visuell representation av statusen för alla aktiva begäranden, och som gör att du kan skapa nya begäranden med hjälp av den inbyggda **Request Builder** eller genom att överföra JSON-filer. Mer information om hur du använder användargränssnittet finns i användarhandboken [för](ui/overview.md)sekretesstjänsten.