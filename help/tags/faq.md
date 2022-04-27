---
title: Tags Troubleshooting Guide
description: Få svar på vanliga frågor om taggar i Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: c21699af0d08d0f63562910e2174273f0a139538
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---

# Felsökningsguide för taggar

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Several terminology changes have rolled out across the product documentation as a result. Please refer to the following [document](./term-updates.md) for a consolidated reference of the terminology changes.

Det här dokumentet innehåller svar på vanliga frågor om taggar i Adobe Experience Platform.

## What are tags?

Taggar är nästa generation av tagghanteringsfunktioner från Adobe, som är inbyggda i Adobe Experience Platform. Taggar gör att klienter kan:

- Deploy client-side web products using integrations called *extensions*
- Dynamically deliver configuration to update client implementations in native mobile applications
- Inhämta, definiera, hantera och dela data konsekvent mellan marknadsförings- och annonsprodukter från andra leverantörer och från Adobe

Taggar är ett avancerat kod- och konfigurationsleveranssystem som utvärderar villkor och utför åtgärder för att effektivt distribuera bibliotek och produkter på klientsidan. They also provides a highly scalable approach to managing and building integrations and has a robust set of APIs for programmatic interaction.

## How much do tags cost?

Inga extra kostnader för taggar. De är tillgängliga för alla [!DNL Adobe Experience Cloud] kund.

## Jag hörde att det finns plugins nu. Vad handlar det om?

Tags are built into the Adobe Experience Platform and are fully extensible. Customers, Adobe Partners, agencies, and marketing or advertising technology vendors can build a tag extension that adds new functionality or modifies existing functionality. Systemet gör att partners och kunder kan skapa, hantera och uppdatera sina egna integreringar. This is just one way Adobe is opening up the Adobe Experience Platform so customers and partners can build products and businesses on it. Detta hjälper alla att enklare koppla Adobe-tekniken till marknadsförings- och marknadsföringsteknologierna från andra leverantörer.

## Kommer alla tillägg från tredje part att vara tillgängliga direkt?

Extensions are already available for Adobe solutions and a large and growing number of independent analytics, marketing, advertising, and consent vendors and technologies. We continue to work with our partners to expand the ecosystem. Eftersom programtilläggen kan byggas, hanteras och uppdateras av teknikägarna behöver kunderna inte vänta på att Adobe ska konstruera dem.

## När kan kunder och partners bygga tillägg?

Tags have opened its virtually self-service portal, which extension developers can use to build their own integrations with the Adobe Cloud Platform.

We have many customers who also choose to build their own private extensions for use only within their own companies using the same extension development methods.

## Uppfyller taggarna mitt företags säkerhetsstandarder?

Taggar är klara för SOC-2 och Gramm-Leach-Bliley Act. Taggar kan också användas som värdtjänst. JavaScript-bibliotek och mobila konfigurationer kan hanteras från dina egna servrar eller det CDN som du väljer. För I.T. och säkerhetsteam ger er möjlighet att köra automatiserad testning, checka in filerna i ert eget versionskontrollsystem och helt följa alla interna produktionsmigreringsprocesser, säkerhetsrelaterade eller andra.

## När kan jag gå till taggar?

Nu är det bästa tillfället att gå över till taggar. Migreringsprocessen gör det enkelt att kopiera DTM-egenskaper till taggar. Vi rekommenderar omfattande testning, men vi har automatiserat så mycket vi kan (inga sidinbäddade kodändringar och automatiserad migrering av regler och dataelement).

## Har taggarna stöd för single-page-appar och mitt favoritramverk?

Ja. Taggar kan ge användare och tilläggsutvecklare flexibilitet när det gäller att samla in, hantera och distribuera data i ensidiga programupplevelser eller Ajax-tunga sidor eller webbplatser. Detta gäller oavsett dina utvecklingsramverksinställningar, oavsett om det är Angular, React.js, Ember, Meteor osv.

## Do tags support dynamic data layers?

Ja. Taggar innehåller ett tillägg som specialiserar sig på att lyssna efter ändringar i dynamiska datalager.

## Vilka händelsetyper stöder taggarna?

Händelsetyper är tillgängliga via tillägg. The amount of event types supported varies by extension. For example, the YouTube extension includes four video event types: play, pause, end, and time played. Tack vare tillägg kan taggar ha stöd för andra händelsetyper i webbläsaren eller syntetiska händelsetyper, som specifika aktivitetssekvenser för besökare.

## Will tags speed up (or slow down) my website?

Tags are designed to deliver and run marketing and advertising technologies on your website as efficiently as possible using today&#39;s best practices. När de används på rätt sätt har taggar visat sig förbättra prestanda för webbplatser jämfört med alternativa metoder som erbjuder liknande funktionalitet.

## Which browsers do tags support?

Webbläsarstöd för taggar:

- [!DNL Chrome] (latest)
- [!DNL Safari] (senaste)
- [!DNL Firefox] (senaste)
- [!DNL Microsoft Edge] (senaste)
- [!DNL Internet Explorer] (10 och senare)
- [!DNL iOS Safari] (latest)
- [!DNL Android Chrome] (senaste)

Webbläsarstöd för taggprogrammets gränssnitt:

- [!DNL Chrome] (senaste)
- [!DNL Safari] (senaste)
- [!DNL Firefox] (senaste)
- [!DNL Microsoft Edge] (latest)

De flesta Adobe-kunder använder moderna webbplattformsfunktioner i sina webbläsare för att skapa bättre användarupplevelser, inklusive ensidiga applikationer och interaktiva Ajax-tunga webbplatser och sidor. När de flesta kunder övergår till mer moderna metoder med sina webbplatser kräver de en lösning som liknar taggar som möjliggör dessa strategier.

## Do tags work on native mobile apps?

Ja! Taggar har nu stöd för mobila egenskaper och konfigurationer för nya Adobe Experience Platform [SDK för mobiler](https://sdkdocs.com) för att implementera datainsamling och -leverans i en intern mobilappsmiljö. Please visit [documentation](https://sdkdocs.com) to learn more.

## Varför står det att det uppstod ett fel när mitt konto lästes in?

Om du får ett meddelande om att det uppstod ett fel när ditt konto lästes in innebär det att ditt konto inte tillhör någon produktprofil för taggar. Se guiden [hantera behörigheter](./ui/administration/manage-permissions.md) om du vill lära dig hur du konfigurerar en produktprofil i Adobe Admin Console för att ge åtkomst till användargränssnittet i datainsamlingen.

## Varför kan jag inte lägga till några egenskaper i gränssnittet?

Om du inte kan skapa några nya egenskaper när du är inloggad i användargränssnittet för datainsamling innebär det att ditt konto inte tillhör en produktprofil som har behörigheten Hantera egenskaper.

Se guiden [hantera behörigheter](./ui/administration/manage-permissions.md) om du vill lära dig hur du konfigurerar en produktprofil i Adobe Admin Console för att ge rättigheten Hantera egenskaper. Mer information om de olika rättigheterna för taggar finns i översikten på [användarbehörigheter för taggar](./ui/administration/user-permissions.md).

## What if I have other questions?

Om du har andra frågor kan du ställa på [Adobe Experience Platform Data Collection - communitysida](https://adobe.com/go/launchme) på Experience League eller gå med [officiell Slack-grupp för tagghanterare](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).
