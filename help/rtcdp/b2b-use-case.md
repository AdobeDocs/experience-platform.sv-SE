---
keywords: RTCDP;CDP;Real-time Customer Data Platform;realtids kunddataplattform;realtids-cdp;cdp;rtcdp
title: Exempel på användningsfall för Real-time Customer Data Platform B2B Edition
description: Det här exempelscenariot är ett exempel på hur du konfigurerar implementeringen av Adobe Real-Time Customer Data Platform B2B Edition.
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# Exempel på användningsfall för Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition utökar de befintliga erbjudandena från Real-Time CDP och Adobe Experience Platform med stöd för B2B-data och arbetsflöden. Det här dokumentet innehåller ett exempel på hur man kan använda B2B-versionen för att demonstrera de ytterligare fördelarna. De omfattar följande:

- Kombinera person- och kontodata från olika externa datakällor för att skapa en heltäckande bild som ger en bättre förståelse för kunderna och mer korrekt segmentering. Läs dokumentationen om [skapa XDM-schemarelationer](./schemas/b2b.md) för användning med olika B2B-källor för mer information.
- Segmentera en målgrupp baserat på attribut för relaterade enheter. Detta inkluderar konton, säljprojekt, kampanjer och marknadsföringslistor. Segment begränsas inte längre till bara personattribut och upplevelsehändelser. Se [Dokumentation för B2B-segmentering](./segmentation/b2b.md) för fler exempel på hur man skapar B2B-specifika målgrupper.
- Inbyggt stöd för användning av en person som är relaterad till flera konton.

## Användningsfall

Bodea, ett teknikföretag, har en ny produkt och vill samtidigt rikta sig till kunder med ett e-postmeddelande och en reklamkampanj från LinkedIn. För att maximera effektiviteten i marknadsföringskampanjen vill Bodea även rikta sig till de personer som är kopplade till det befintliga kontot som har spenderat över en miljon dollar på sina produkter tidigare OCH som har besökt den nya produktsidan den senaste månaden.

Bodea har dock två olika verksamhetsområden. Bodeas första affärsområde &quot;Line 1&quot; skapar programvara för bilindustrin. Företagets andra verksamhetsområde,&quot;Line 2&quot;, säljer 3D-skrivare som skapar fordonsdelar. Till följd av Bodeas två verksamhetsområden är de intäktsdata som genereras från Bodeas kundkonton inte samlade i en enda vy.

Varje affärsgren har ett eget försäljningssystem: CRM 1 och CRM 2. Båda dessa CRM-säljsystem är kopplade till sin egen automatiseringsplattform för marknadsföring,&quot;Marketo 1&quot; och&quot;Marketo 2&quot;. Data från CRM 1 synkroniseras endast till Marketo 1 och data från CRM2 synkroniseras endast till Marketo 2. Deras data lagras i olika informationsisoleringar.

## Aktuell datasituation

Eftersom båda affärsgrenarna av Bodeas affärsverksamhet säljer till Townsend-företaget registreras Townsend-affärsdata som två separata konton i varje försäljningssystem.

I Marketo 1 registreras Townsend som Konto 1. Den har två samhörande personer (p1@townsend.com och p2@townsend.com) och en sluten möjlighet på 200 kB (&quot;säljprojekt 1&quot;) i CRM 1. Dessa data synkroniseras från CRM 1 till Marketo 1.

I Marketo 2 registreras Townsend som Konto 2. Konto 2 har också två samhörande personer (p2@townsend.com och p3@townsend.com) och en sluten möjlighet på 900 kB (&quot;säljprojekt 2&quot;) i CRM 2. Dessa data synkroniseras från CRM 2 till Marketo 2.

För integrerings- och kontrolländamål har Bodea också ett system för Överordnad Data Management (MDM) där man har en post som anger att konto 1 i Marketo 1 (och CRM 1) och konto 2 i Marketo 2 (och CRM 2) är samma företag.

Under den senaste månaden `p2@townsend.com` besökte den nya produktsidan och webbbesöket spelades in av Marketo 1.

![kontoinformationsdiagram](./assets/account-info.png)

## Problemet

Rad 1 har just släppt en ny programprodukt och vill sälja in den i Bodeas befintliga toppskiktskundbas. Bodea lanserar en marknadsföringskampanj med den specifika målgruppen i åtanke.

Eftersom relevant Townsend-information registreras som Konto 1 i Marketo 1 och Konto 2 i Marketo 2 kan Bodeas marknadsföringsteam inte utnyttja den isolerade informationen effektivt.

Det förhindrar Bodeas marknadsföringsteam från att effektivt rikta in specifika affärskontakter på dessa företag med denna nya möjlighet.

Till dags dato har Townsend spenderat över en miljon dollar på Bodea-produkter på alla sina konton. Ett segment som skapats med det gamla systemet skulle dock inte omfatta någon från Townsend om inte den totala kostnaden inom ett enda försäljningssystem uppgick till mer än en miljon dollar. Detta beror på att intäktsinformationen är indelad i konton i olika försäljningssystem.

Eftersom Townsend utgifter delas upp i olika försäljningssystem och inte totalt mer än en miljon per styck, hittar segmentet inte någon som är kvalificerad i Marketo 1 eller Marketo 2.

### Hur Real-Time CDP B2B Edition löser problemet

Med Real-Time CDP B2B Edition kan Bodeas marknadsföringsteam

- Kombinera data från olika källor (olika instanser av Marketo och CRM samt Överordnad Data Management) till Real-Time CDP B2B Edition.

Med RT-CDP B2B Edition kan Bodea använda Marketo Engage Source Connector för att hämta B2B-data från Marketo 1 och Marketo 2 till Experience Platform och hålla dessa data aktuella med plattformsanslutna applikationer. Se [Marketo källanslutning](../sources/connectors/adobe-applications/marketo/marketo.md) mer information.

B2B-data (personer, konton, säljprojekt och aktiviteter) från CRM1 synkroniseras till Marketo 1. På samma sätt synkroniseras alla B2B-data från CRM 2 till Marketo 2. De synkas till Adobe Experience Platform via Marketo källanslutning. Om Bodea vill hämta ytterligare data från en CRM till Experience Platform kan de använda befintliga CRM Connectors.

För enkelhetens skull och i det här exemplet identifieras människor av sina e-postmeddelanden. De kombinerade kontouppgifterna för det här exemplet ser ut så här:

| Personer |
|---|
| p1@townsend.com |
| p2@townsend.com (som besökte den nya produktsidan förra månaden) |
| p3@townsend.com |

| Affärsmöjligheter (vunna) |
|---|
| Möjligheter 1, 200 000 dollar |
| Möjlighet 2, 900 000 dollar |

- Skapa unika segment med hjälp av denna sammanställda information för olika marknadsföringssatsningar. I det här exemplet hittar segmentet alla personer som:

   - Har associerade möjligheter (mellan ALLA konton) som överstiger 1 miljon dollar i värde
   - OCH
   - Har besökt produktsidan den senaste månaden

- Skapa en målgrupp som är de mest effektiva mottagarna av Bodeas nya marknadsföringskampanj. I det här exemplet hjälper RT-CDP, B2B Edition marknadsföraren att identifiera `p2@townsend.com` som det rätta målet för denna marknadsföringskampanj.

Genom att använda destinationerna Marketo Engage och LinkedIn har Bodea en totallösning för kundupplevelsehantering (CXM) för marknadsföringsteamet. Den målgrupp som skapas i Experience Platform flyttas till Marketo-målet där den visas som en statisk lista. Den här målgruppen läggs sedan automatiskt till i en marknadsföringskampanj från Marketo. Samtidigt kan målgruppen även skickas till en marknadsföringskampanj från LinkedIn via RT-CDP B2B Edition.

## Nästa steg

Genom att läsa det här dokumentet har du nu introducerats till de typer av mål och problem som kan lösas med Real-Time CDP B2B Edition.

Följande dokumentation rekommenderas för att förbättra din förståelse av B2B-specifika funktioner:

- [Real-time Customer Data Platform B2B Edition - komplett självstudiekurs](./b2b-tutorial.md)
- [Källor i Real-time Customer Data Platform B2B Edition](./sources/b2b.md)
- [Scheman i Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Exempel på B2B-segmentering](./segmentation/b2b.md)
- [Kontoprofiler - översikt](./accounts/account-profile-overview.md)
- [Destinationer i Real-time Customer Data Platform B2B Edition](./destinations/b2b.md)
- [Konfigurera ett mål för LinkedIn Matched Auditions](../destinations/catalog/social/linkedin.md)
