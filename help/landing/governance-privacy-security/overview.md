---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Styrning, integritet och säkerhet i Adobe Experience Platform
topic: overview
description: Experience Platform tillhandahåller flera tjänster och verktyg som gör att ni kan kontrollera era insamlade upplevelsedata på ett säkert sätt för att följa era affärspraxis, juridiska skyldigheter och utvecklingsprocesser.
translation-type: tm+mt
source-git-commit: 6ec317dd790b6ad77d8181c1398934f9636c5f5f
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---


# Styrning, integritet och säkerhet i Adobe Experience Platform

Med Adobe Experience Platform kan ni importera, analysera, optimera och agera utifrån era data för att förbättra kundupplevelserna avsevärt. Dessa data är enorma, komplexa och oerhört värdefulla. Beroende på vilken typ av databehandling ni bedriver, vilka juridiska behörigheter ert företag tillämpar och era organisationsprofiler när det gäller dataanvändning måste ni noga kontrollera och övervaka insamlingen och användningen av kundupplevelsedata för att skydda era affärsintressen.

Experience Platform tillhandahåller flera tjänster och verktyg som gör att ni kan kontrollera era insamlade upplevelsedata på ett säkert sätt för att följa era affärspraxis, juridiska skyldigheter och utvecklingsprocesser. I avsnitten nedan ges en introduktion till var och en av dessa tjänster tillsammans med länkar till dokumentation för ytterligare information.

Tjänsterna kan kategoriseras i tre domäner:

* [Datastyrning](#governance)
* [Integritet](#privacy)
* [Säkerhet](#security)

## Datastyrning {#governance}

Datastyrning är ett viktigt koncept som är sammankopplat med alla funktioner i Experience Platform. Datastyrning representerar er förmåga att kontrollera och förstå era data under hela resan via Platform. Detta innebär att upprätthålla datakvalitet, datalinje, datakatalogisering med mera.

### Adobe Experience Platform Data Governance {#data-governance}

Adobe Experience Platform datastyrning är en plattformstjänst som gör att ni kan hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll inom Experience Platform på olika nivåer, bland annat i fråga om dataanvändningsetiketter, dataanvändningspolicyer, policystyrning och datalänkning.

Mer information finns i [Datastyrningsöversikten](../../data-governance/home.md).

### Katalog och datauppsättningar {#catalog}

Katalogtjänsten är systemet för registrering av dataplatser och datalänkning inom plattformen. Alla data som importeras till Experience Platform lagras i Data Lake som filer och kataloger, men i Catalog finns metadata och beskrivning för dessa filer och kataloger för sökning och övervakning.

Katalogen organiserar inkapslade data i datauppsättningar, där varje datauppsättning innehåller metadata som kan användas för att etikettera och kategorisera data som den innehåller.

Mer information om tjänsten finns i [Katalogtjänstöversikt](../../catalog/home.md). Mer information om hur du hanterar datauppsättningar i Experience Platform finns i översikten över [datauppsättningar](../../catalog/datasets/overview.md).

## Sekretess {#privacy}

Sekretess är ett kritiskt problem för ert företag, era beslutsfattare och era kunder. Eftersom personuppgifter som samlas in från era kunder är centrala för nästan alla arbetsflöden i Experience Platform erbjuder Platform tjänster som stöder dessa initiativ.

### Adobe Experience Platform Privacy Service {#privacy-service}

Juridiska sekretessbestämmelser som EU:s allmänna dataskyddsförordning (GDPR) och Kaliforniens konsumentintegritetslag (CCPA) ger medborgare inom deras jurisdiktion rätt att få tillgång till och ta bort de personuppgifter som du samlar in och lagrar från dem.

Adobe Experience Platform Privacy Service tillhandahåller ett RESTful-API och användargränssnitt för att hantera dessa förfrågningar. Med Privacy Service kan ni skicka in förfrågningar om åtkomst till eller radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

Mer information finns i [Privacy Servicen overview](../../privacy-service/home.md).

### Samling {#consent} för samtycke

Många juridiska sekretessbestämmelser har infört krav på aktivt och specifikt samtycke när det gäller datainsamling, personalisering och andra användningsfall inom marknadsföring. För att uppfylla dessa krav kan Experience Platform samla in information om samtycke i enskilda kundprofiler och använda dessa inställningar som en avgörande faktor i hur varje kunds data används i arbetsflöden för plattformen längre fram i kedjan.

Mer information om hur du samlar in och bearbetar kundmedgivandedata i enlighet med IAB Transparency and Consent Framework (TCF) 2.0 finns i översikten om stöd för IAB TCF 2.0 i Platform](./consent/iab/overview.md).[

<!-- For more information on the consent collection process using the Adobe standard, see the [consent collection overview]. -->

## Säkerhet {#security}

Integriteten och säkerheten hos era data är oundgänglig för ert företag, och denna risk kräver branschledande säkerhetsfunktioner. För att klara den här utmaningen har Platform flera verktyg som hjälper dig att skydda dina dataåtgärder.

### Åtkomstkontroll {#access-control}

Experience Platform använder Adobe Admin Console för att tillhandahålla rollbaserad åtkomstkontroll för olika plattformsfunktioner. Den här funktionen utnyttjar produktprofiler i Admin Console, som länkar användare med behörigheter och sandlådor.

Mer information finns i [översikten över åtkomstkontroll](../../access-control/home.md).

### Sandlådor {#sandboxes}

Experience Platform är byggt för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

För att tillgodose behovet av flexibilitet i utvecklingen tillhandahåller Experience Platform sandlådor som delar upp en enda plattformsinstans i separata virtuella miljöer för att hjälpa er att utveckla era program för digitala upplevelser baserat på er egen utvecklingslivscykel.

Mer information finns i [översikten över sandlådor](../../sandboxes/home.md).

## Nästa steg

Detta dokument innehåller en översikt över de olika plattformstjänster och verktyg som används för datastyrning, integritet och säkerhet. Mer information om dessa funktioner finns i dokumentationen som är länkad till i den här handboken.