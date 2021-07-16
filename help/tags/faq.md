---
title: 'Vanliga frågor och svar '
description: Få svar på vanliga frågor om taggar i Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Felsökningsguide för taggar

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](./term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Det här dokumentet innehåller svar på vanliga frågor om taggar i Adobe Experience Platform.

## Vad är taggar?

Taggar är nästa generation av tagghanteringsfunktioner från Adobe, som är inbyggda i Adobe Experience Platform. Taggar gör att klienter kan:

- Distribuera webbprodukter på klientsidan med integreringar som kallas *tillägg*
- Leverera dynamiskt konfigurationer för att uppdatera klientimplementeringar i inbyggda mobilprogram
- Inhämta, definiera, hantera och dela data konsekvent mellan marknadsförings- och annonsprodukter från andra leverantörer och från Adobe

Taggar är ett avancerat kod- och konfigurationsleveranssystem som utvärderar villkor och utför åtgärder för att effektivt distribuera bibliotek och produkter på klientsidan. De erbjuder också en mycket skalbar metod för att hantera och bygga integreringar och har en robust uppsättning API:er för programmatisk interaktion.

## Hur mycket kostar taggar?

Inga extra kostnader för taggar. De är tillgängliga för alla [!DNL Adobe Experience Cloud]-kunder.

## Jag hörde att det finns plugins nu. Vad handlar det om?

Taggar är inbyggda i Adobe Experience Platform och kan utökas. Kunder, Adobe-partners, byråer och leverantörer av marknadsförings- eller annonseringsteknologier kan bygga ett taggtillägg som lägger till nya funktioner eller ändrar befintliga funktioner. Systemet gör att partners och kunder kan skapa, hantera och uppdatera sina egna integreringar. Detta är bara ett sätt som Adobe öppnar upp Adobe Experience Platform så att kunder och partners kan bygga produkter och företag på det. Detta hjälper alla att enklare koppla Adobe-tekniken till marknadsförings- och marknadsföringsteknologierna från andra leverantörer.

## Kommer alla tillägg från tredje part att vara tillgängliga direkt?

Det finns redan tillägg för lösningar från Adobe och ett stort och växande antal oberoende leverantörer och tekniker inom analys, marknadsföring, annonsering och medgivande. Vi fortsätter att samarbeta med våra partners för att utöka ekosystemet. Eftersom programtilläggen kan byggas, hanteras och uppdateras av teknikägarna behöver kunderna inte vänta på att Adobe ska konstruera dem.

## När kan kunder och partners bygga tillägg?

Taggar har öppnat sin i stort sett självbetjäningsportal, som utvecklare kan använda för att bygga egna integreringar med Adobe Cloud Platform.

Vi har många kunder som också väljer att bygga egna privata tillägg som bara ska användas i de egna företagen med samma utvecklingsmetoder.

## Uppfyller taggarna mitt företags säkerhetsstandarder?

Taggar är klara för SOC-2 och Gramm-Leach-Bliley Act. Taggar kan också användas som värdtjänst. JavaScript-bibliotek och mobila konfigurationer kan hanteras från dina egna servrar eller det CDN som du väljer. För I.T. och säkerhetsteam ger er möjlighet att köra automatiserad testning, checka in filerna i ert eget versionskontrollsystem och helt följa alla interna produktionsmigreringsprocesser, säkerhetsrelaterade eller andra.

## När kan jag gå till taggar?

Nu är det bästa tillfället att gå över till taggar. Migreringsprocessen gör det enkelt att kopiera DTM-egenskaper till taggar. Vi rekommenderar omfattande testning, men vi har automatiserat så mycket vi kan (inga sidinbäddade kodändringar och automatiserad migrering av regler och dataelement).

## Har taggarna stöd för single-page-appar och mitt favoritramverk?

Ja. Taggar kan ge användare och tilläggsutvecklare flexibilitet när det gäller att samla in, hantera och distribuera data i ensidiga programupplevelser eller Ajax-tunga sidor eller webbplatser. Detta gäller oavsett dina utvecklingsramverksinställningar, oavsett om det är Angular, React.js, Ember, Meteor osv.

## Stöder taggar dynamiska datalager?

Ja. Taggar innehåller ett tillägg som specialiserar sig på att lyssna efter ändringar i dynamiska datalager.

## Vilka händelsetyper stöder taggarna?

Händelsetyper är tillgängliga via tillägg. Hur många händelsetyper som stöds varierar beroende på tillägg. YouTube-tillägget innehåller till exempel fyra videohändelsetyper: spela upp, pausa, avsluta och spela upp. Tack vare tillägg kan taggar ha stöd för andra händelsetyper i webbläsaren eller syntetiska händelsetyper, som specifika aktivitetssekvenser för besökare.

## Kommer taggarna att göra webbplatsen snabbare (eller göra den långsammare)?

Taggar är utformade för att leverera och köra marknadsförings- och annonstekniker på er webbplats så effektivt som möjligt med dagens bästa praxis. När de används på rätt sätt har taggar visat sig förbättra prestanda för webbplatser jämfört med alternativa metoder som erbjuder liknande funktionalitet.

## Vilka webbläsare stöder taggarna?

Webbläsarstöd för taggar:

- [!DNL Chrome] (senaste)
- [!DNL Safari] (senaste)
- [!DNL Firefox] (senaste)
- [!DNL Microsoft Edge] (senaste)
- [!DNL Internet Explorer] (10 och senare)
- [!DNL iOS Safari] (senaste)
- [!DNL Android Chrome] (senaste)

Webbläsarstöd för taggprogrammets gränssnitt:

- [!DNL Chrome] (senaste)
- [!DNL Safari] (senaste)
- [!DNL Firefox] (senaste)
- [!DNL Microsoft Edge] (senaste)

De flesta Adobe-kunder använder moderna webbplattformsfunktioner i sina webbläsare för att skapa bättre användarupplevelser, inklusive ensidiga applikationer och interaktiva Ajax-tunga webbplatser och sidor. När de flesta kunder övergår till mer moderna metoder med sina webbplatser kräver de en lösning som liknar taggar som möjliggör dessa strategier.

## Fungerar taggar i inbyggda mobilappar?

Ja! Taggar har nu stöd för mobila egenskaper och konfigurationer för nya Adobe Experience Platform [SDK:er för mobiler](https://sdkdocs.com) för att implementera datainsamling och leverans i en intern mobilappsmiljö. Mer information finns i [dokumentationen](https://sdkdocs.com).

## Vad händer om jag har andra frågor?

Om du har andra frågor kan du ställa dem i Adobe Community på sidan med huvudtaggar på [https://adobe.com/go/launchme](https://adobe.com/go/launchme).

Taggar är bara ett exempel på var vår plattform är på väg: mer öppen, mer integrerad och som alltid är inriktad på att lyckas med kunderna.
