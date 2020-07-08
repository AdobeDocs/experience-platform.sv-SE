---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---


# Översikt över Adobe Experience Platform Privacy Servicen

För att kunna leverera bättre kundupplevelser måste ni samla in och lagra kundernas personuppgifter. När du använder dessa data är det viktigt att förstå och respektera dina kunders integritet. Nya juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran.

Adobe Experience Platform Privacy Servicen tillhandahåller ett RESTful-API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med Privacy Service kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

## Varför Privacy Service?

Privacy Servicen utvecklades som svar på en grundläggande förändring i hur företag måste hantera sina kunders personuppgifter. Det centrala syftet med Privacy Servicen är att automatisera efterlevnaden av datasekretessregler som, när de överträds, kan leda till allvarliga böter och störa datahanteringen för ert företag.

### Privacy Service och GDPR

I den [](https://eugdpr.org/)allmänna dataskyddsförordningen (GDPR) infördes flera nya rättigheter för EU-medlemmar, bland annat **rätten till åtkomst** och **rätten att raderas**. Detta innebär att alla EU-medborgare vars personuppgifter har samlats in av ert företag när som helst kan begära att få tillgång till eller radera sina uppgifter. Om dessa förfrågningar inte uppfylls inom 30 dagar kan det leda till böter på flera miljoner dollar för din organisation.

Privacy Servicen stöder förfrågningar om åtkomst och borttagning för GDPR och spårar dem separat från förfrågningar enligt CCPA-förordningen. Mer information finns i Vanliga frågor [och](gdpr/faq.md) terminologer [för](gdpr/terminology.md) GDPR.

### Privacy Service och CCPA

CCPA ( [California Consumer Privacy Act](https://www.caprivacy.org/about) ) förbättrar sekretessen och konsumentskyddet för personer bosatta i Kalifornien. CCPA ger personer bosatta i Kalifornien nya integritetsrättigheter, inklusive rätten att få tillgång till och radera sina personuppgifter, att få veta om deras personuppgifter säljs eller offentliggörs (och till vem) samt rätten att avanmäla sig från att få sina uppgifter sålda till tredje part.

Privacy Servicen stöder åtkomst- och borttagningsbegäranden för CCPA-förordningen och spårar dem separat från GDPR-begäranden. Privacy Servicen har också stöd för att skicka begäran om avanmälan för Experience Cloud som stöder dem. Mer information finns i Vanliga frågor om [CCPA](ccpa/faq.md) .

## Så här använder du Privacy Service för att hantera förfrågningar om sekretessjobb

Privacy Service innehåller ett RESTful-API och användargränssnitt som gör att du kan hantera dina kunders förfrågningar om åtkomst till/borttagning av privata data eller avanmäla dig från försäljning (kallas även **sekretessjobb**). Tjänsten har också en central mekanism för revision och loggning som gör att du kan visa status och resultat för sekretessjobb som involverar Experience Cloud-program.

>[!NOTE]
>
>Avanmälningsbegäranden stöds för närvarande bara av Privacy Services-API:t.

### Använda API

Med [Privacy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) kan du skapa och hantera sekretessjobb med RESTful API-anrop, vilket gör att du kan programmässigt hantera kompatibilitetsregler för dina Experience Cloud-program. Detaljerade anvisningar om hur du använder API:t finns i utvecklarhandboken [för](api/getting-started.md)Privacy Service API.

### Använda gränssnittet

Med Privacy Servicens användargränssnitt kan du skapa och övervaka sekretessjobb med ett grafiskt gränssnitt. Användargränssnittet innehåller en **statusrapportwidget** som ger en visuell representation av statusen för alla aktiva begäranden, och som gör att du kan skapa nya begäranden med hjälp av den inbyggda **Request Builder** eller genom att överföra JSON-filer. Mer information om hur du använder användargränssnittet finns i användarhandboken för [Privacy Service](ui/overview.md).