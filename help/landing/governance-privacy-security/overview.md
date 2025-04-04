---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Styrning, sekretess och säkerhetsöversikt
description: Adobe Experience Platform tillhandahåller flera tjänster och verktyg som gör att du kan kontrollera dina insamlade upplevelsedata på ett säkert sätt för att följa din affärspraxis, juridiska skyldigheter och utvecklingsprocess.
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Styrning, integritet och säkerhet i Adobe Experience Platform

Med Adobe Experience Platform kan ni importera, analysera, optimera och agera utifrån era data för att förbättra kundupplevelserna avsevärt. Dessa data är enorma, komplexa och oerhört värdefulla. Beroende på vilken typ av databehandling ni bedriver, vilka juridiska behörigheter ert företag tillämpar och era organisationsprofiler när det gäller dataanvändning måste ni noga kontrollera och övervaka insamlingen och användningen av kundupplevelsedata för att skydda era affärsintressen.

Experience Platform tillhandahåller flera tjänster och verktyg som gör att ni kan kontrollera era insamlade upplevelsedata på ett säkert sätt för att följa era affärspraxis, juridiska skyldigheter och utvecklingsprocesser. I avsnitten nedan ges en introduktion till var och en av dessa tjänster tillsammans med länkar till dokumentation för ytterligare information.

Tjänsterna kan kategoriseras i tre domäner:

* [Dataförvaltning](#governance)
* [Sekretess](#privacy)
* [Säkerhet](#security)

## Dataförvaltning {#governance}

Datastyrning är ett viktigt koncept som är sammankopplat med alla funktioner i Experience Platform. Datastyrning innebär att ni kan kontrollera och förstå data under hela resan genom Experience Platform. Detta innebär att upprätthålla datakvalitet, datalinje, datakatalogisering med mera.

### Adobe Experience Platform datastyrning {#data-governance}

Som Experience Platform-tjänst kan ni med Adobe Experience Platform Data Governance hantera kunddata och säkerställa att ni följer gällande regler, begränsningar och policyer för dataanvändning. Det spelar en nyckelroll inom Experience Platform på olika nivåer, bland annat i fråga om dataanvändningsetiketter, dataanvändningspolicyer, policystyrning och datalänkning.

Mer information finns i [Översikt över datastyrning](../../data-governance/home.md).

### Katalog och datauppsättningar {#catalog}

Katalogtjänsten är arkivsystemet för dataplatser och -länkar inom Experience Platform. Alla data som importeras till Experience Platform lagras i Data Lake som filer och kataloger, men i Catalog finns metadata och beskrivning för dessa filer och kataloger för sökning och övervakning.

Katalogen organiserar inkapslade data i datauppsättningar, där varje datauppsättning innehåller metadata som kan användas för att etikettera och kategorisera data som den innehåller.

Mer information om tjänsten finns i [Katalogtjänstöversikt](../../catalog/home.md). Mer information om hur du hanterar datauppsättningar i Experience Platform finns i [översikten över datauppsättningar](../../catalog/datasets/overview.md).

## Sekretess {#privacy}

Sekretess är ett kritiskt problem för ert företag, era beslutsfattare och era kunder. Eftersom personuppgifter som samlas in från era kunder är centrala i nästan alla Experience Platform arbetsflöden erbjuder Experience Platform tjänster som stöder dessa initiativ.

### Adobe Experience Platform Privacy Service {#privacy-service}

Juridiska sekretessbestämmelser som EU:s allmänna dataskyddsförordning (GDPR) och Kaliforniens konsumentintegritetslag (CCPA) ger medborgare inom deras jurisdiktion rätt att få tillgång till och ta bort de personuppgifter som du samlar in och lagrar från dem.

Adobe Experience Platform Privacy Service tillhandahåller ett RESTful-API och användargränssnitt för att hantera dessa förfrågningar. Med Privacy Service kan ni skicka in förfrågningar om åtkomst till eller radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

Mer information finns i [Privacy Service-översikten](../../privacy-service/home.md).

### Samtyckesbearbetning {#consent}

Många juridiska sekretessbestämmelser har infört krav på aktivt och specifikt samtycke när det gäller datainsamling, personalisering och andra användningsfall inom marknadsföring. För att uppfylla dessa krav kan Experience Platform inhämta information om samtycke i enskilda kundprofiler och använda dessa inställningar som en avgörande faktor i hur varje kunds data används i Experience Platform-arbetsflöden längre fram i kedjan.

Mer information om hur du bearbetar kundens samtycke och inställningsdata med Adobe-standarden finns i översikten om [godkännandebearbetning i Experience Platform](./consent/adobe/overview.md).

Mer information om hur du bearbetar kundmedgivandedata i enlighet med IAB Transparency and Consent Framework (TCF) 2.0 finns i översikten om [IAB TCF 2.0-stöd i Experience Platform](./consent/iab/overview.md).

## Säkerhet {#security}

Integriteten och säkerheten hos era data är oundgänglig för ert företag, och denna risk kräver branschledande säkerhetsfunktioner. För att klara den här utmaningen har Experience Platform flera verktyg som hjälper dig att skydda dina dataåtgärder.

### Datakryptering

Alla Experience Platform-data krypteras under överföring och i vila. Mer information finns i dokumentet om [datakryptering i Experience Platform](./encryption.md).

### Åtkomstkontroll {#access-control}

Experience Platform använder Adobe Admin Console för att tillhandahålla rollbaserad åtkomstkontroll till olika Experience Platform-funktioner. Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor.

Mer information finns i [åtkomstkontrollsöversikten](../../access-control/home.md).

### Sandlådor {#sandboxes}

Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose behovet av flexibilitet i utvecklingen tillhandahåller Experience Platform sandlådor som delar upp en enda Experience Platform-instans i separata virtuella miljöer så att ni kan utveckla era digitala upplevelseprogram utifrån er egen utvecklingslivscykel.

Se [översikten över sandlådor](../../sandboxes/home.md) för mer information.

## Nästa steg

I det här dokumentet finns en översikt över de olika Experience Platform-tjänster och verktyg som rör datastyrning, integritet och säkerhet. Mer information om dessa funktioner finns i dokumentationen som är länkad till i den här handboken.
