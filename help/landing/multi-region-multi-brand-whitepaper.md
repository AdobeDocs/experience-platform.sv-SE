---
title: Adobe Experience Platform för företag med flera regioner och varumärken
description: Lär er hur ni ger era implementeringsteam de verktyg och insikter som behövs för att effektivt kunna navigera i Adobe Experience Platform knep.
source-git-commit: 6e96cf7660a9a7fe1b4eaef645bca55ed89b7673
workflow-type: tm+mt
source-wordcount: '5322'
ht-degree: 0%

---


# Adobe Experience Platform för företag med flera regioner och varumärken

## Introduktion

Adobe Experience Platform ligger i framkanten när det gäller omvandlingslösningar och ger er möjlighet att utnyttja era kunddata och ert innehåll fullt ut. Med Experience Platform kan ni centralisera och standardisera data från olika system och utnyttja datavetenskap och maskininlärning. Resultatet blir bättre framtagning och leverans av personaliserade upplevelser som får genklang hos era kunder.

Experience Platform ger er möjlighet att representera strukturen och styra era affärsdata för skalbara, flexibla implementeringar. Implementering av plattformsapplikationer är en viktig resa som kräver strategisk planering och noggranna överväganden, särskilt om ni arbetar i globala, regionala och varumärkesspecifika domäner eller en kombination av alla dessa aspekter.

Det här faktabladet fungerar som referens och innehåller en produktuppfattning och en uppsättning riktlinjer. Dess främsta mål är att ge er och era implementeringsteam de verktyg och insikter som behövs för att effektivt kunna navigera i Experience Platform knepigt. Genom att tillhandahålla ett strukturerat ramverk för utvärdering av specifika behov, överväganden och verkliga användningsområden, får du den kunskap som behövs för att utnyttja Experience Platform och plattformsbaserade tillämpningar fullt ut. När ni läser följande avsnitt hittar ni värdefulla insikter och rekommendationer för att effektivisera implementeringsprocessen och öka er organisations förmåga att leverera exceptionella upplevelser till er målgrupp, samtidigt som ni tillhandahåller styrning och kontroller för att upprätthålla sekretess och regelefterlevnad.

![CDP-enhetlig profil](./images/whitepaper/CDPoverview.png)

## Förstå flervarumärkes- och flerregionsföretag

Om ni har ett flervarumärke, ett flerregionalt företag har ni antagligen unika datahanteringskrav för Experience Platform. Att förstå era specifika krav är avgörande för att skräddarsy Experience Platform-implementeringen efter just era behov.

När ni utforskar olika installationsalternativ måste ni förstå och tänka på vilka personligheter som kommer att interagera med Experience Platform och plattformsbaserade program. Att utforma upplevelsen utifrån deras roller och intressen säkerställer en lyckad implementering. Här är tre nyckelpersoner som du bör tänka på när du utforskar alternativen:

**Mary, marknadsföraren:**

- Fokus: Kundvärvning och personalisering av upplevelser i stor skala.
- Mål: Skapa omfattande profiler och förbättra medieeffektiviteten.

**Ted, teknikern**

- Fokus: Organiserad datahantering.
- Mål: Säkerställa regelefterlevnad, hantera vattentäta skott och betjäna olika affärsområden.

**Dan, dataarkitekten**

- Fokus: Noggrannhet och kvalitet för data.
- Mål: Säkerställa datasekretess och förtroende, utforma scheman och datamodeller, hantera datakällor.

### Ett företag med begränsad dataisolering

En viktig arkitekturprincip i Experience Platform är en princip där kunddata är begränsade till en viss produktionssandlåda som bygger på riktlinjer och krav för styrning.

Om er organisation behöver en enda datamiljö för att kunna hantera er marknadsföringsupplevelse i stor skala kanske ni föredrar att konsolidera alla data i en enda Experience Platform-sandlåda med minimala krav på dataisolering. I den här konfigurationen importeras data till en sandlåda, och alla relaterade identiteter representeras som en enda enhetlig profil, oavsett om den identifieras av en pseudonym eller känd identitet. Det innebär att era marknadsförare kan komma åt alla profilattribut och uppleva händelsedata inom Experience Platform i hela företaget. De kan använda dessa data tillsammans med plattformsbaserade applikationer för att skapa målgrupper och resor med minimalt behov av att begränsa marknadsförarna från att använda alla data oavsett varumärke eller region. Detta underlättar smidig segmentering och målgruppsaktivering i de destinationer som stöds av Experience Platform-programmen. Denna strategi fungerar bra om ni vill utnyttja hela kundbasen, oavsett regionala eller varumärkesspecifika skillnader, för enhetliga och sammanhängande marknadsföringssatsningar.

![CDP-Architecture Single Production Sandbox](./images/whitepaper/Architecture-single-prod-sandbox.png)

#### Så här fungerar det

Vi börjar med att planera implementeringen och konfigurera din toppnivåmiljö. Därefter bestämmer du hur många sandlådor, roller och behörigheter som krävs för att köra Experience Platform och plattformsbaserade program som är optimala för ditt företag.

##### Allmän konfiguration för implementeringen

- Konfigurera sandlådor så att enhetliga kundprofiler kan byggas.
- Ställ in roller och åtkomstkontroller för att administrera sandlådor och åtkomst till funktioner för varje person.
- Hantera utvecklingslivscykeln med en utvecklingssandlåda och sandlådeverktyg.

**Sandlådor**

Sandlådor är virtuella partitioner i en enda instans av Experience Platform, vilket möjliggör smidig integrering med utvecklingsprocessen i era program för digitala upplevelser. Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till den sandlådan och påverkar inte någon annan sandlåda, inklusive data och tillgång till data. Det finns två typer av sandlådor som stöds i Experience Platform:

- **Produktionssandlåda**: En produktionssandlåda är avsedd att användas med profiler i din produktionsmiljö. Med Experience Platform kan du skapa flera produktionssandlådor för att tillhandahålla rätt datafunktionalitet samtidigt som driftisoleringen bibehålls.

- **Utvecklingssandlåda**: En utvecklingssandlåda kan användas exklusivt för utveckling och testning med icke-produktionsprofiler.

Du kan skapa flera sandlådor av alla typer, och för den här typen av företag använder vi en produktions- och en utvecklingssandlåda för att illustrera hur den här typen av företag ska köras och köras.

![CDP-Skapa en sandlåda](./images/whitepaper/Create-sandbox.png)

I produktionssandlådan förväntar vi oss att ni ska importera era produktionsprofiler och upplevelsehändelsedata för att skapa en enhetlig profil för era marknadsföringsaktiviteter. Mer information om hur du kombinerar kända och anonyma data från flera företagskällor för att skapa kundprofiler som kan användas för att leverera personaliserade kundupplevelser i alla kanaler och enheter i realtid finns i [Adobe Real-Time Customer Data Platform-dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-platform/rtcdp/home).

**Åtkomstkontroller**

Du kan definiera åtkomstkontroller med roller och behörigheter för att styra åtkomsten till programresurser beroende på vilken persondator och vilka funktioner som krävs. Dessutom kan du begränsa åtkomsten till specifika fält i profildata. I det här steget bör ni gå igenom de djupgående stegen för att bättre styra användningen av Experience Platform, plattformsbaserade program och era kunddata.

Överväg en datatekniker som kanske inte behöver tillgång till alla Experience Platform-funktioner och plattformsbaserade programfunktioner. De ansvarar vanligtvis för att skapa datadefinitioner (scheman), konfigurera datakällor för att importera data och skapa datauppsättningar. Men de kanske inte är samma person som skapar och aktiverar målgrupper för personaliserade kundupplevelser. Skapa en roll för den här personen, lägg till lämpliga behörigheter och ge åtkomst endast till de funktioner som krävs. En marknadsförare skulle däremot inte skapa scheman och inhämta data utan istället fokusera på att skapa och aktivera målgrupper för att möjliggöra personaliserade kundupplevelser.

Om du vill kan du lägga till detaljerade åtkomstkontroller för att begränsa åtkomsten till specifika fält i den enhetliga kundprofilen med attributbaserad åtkomstkontroll/åtkomstkontroll på fältnivå. Detta är styrningsmekanismer i Experience Platform som gör att du kan begränsa åtkomst till dataattribut baserat på fördefinierade etiketter. Med åtkomstkontroll på fältnivå kan personligt identifierbara data styras och åtkomsten begränsas i alla Experience Platform- och programarbetsflöden. Mer information om åtkomstkontrollsfunktioner finns i [åtkomstkontrollsdokumentationen](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home).

![CDP-åtkomstkontroller, konfigurera rollbehörigheter](./images/whitepaper/Access-Controls-Configure-RolePermissions.png)

**Utvecklingslivscykel med utvecklingssandlådor**

En utvecklingssandlåda fungerar på samma sätt som en produktionssandlåda i alla funktionella aspekter. Det skiljer sig genom att det kommer att finnas avtalsenliga garantimöjligheter som håller dig inom licensgränserna. Den är exklusiv för utveckling och testning med icke-produktionsprofiler, som stöder upp till 10 % av din licensierade profil (mäts kumulativt i alla godkända utvecklingssandlådor). Mer information och skyddsförslag finns i översiktsdokumentationen för [sandlådor](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/home) och på sidan [produktbeskrivningar](https://helpx.adobe.com/se/legal/product-descriptions.html) för berättigandeinformation.

Du kan ha flera utvecklingssandlådor (upp till 4 i det här företagsexemplet, eftersom vi använder en produktionssandlåda) för utvecklings- och testlivscykeln.

**Exportera och importera paket med sandlådeverktyg**

Verktygsfunktionen i sandlådan gör att användare med lämplig behörighet kan paketera sitt arbete från en utvecklingssandlåda och exportera det till en databas. Den här databasen är tillgänglig för andra användare, som kan importera dessa paket till sina angivna sandlådor. Denna funktion säkerställer enhetliga konfigurationer över sandlådor, vilket underlättar smidiga export- och importprocesser.

När du använder sandlådeverktyg förbättras konfigurationsnoggrannheten avsevärt och den tid som krävs för implementeringen minskar. Det gör det möjligt att effektivt flytta framgångsrika konfigurationer mellan olika sandlådor.

Med sandlådeverktygen kan du markera olika objekt och exportera dem till ett paket. Ett paket kan innehålla ett eller flera objekt, men alla objekt måste komma från samma sandlåda.

**Automatisering av sandlådor via API:er**

Du kan använda Experience Platform API:er för att automatisera sandlådedistributioner och konfigurationsåtgärder. API:er ger programmerbar kontroll för repetitiva uppgifter som export, import eller ändring av sandlådekonfigurationer, vilket ger flexibilitet om du föredrar automatiserade arbetsflöden.

Mer information om sandlådeverktyg finns i [dokumentationen för sandlådeverktyg](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/ui/sandbox-tooling).

| ![CDP-Skapa ett paket](./images/whitepaper/create-package.png) | ![CDP-List-paket](./images/whitepaper/list-packages.png) |
| --- | --- |

### Region eller varumärkesspecifik dataisolering

Om ni kräver fullständig isolering (t.ex. regional eller varumärkesbaserad) kan ni bedriva verksamhet enligt strikta regler för dataåtkomst eller juridiska krav som begränsar era varumärkesteam tillgång till data som är specifika för deras respektive regioner eller varumärken. Ni definierar åtkomstmönster baserat på region- eller varumärkesspecifika data och ser till att ni följer interna, reglerande och datastyrande protokoll. Detta tillvägagångssätt är avgörande om ni arbetar inom reglerade branscher (t.ex. hantering av PII-data) eller behöver upprätthålla distinkta och segmenterade data för olika geografiska regioner eller varumärkesidentiteter.

![CDP-Architecture Multiple Production Sandboxes](./images/whitepaper/Architecture-multiple-prod-sandbox.png)

#### Så här fungerar det

Vi börjar med att planera implementeringen, konfigurera din toppnivåmiljö och bestämma hur många sandlådor, roller och behörigheter som krävs för att köra Experience Platform och plattformsbaserade program som är optimalt för ditt företag.

##### Allmän konfiguration för implementering av flera sandlådor

- Konfigurera flera produktionssandlådor för att kunna skapa enhetliga kundprofiler i varje sandlåda.

- Ställ in roller och åtkomstkontroller för att administrera sandlådor och åtkomst till funktioner för varje person.

- Hantera utvecklingslivscykeln med sandlådeverktyg.

- Global rapportering och aktivering (samla in data från flera sandlådor för att få information om olika organisationer med Customer Journey Analytics).

**Sandlådor**

I motsats till en konfiguration med en enda produktionssandlåda kan du behöva ett mer komplext tillvägagångssätt om du behöver isolera data och arbetsflöden helt och hållet. Det är här som flera produktionssandlådor spelas upp, där var och en representerar en isoleringsenhet som är anpassad efter dina specifika behov.

Som vi nämnt är varje sandlåda en virtuell partition inom en enda plattformsinstans. Med dessa sandlådor kan du hantera data, arbetsflöden och processer i en kontrollerad miljö som inte stör andra sandlådor. Utvecklingssandlådor är avsedda för testning och utveckling med icke-produktionsprofiler, men produktionssandlådor är ryggraden i liveoperationer och stöder inmatning av faktiska produktionsdata för verkliga marknadsföringsaktiviteter.

Viktiga fördelar med ren isolering i produktionssandlådor:

1. **Datastyrning och efterlevnad:** Om du arbetar i reglerade branscher eller regioner med strikta datasekretesslagar måste du se till att data från en region eller ett varumärke förblir isolerade. Med flera produktionssandlådor kan ni uppfylla styrningskrav eller branschspecifika standarder genom att se till att data bara är tillgängliga i rätt sandlåda.

2. **Driftseffektivitet:** Genom att isolera data och arbetsflöden kan du hantera dina åtgärder mer effektivt. Dina team som ansvarar för olika regioner eller varumärken kan arbeta oberoende av varandra i sina dedikerade sandlådor utan att behöva oroa sig för oavsiktliga dataläckor eller obehörig åtkomst.

3. **Anpassade arbetsflöden:** Du kan anpassa varje produktionssandlåda efter din regions specifika behov eller det varumärke den representerar. På så sätt kan ni implementera anpassade arbetsflöden, datamodeller och marknadsföringsstrategier som är optimerade för det segmentet.

4. **Skalbarhet:** I takt med att du växer kan du enkelt skapa ytterligare produktionssandlådor för nya regioner eller varumärken. Denna skalbarhet säkerställer att plattformen kan anpassa sig efter dina behov utan att dataintegriteten eller prestandan äventyras.

5. **Förbättrad kontroll:** Med flera produktionssandlådor har dina administratörer detaljerad kontroll över åtkomstbehörigheter, datainhämtning och arbetsflödeskörning. På så sätt kan ni på ett säkrare och mer strukturerat sätt hantera komplexa operationer i hela företaget.

**Åtkomstkontroller**

I samband med flera produktionssandlådor är åtkomstkontroller fortfarande en viktig del i hanteringen av data och arbetsflöden i Experience Platform. Komplexiteten ökar dock eftersom era administratörer måste se till att användarna bara har tillgång till de sandlådor som är relevanta för deras roller, samtidigt som de fortfarande aktiverar operationer över sandlådor för användare som behöver det, som era marknadsföringsteam som omfattar flera regioner eller datatekniker som ansvarar för global datainmatning och datamodellering.

**Definiera roller och behörigheter i alla sandlådor:**

På samma sätt som i det enskilda läget för produktionssandlådan kan du definiera åtkomstkontrollprinciper med roller och behörigheter som är anpassade efter olika personers behov. Du måste dock tänka på hur de här rollerna sträcker sig över olika sandlådor i en miljö med flera sandlådor.

Till exempel:

- **Regionala marknadsförare:** Om dina marknadsförare arbetar i flera regioner kan deras roller behöva omfatta mer än en sandlåda. Du kan ge dem de behörigheter som krävs för att få åtkomst till resurser i flera sandlådor samtidigt som du ser till att deras åtkomst fortfarande begränsas till rätt data och arbetsflöden i varje sandlåda.

- **Datatekniker:** Datatekniker som ansvarar för att skapa datamodeller, definiera scheman och hantera datainmatning kan behöva åtkomst till alla sandlådor. Du kan utforma deras roller så att de kan fungera på hela plattformen samtidigt som deras åtkomst begränsas till funktioner och data som är relevanta för deras uppgifter. Din datatekniker som arbetar med datamodeller för Europa och Nordamerika kan till exempel komma åt produktionssandlådorna för dessa regioner med tillstånd att ändra scheman och importera data. De skulle dock inte ha möjlighet att komma åt marknadsföringsfunktioner som att skapa och aktivera målgrupper.

**Granska överväganden för åtkomstkontroll:**

I en miljö med flera sandlådor blir den detaljerade åtkomstkontrollen ännu viktigare. Attributbaserad åtkomstkontroll (åtkomstkontroll på fältnivå/åtkomstkontroll på objektnivå) gör att du kan begränsa åtkomsten till specifika datafält i profiler eller vissa målgrupper ytterligare och se till att känslig eller personligt identifierbar information (PII) skyddas i alla dina sandlådor. Till exempel:

- Du kan begränsa åtkomsten till vissa datafält i en sandlåda till endast användare i den regionen. Detta garanterar att PII-data eller känsliga data endast är synliga för dem som behöver dem, i enlighet med sekretessbestämmelser och interna styrningspolicyer.

- För användare med åtkomst över sandlådor ser attributbaserad åtkomstkontroll till att även om de har åtkomst till flera sandlådor så begränsas deras synlighet för känsliga data av deras roll och av deras&quot;need-to-know&quot;-bas.

Fördelar med rollbaserade och attributbaserade åtkomstkontroller:

1. Genom att styra åtkomsten baserat på roller och attribut kan ni avsevärt minska risken för obehörig dataåtkomst, vilket säkerställer att endast de som har rätt behörighet kan visa eller ändra känslig information.

2. Tydliga och väldefinierade roller och behörigheter effektiviserar verksamheten, eftersom varje person har tillgång till de funktioner och data de behöver utan onödigt trassel eller risker. Denna skärpa stöder effektiva arbetsflöden och minskar friktionen.

3. I takt med att företaget växer och utvecklas kan åtkomstkontrollerna justeras för att passa nya regioner, varumärken eller roller. Flexibiliteten att ändra åtkomsten utan att störa befintliga arbetsflöden är avgörande för att du ska kunna skala din verksamhet.

4. Administratörer kan ha centraliserad kontroll över alla sandlådor, vilket säkerställer konsekvens i hur åtkomstkontroller tillämpas i hela företaget samtidigt som man kan anpassa för olika regioner eller varumärken.

**Utvecklingslivscykel med utvecklingssandlådor**

För att kunna hantera utvecklingslivscykeln i flera regioner och varumärken inom Experience Platform måste ni ha en stabil strategi som säkerställer konsekvens, effektivitet och skalbarhet. Utvecklingssandlådor har stöd för utvecklingslivscykeln i en komplex miljö med flera produktionssandlådor. De har förbättrats med sandlådeverktygen, som möjliggör smidig konfigurationsdelning och driftsättning i olika miljöer.

Utvecklingssandlådor spelar en viktig roll i utvecklingslivscykeln. Dessa sandlådor utgör en isolerad miljö där utvecklare och datatekniker kan bygga, testa och iterera i konfigurationer utan att påverka produktionsdata. Även om de fungerar på liknande sätt som produktionssandlådor skiljer sig utvecklingssandlådor åt eftersom de är avsedda för testning med icke-produktionsprofiler och styrs av avtalsbegränsningar, till exempel stöd för upp till 10 % av din licensierade profil i alla auktoriserade utvecklingssandlådor.

Du kan skapa flera utvecklingssandlådor som har stöd för olika team eller regioner. På så sätt kan var och en av era team experimentera med arbetsflöden som är specifika för deras region eller varumärke, vilket säkerställer att produktionsmiljöerna förblir stabila och säkra under utvecklingen. Om du har många produktionssandlådor rekommenderar vi att du använder en pool med utvecklingssandlådor för att stödja flera regioner/varumärken.

**Exportera och importera paket med sandlådeverktyg**

Verktygsfunktionen i sandlådan är ett kraftfullt verktyg om du hanterar flera sandlådor. Det gör det möjligt för utvecklare, datatekniker och marknadsförare att paketera sitt arbete i en utvecklingssandlåda, inklusive scheman, datamodeller och andra konfigurationer, och sedan exportera dem till en databas. Därifrån kan andra användare komma åt och importera dessa paket till sina utsedda sandlådor, vilket underlättar smidig delning och driftsättning av lyckade konfigurationer i hela företaget.

Din datatekniker som arbetar i en utvecklingssandlåda för den nordamerikanska regionen kan till exempel skapa ett schema och paketera det med alla sina beroenden. En annan datatekniker i en annan region, till exempel Europa, kan komma åt det här paketet och importera det till sin regionala sandlåda. Denna process säkerställer en konsekvent datamodellering och konfiguration i hela företaget, vilket minskar risken för fel och förbättrar effektiviteten.

Fördelar med sandlådeverktyg i en miljö med flera sandlådor:

1. Verktyg i sandlådan effektiviserar utvecklingscykeln genom att tillåta att framgångsrika konfigurationer enkelt delas över flera sandlådor. Detta minskar dubbelarbetet och säkerställer att bästa praxis implementeras på ett konsekvent sätt i alla regioner och varumärken.

2. Möjligheten att exportera och importera paket mellan olika sandlådor förbättrar interoperabiliteten inom företaget. Team i olika regioner kan samarbeta effektivare och se till att deras konfigurationer är anpassade efter de övergripande företagsmålen samtidigt som de klarar regionala eller varumärkesspecifika krav.

3. I takt med att företag växer och lägger till fler sandlådor för att ta emot nya regioner eller varumärken ger sandlådeverktygen den skalbarhet som behövs för att hantera dessa miljöer på ett effektivt sätt. Nya sandlådor kan snabbt konfigureras med befintliga paket, vilket snabbar upp introduktionsprocessen och minskar den tid som krävs för att driftsätta.

4. Genom att paketera konfigurationer och beroenden i en utvecklingssandlåda och sedan distribuera dem till produktionssandlådor kan företag säkerställa att deras konfigurationer är korrekta och konsekventa över hela organisationen. Detta minskar risken för fel och förbättrar plattformens tillförlitlighet.

5. Med sandlådeverktyg blir övergången från utveckling till produktion smidig och kontrollerad. När konfigurationer har testats och validerats i en utvecklingssandlåda kan de exporteras och importeras till en produktionssandlåda i trygg förvissning om att de fungerar som förväntat.

**Global rapportering och aktivering**

Detta innebär att samla in data från flera sandlådor för att få information om olika organisationer, vilket ofta kräver en dedikerad rapportsandlåda för integrering med Customer Journey Analytics.

Även om det finns tydliga fördelar med att använda flera produktionssandlådor för att isolera regionala och varumärkesspecifika operationer ger det också upphov till utmaningar som kräver kreativa lösningar. En viktig utmaning är möjligheten att analysera data över sandlådor för global rapportering och globala kampanjsyften. Företag måste ofta förstå kundresan på global nivå, vilket innefattar att integrera data från flera sandlådor och möjliggöra marknadsföringsaktiviteter över sandlådor. Nedan beskrivs olika strategier för att hantera dessa utmaningar.

**Global rapportering över sandlådor**

När ett företag arbetar med flera produktionssandlådor, där var och en representerar en region eller ett varumärke, blir det komplicerat att analysera kunddata över alla sandlådor. Att skapa en enhetlig bild av kundresan över olika varumärken kräver till exempel att data från dessa isolerade miljöer konsolideras.

**Dedikerad global sandlåda**

![CDP-dedikerad global rapportsandlåda](./images/whitepaper/dedicated-global-reporting-sandbox.png)

Denna sandlåda fungerar som en central databas där data från enskilda regionala eller varumärkesspecifika sandlådor konsolideras. En vanlig lösning är att använda frågetjänsten i varje sandlåda för att extrahera relevanta kunddata. Detta kan omfatta profiler och upplevelsehändelser som behöver analyseras i olika regioner eller varumärken. När data har förberetts från varje sandlåda hämtas de in i den globala rapportsandlådan för analys och målgruppsskapande.

Använd Customer Journey Analytics för att utföra marknadsanalyser och varumärkesanalyser på aggregerade data i den globala sandlådan för att få en heltäckande bild av kundinteraktioner över alla varumärken och regioner. På så sätt kan de generera värdefulla insikter, som att identifiera kunder som interagerar med flera varumärken och skapa korsvarumärken eller korsregionala målgrupper. Dessa insikter kan användas för olika syften, bland annat för att aktivera marknadsföringsstrategier, personalisera kundupplevelser och driva företagets tillväxt.

**Målgruppsdelning**

Den globala sandlådan gör det även möjligt för globala marknadsföringsteam att definiera och hantera målgrupper i en vidare skala. Med hjälp av sandlådeverktyg kan dessa globala målgrupper (endast definitioner, inte data) exporteras från den globala sandlådan till enskilda varumärken eller regionala sandlådor, så att lokala marknadsföringsteam kan utvärdera och aktivera dem på sina respektive marknader.

Dessutom kan du använda Experience Platform Segment Match, en funktion i Platform som möjliggör segmentdelning mellan sandlådor (kvalificerad publik) mellan olika organisationsenheter eller affärsenheter.

Med denna segmentdelningstjänst kan två eller flera användare utbyta segmentdata på ett säkert, styrt och sekretessvänligt sätt.

Mer information om funktionen för segmentmatchning finns i [dokumentationen för segmentmatchning](https://experienceleague.adobe.com/sv/docs/experience-platform/segmentation/ui/segment-match/overview).

### En kombination av strategier för globala verksamheter, regionala och varumärkesspecifika

Många företag med flera varumärken arbetar globalt och söker därför ofta en kombination av både enhetliga och isolerade datahanteringsstrategier. De försöker skilja på data för flera regioner eller länder i det här scenariot. Varumärken inom organisationen kan förvänta sig att de arbetar exklusivt med de data som är kopplade till deras specifika varumärke, allt inom samma datagränser för en geografisk eller nationell region. Detta tillvägagångssätt möjliggör centraliserad datahantering på regional nivå eller nationell nivå samtidigt som det underlättar varumärkesspecifik marknadsföring och datahantering. Det är en modell som kombinerar fördelarna med enhetlig datahantering med behovet av varumärkes- och regionspecifik isolering.

Med hänsyn till dessa krav kan Experience Platform konfigureras för att ge dig en mycket anpassningsbar och flexibel datahanteringslösning, vilket säkerställer att företag med flera varumärken och regioner effektivt kan representera ert företag inom plattformen. Oavsett om målet är att maximera de samlade kunddata, bibehålla strikt isolering av data eller uppnå balans mellan dessa två, är Experience Platform utrustat för att uppfylla företagets olika behov.

![CDP-Architecture A blend approach](./images/whitepaper/Architecture-blend-sandbox.png)

#### Så här fungerar det

Vi börjar med att planera implementeringen, konfigurera din toppnivåmiljö och bestämma hur många sandlådor, roller och behörigheter som krävs för att köra Experience Platform och plattformsbaserade program som är optimalt för det här företaget.

##### Allmänna inställningar för det här företaget

- Konfigurera flera produktionssandlådor för att kunna skapa enhetliga kundprofiler.

- Ställ in roller och åtkomstkontroller för att administrera sandlådor och åtkomst till funktioner för varje person.

- Konfigurera attributbaserad åtkomstkontroll: Åtkomstkontroll på fältnivå/åtkomstkontroll på objektnivå för detaljstyrning av profilattribut och målgrupper.

- Hantera utvecklingslivscykeln med utvecklingssandlådor och sandlådeverktyg.

- Global rapportering.

**Sandlådor**

Konfigurera en sandlåda per varumärke/region. Se avsnitten ovan för att skapa flera produktionssandlådor.

**Åtkomstkontroller**

Roller och användarbehörigheter:

- Skapa rollen **Marketer—Global** och ge behörighet att skapa, visa och hantera målgrupper. Dessutom får den här rollen behörighet att visa alla kunddata.

- Skapa roller och ge åtkomst endast till vissa funktioner för rätt person. Användarrollerna **Marketer—Germany** och **Marketer—France** får till exempel bara behörighet att skapa, visa och hantera målgrupper på landdata som aktiveras av en kombination av åtkomstkontroll på fältnivå, åtkomstkontroll på objektnivå och standardmålgrupper.

- Skapa rollen **Tekniker—Global** och ge rätt behörighet att skapa och hantera scheman, datauppsättningar, principer, källor och så vidare. Den här rollen ansvarar för all nödvändig administration och alla nödvändiga konfigurationer.

###### Schemadesign och attributbaserad åtkomstkontroll: Åtkomstkontroll på fältnivå

**Experience data model (XDM)**

Ett standardiserat dataschema i Experience Platform som säkerställer enhetlig datastruktur och interoperabilitet för alla plattformsbaserade program.

**Attributbaserad åtkomstkontroll: Åtkomstkontroll på fältnivå och datamodelleringsalternativ:**

- Skapa en datamodell som innehåller klientspecifika XDM-fält (PII) som bör begränsas för varje land.

- Skapa och tillämpa landsetiketter på XDM-fält. Etiketter = Tyskland, Frankrike, Irland, Nederländerna osv.

- Lägg till etiketter i rätt roll. Lägg till exempel till etiketten Tyskland i rollen&quot;Marketer - Tyskland&quot;.

Schema för enskild XDM-profil:

```
\- PII
\- Germany
    \- name --> Label: "Germany"
    \- email --> Label: "Germany"
    \- birthdate --> Label: "Germany"

\- France
    \- name --> Label: "France"
    \- email --> Label: "France"
    \- birthdate --> Label: "France"

\- Netherland
    \- name --> Label: "Netherland", "Germany"
    \- email --> Label: "Netherland", "Germany"
    \- birthdate --> Label: "Netherland", "Germany"

\- Loyalty
    \- member
    \- registrationDate
```

###### Målgrupper: Använd attributbaserad åtkomstkontroll: Åtkomstkontroll på objektnivå för att styra åtkomsten till varumärkes-/landsspecifika målgrupper

**Attributbaserad åtkomstkontroll: Åtkomstkontroll på objektnivå för målgrupper:**

- Skapa målgrupper och styr vilka som kan se dem.

- Skapa och använd landsetiketter på målgrupper. Etiketter = Tyskland, Frankrike, Irland, Nederländerna osv.

- Lägg till etiketter i rätt roll. Lägg till exempel till etiketten&quot;Tyskland&quot; i rollen&quot;Marketer - Tyskland&quot;.

![CDP-Label-målgrupper](./images/whitepaper/label-audience.png)

###### Inkludera en standardmålgrupp när ni skapar varumärkes-/landsspecifika målgrupper

**Standardmålgrupp: Alternativ till åtkomstkontroll på radnivå:**

- För närvarande kan ni med målgruppsverktyget inkludera befintliga målgrupper som byggstenar i målgruppsprocessen.

- Resultatet kommer från publiken, följt av attribut och händelser.

- Det finns ingen mekanism för att automatiskt lägga till en eller flera målgrupper vid tidpunkten för kompositionen.

![CDP-Lägg till en standardmålgrupp](./images/whitepaper/default-audience.png)

###### Aktivering och profilfiltrering på varumärkes-/landsnivå

**Principalternativ för anpassat samtycke:**

Detta gör att du kan styra eller filtrera profiler när de aktiveras:

- Skapa marknadsföringsåtgärder.

- Skapa ett mål och associera marknadsföringsåtgärden.

- Skapa en anpassad medgivandeprincip.

>[!NOTE]
>
> SKU:n för skölden för skydd av privatlivet och säkerhet krävs för att skapa policyer för samtycke.

![CDP-anpassad princip för samtycke och aktiveringsfiltrering](./images/whitepaper/custom-consent-policy.png)

Aktivering av flera varumärken och komplex policy för samtycke:

För att kunna hantera målgruppsaktivering för flera varumärken krävs en detaljerad styrning av samtyckespolicyer som säkerställer att varje varumärkes unika krav uppfylls. Dessutom kan Adobe Privacy and Security Shield (en efterlevnadsfunktion i Experience Platform som upprätthåller dataskyddspolicyer och ser till att lagstiftningen anpassas till olika aktiveringskanaler) införa specifika begränsningar för hur medgivandepolicyer tillämpas i olika aktiveringskanaler. Ni bör noggrant utvärdera dessa överväganden och implementera styrningsramverk för att upprätthålla regelefterlevnad och driftseffektivitet.

Du måste också noggrant navigera bland komplexiteten kring konfigurationer av medgivandeprinciper och kanalspecifika aktiveringar. Det är avgörande för regelefterlevnad och driftseffektivitet att explicit definiera regler för samtycke för varje region eller varumärke och konsekvent hantera dessa konfigurationer.

## Allmänna överväganden

I vissa scenarier kan du välja att distribuera Experience Platform-program och plattformsbaserade program till flera organisations-ID:n i stället för att använda ett enda organisations-ID med många sandlådor. Detta tillvägagångssätt kan ge fördelar när det gäller dataresistens, säkerhet och administration, men det kan också medföra komplexitet. Här följer några viktiga överväganden för att avgöra när en strategi för flera organisationer kan vara lämplig.

### Vad är ett företags-ID?

- Ett företags-ID är Adobe implementering av Federated ID- och OAuth 2.0-protokoll.

- Ett företags-ID är en samling med alla program, användare och behörigheter som en organisation har behörighet till enligt sina Adobe-avtalsvillkor.

- Användarkonton och behörigheter hanteras via respektive organisations Admin Console.

- Organisations-ID:n styr också hur Adobe lösningar samverkar med varandra. Lösningar inom samma organisation kan vara kompatibla.

- I allmänhet distribueras ett organisations-ID i en enda geografisk region.

![CDP-Architecture Multiple IMS Orgs Option](./images/whitepaper/Architecture-multi-imsorg.png)

**Flera organisations-ID: Fördelar och överväganden &#x200B;**

| Fördelar | Överväganden |
| -------- | -------------- |
| Nedan följer en lista över fördelarna med att ha flera organisations-ID:n: <ul><li>Flexibilitet att lagra data i särskilda globala regioner.</li><li>&#x200B; separata användarinloggningar per instans, d.v.s. helfödoverk kan inte logga in på Audible. &#x200B;</li><li>Dedikerade API-slutpunkter som ger varje Market/BU möjlighet att skapa anpassade anslutningar efter behov i sina egna &#x200B;.</li><li>Varje affärsenhet skulle ha sina egna kundhanterade nycklar &#x200B;.</li><li>GDPR-begäranden kan göras per affärsenhet &#x200B;.</li><li>Helt isolerad lagring och beräkning mellan affärsenheter &#x200B;.</li><li>Justerar vissa prestandaresäkerhetsgarantier/begränsningar på organisationsnivå &#x200B;.</li><li>Mer flexibilitet med provisionering och mixning av SKU:er mellan olika affärsenheter. En organisation kan till exempel ha en annan SKU än Adobe Journey Optimizer jämfört med en annan.</li></ul> | Nedan följer några saker du bör tänka på när du har flera organisations-ID:n: <ul><li>Flera organisations-ID:n att hantera, jämfört med ett. &#x200B;</li><li>Flera olika instanser/miljöer att hantera (integreringar, datainläsningar och så vidare).</li><li>&#x200B; ECID är unika per organisation, vilket gör det svårt att matcha data mellan olika &#x200B;.</li><li>Skulle behöva migrera/återimplementera Analytics och Target per organisation - förlora global sammanslagning (om den används för närvarande). &#x200B;</li><li>Mer samordning krävs för att göra GDPR-förfrågningar &#x200B; olika affärsenheter.</li><li>Vissa Experience Platform-baserade programintegrationer lagrar metadata på organisationsnivå. Allt är inte&quot;sandlådor&quot;. &#x200B;</li><li>Organisations-ID är fäst till en region. Värdplatsen för Adobe AWS ligger för närvarande endast i USA. Adobe stöder inte migrering från en värdregion till en annan. &#x200B;</li><li>Edge är inte sandlådemedveten (för händelsevidarebefordran).</li></ul> |

**ID för en organisation: Fördelar och överväganden**

![CDP-Architecture Multiple Production Sandboxes](./images/whitepaper/Architecture-multiple-prod-sandbox.png)

| Fördelar | Överväganden |
| -------- | -------------- |
| Nedan följer en lista över fördelarna med att ha ett enda organisations-ID: <ul><li>Tillhandahålla enskilda sandlådor för att skapa logisk separation mellan affärsenheter inom en distribuerad region</li><li>Ett enda organisations-ID som IT-avdelningen kan hantera för användare, provisionering och så vidare.</li><li>Ingen migrering av Adobe Tags, Target, Analytics med flera, om ni stannar kvar i samma företags-ID.</li><li>Ingen återställning krävs för befintliga ECID:n - förhindrar&quot;urklippning&quot; i Adobe Analytics-data.</li><li>En inloggning för globala marknadsföringsresurser.</li><li>Användaråtkomsträttigheter för att styra vem som har åtkomst till vilka sandlådor, med lämpliga nivåer av rollbaserad åtkomstkontroll.</li><li>Utnyttja Global Analytics och Target-instanser och rapportera Suite-data.</li></ul> | Nedan följer några saker du bör tänka på när du har ett enda organisations-ID: <ul><li>Data lagras i en enda region.</li><li>Möjligt behov av att konsolidera data till ett enda organisations-ID.</li><li>Alla affärsenheter skulle ha samma infrastruktur för alla program (Experience Platform, Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics).</li><li>Guardrails: Vissa är globala per organisation, till exempel segmentering för direktuppspelning, som är 1,5 000 RPS.</li><li>GDPR-begäranden fungerar på organisationsnivå och kan inte riktas till särskilda sandlådor.</li><li>Kundhanterade nycklar anges på nivå för organisations-ID - alla sandlådor för affärsenheter skulle dela samma krypteringsnyckel med den här metoden.</li><li>Kommer att kräva tydlighet i företagslicensiering i DX och CC för att se till att programmen tillhandahålls i rätt organisations-ID.</ul></li> |

**Fördelar och överväganden**

Flera organisations-ID:n styr användaråtkomst, rättigheter och datasegmentering på organisationsnivå jämfört med ett enda organisations-ID, som styr på sandlådenivå.

| Scenario/Krav | Flera organisations-ID | Flera sandlådor (ID för en organisation) |
| ----------------------------------- | --------------------------------------------------- | ----------------------------------------------- |
| Datastorlek | Fullständigt isolerings- och regionspecifika organisations-ID:n | Enregionsdistribution |
| Datastyrning och isolering | Fullständig separation och isolering | Operativ isolering, delat organisations-ID |
| Efterlevnadshantering (t.ex. GDPR) | Separata begäranden per organisations-ID | En begäran gäller för alla sandlådor |
| Infrastrukturkostnader och licensiering | Kan vara högre på grund av dubblettinställningar | Normalt lägre med centraliserad administration |
| Global rapportering och aktivering | Utmaning på grund av isolerade miljöer | Enklare rapportering och aktivering över flera regioner |
| Administrativ komplexitet | Högre på grund av flera isolerade organisations-ID:n | Lägre, centraliserad administration |

## Sammanfattning

Experience Platform ger ett robust ramverk för att centralisera, styra och aktivera kunddata i flera olika affärsmodeller för olika varumärken. Rapporten har utforskat viktiga distributionsstrategier, styrningsmodeller och bästa praxis för att optimera Experience Platform-implementering för organisationer med olika dataisolerings- och driftbehov.

## Viktiga uppgifter

1. **Flexibla distributionsmodeller**

   - Företag kan välja mellan **enkel sandlåda, flera sandlådor eller hybridmetoder** baserat på sina drifts-, kompatibilitets- och styrningskrav.

   - **Globala organisationer** kan kräva flera produktionssandlådor för att uppfylla styrningskrav samtidigt som verksamhetseffektiviteten bibehålls.

2. **Datastyrning och åtkomstkontroll**

   - **Attributbaserad åtkomstkontroll, åtkomstkontroll på fältnivå och åtkomstkontroll på objektnivå** möjliggör exakt styrning av dataåtkomst.

   - Du måste definiera **tydliga roller och behörigheter** för olika profiler (t.ex. marknadsförare, dataarkitekter och IT-team) för att säkerställa korrekt dataanvändning.

3. **Verktyg och automatisering i sandlådan**

   - **Sandlådeverktyg** förenklar konfigurationshanteringen, vilket gör att team kan exportera och importera inställningar på ett effektivt sätt.

   - **API-baserad automatisering** är ett tillgängligt alternativ för företag som vill effektivisera sandlådedistributioner och styrning i stor skala.

4. **Globala strategier för rapportering och aktivering**

   - Företag som använder **Customer Journey Analytics** måste ta hänsyn till datasynkronisering och affärsmässiga konsekvenser när globala rapporter konsolideras.

   - **Segmentmatchning** innehåller en sekretesskompatibel mekanism för målgruppsdelning över sandlådor, vilket säkerställer sömlösa marknadsföringsaktiveringar.

5. **ID:n för flera organisationer jämfört med hänsyn till flera sandlådor**

   - Du måste noggrant bedöma om **flera organisations-ID:n eller flera sandlådor** ska distribueras baserat på datastorlek, efterlevnad och driftbehov.

   - **Organisations-ID** erbjuder fullständig isolering&#x200B;**, medan flersandlådeinställningar ger operativ flexibilitet i ett delat styrningsramverk**.

## Sluttankar

När företag anpassar sina funktioner för digitala upplevelser fungerar Experience Platform som en grundläggande plattform för datadriven marknadsföring, kundanalys och flerkanalsaktiveringar. För en lyckad implementering krävs noggrann planering av **sandlådestyrning, efterlevnadsprinciper och operativa arbetsflöden** för att säkerställa långsiktig effektivitet och skalbarhet.

Genom att utnyttja de bästa metoderna som beskrivs i det här vitboken kan du **optimera Experience Platform för åtgärder för flera varumärken och flera regioner**, vilket säkerställer smidig datahantering, regelefterlevnad och personaliserade kundupplevelser i stor skala.

## Bekräftelse

Rapporten har tagits fram med insikter och feedback från ämnesexperter i olika team, vilket ger korrekthet, tydlighet och praktisk vägledning. Vi tackar alla kolleger för deras värdefulla synpunkter och kommentarer. Deras expertis har hjälpt till att förfina detta dokument för att bättre kunna hjälpa företag som implementerar Adobe Experience Platform i miljöer med flera varumärken och regioner.
