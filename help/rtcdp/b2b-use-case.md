---
keywords: RTCDP;CDP;Real-Time Customer Data Platform;kunddataplattform i realtid;cdp i realtid;cdp;rtcdp
title: Exempel på användningsfall för Real-Time Customer Data Platform B2B edition
description: Det här exempelscenariot är ett exempel på hur du konfigurerar implementeringen av Adobe Real-Time Customer Data Platform B2B Edition.
feature: Get Started, Use Cases, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 1%

---

# Exempel på användningsfall för Real-Time Customer Data Platform B2B edition

Real-Time Customer Data Platform B2B edition utökar möjligheterna med Real-Time CDP och Adobe Experience Platform för att stödja B2B-data och arbetsflöden. Det här dokumentet innehåller ett exempel på hur du kan utnyttja B2B edition ytterligare. De omfattar följande:

- Kombinera person- och kontodata från olika externa datakällor för att skapa en heltäckande bild som ger en bättre förståelse för kunderna och mer korrekt segmentering. Mer information finns i dokumentationen om [att skapa XDM-schemarelationer](./schemas/b2b.md) som kan användas med olika B2B-källor.
- Segmentera en målgrupp baserat på attribut för relaterade enheter. Detta inkluderar konton, säljprojekt, kampanjer och marknadsföringslistor. Publiken begränsas inte längre till bara personattribut och upplevelsehändelser. Se [B2B-segmenteringsdokumentationen](./segmentation/b2b.md) för fler exempel på hur du skapar B2B-specifika målgrupper.
- Inbyggt stöd för användning av en person som är relaterad till flera konton.

## Användningsfall

Bodea, ett teknikföretag, har en ny produkt och vill samtidigt rikta sig till kunder med ett e-postmeddelande och en LinkedIn-reklamkampanj. För att maximera effektiviteten i marknadsföringskampanjen vill Bodea även rikta sig till de personer som är kopplade till det befintliga kontot som har spenderat över en miljon dollar på sina produkter tidigare OCH som har besökt den nya produktsidan den senaste månaden.

Bodea har dock två olika verksamhetsområden. Bodeas första affärsområde &quot;Line 1&quot; skapar programvara för bilindustrin. Företagets andra verksamhetsområde,&quot;Line 2&quot;, säljer 3D-skrivare som skapar fordonsdelar. Till följd av Bodeas två verksamhetsområden är de intäktsdata som genereras från Bodeas kundkonton inte samlade i en enda vy.

Varje affärsgren har ett eget försäljningssystem: &quot;CRM 1&quot; och &quot;CRM 2&quot;. Båda dessa CRM-system är kopplade till sin egen automatiseringsplattform för marknadsföring,&quot;Marketo 1&quot; och&quot;Marketo 2&quot;. Data från CRM 1 synkroniseras endast till Marketo 1 och data från CRM2 synkroniseras endast till Marketo 2. Deras data lagras i olika informationsisoleringar.

## Aktuell datasituation

Eftersom båda affärsgrenarna av Bodeas affärsverksamhet säljer till Townsend-företaget registreras Townsend-affärsdata som två separata konton i varje försäljningssystem.

I Marketo 1 registreras Townsend som Konto 1. Den har två samhörande personer (p1@townsend.com och p2@townsend.com) och en sluten möjlighet på 200 kB (&quot;säljprojekt 1&quot;) i CRM 1. Dessa data synkroniseras från CRM 1 till Marketo 1.

I Marketo 2 registreras Townsend som Konto 2. Konto 2 har också två samhörande personer (p2@townsend.com och p3@townsend.com) och en sluten möjlighet på 900 kB (&quot;säljprojekt 2&quot;) i CRM 2. Dessa data synkroniseras från CRM 2 till Marketo 2.

För integrerings- och kontrolländamål har Bodea också ett MDM-system (Master Data Management) där man har en post som anger att konto 1 i Marketo 1 (och CRM 1) och konto 2 i Marketo 2 (och CRM 2) är samma företag.

Under den senaste månaden besökte `p2@townsend.com` den nya produktsidan och webbbesöket spelades in av Marketo 1.

![kontoinformationsdiagram](./assets/account-info.png)

## Problemet

Rad 1 har just släppt en ny programprodukt och vill sälja in den i Bodeas befintliga toppskiktskundbas. Bodea lanserar en marknadsföringskampanj med den specifika målgruppen i åtanke.

Eftersom relevant Townsend-information registreras som Konto 1 i Marketo 1 och Konto 2 i Marketo 2 kan Bodeas marknadsföringsteam inte utnyttja den isolerade informationen på ett effektivt sätt.

Det förhindrar Bodeas marknadsföringsteam från att effektivt rikta in specifika affärskontakter på dessa företag med denna nya möjlighet.

Till dags dato har Townsend spenderat över en miljon dollar på Bodea-produkter på alla sina konton. Men en målgrupp som skapats med sitt gamla system skulle inte inkludera någon från Townsend om inte totalsumman för ett enda försäljningssystem uppgick till mer än en miljon dollar. Detta beror på att intäktsinformationen är indelad i konton i olika försäljningssystem.

Eftersom Townsend utgifter är fördelade över olika försäljningssystem och inte totalt mer än en miljon per styck, skulle segmentdefinitionen inte hitta någon som är kvalificerad i antingen Marketo 1 eller Marketo 2.

### Hur Real-Time CDP B2B edition löser problemet

Med Real-Time CDP B2B edition kan Bodeas marknadsföringsteam

- Kombinera data från alla olika källor (flera Marketo- och CRM-instanser samt Master Data Management) till Real-Time CDP B2B edition.

Med RT-CDP B2B edition kan Bodea använda Marketo Engage Source Connector för att hämta B2B-data från Marketo 1 och Marketo 2 till Experience Platform och hålla dessa data aktuella med Experience Platform-anslutna program. Mer information finns i dokumentationen för [Marketo-källanslutningen](../sources/connectors/adobe-applications/marketo/marketo.md).

B2B-data (personer, konton, säljprojekt och aktiviteter) från CRM1 synkroniseras till Marketo 1. På samma sätt synkroniseras alla B2B-data från CRM 2 till Marketo 2. De synkas till Adobe Experience Platform via Marketo källanslutning. Om Bodea däremot vill hämta ytterligare data från en CRM till Experience Platform kan de använda befintliga CRM Connectors.

För enkelhetens skull och i det här exemplet identifieras människor av sina e-postmeddelanden. De kombinerade kontouppgifterna för det här exemplet ser ut så här:

| Folk |
|---|
| p1@townsend.com |
| p2@townsend.com (som besökte den nya produktsidan den senaste månaden) |
| p3@townsend.com |

| Affärsmöjligheter (vunna) |
|---|
| Möjligheter 1, 200 000 dollar |
| Möjlighet 2, 900 000 dollar |

- Skapa unika målgrupper med hjälp av denna sammanställda information för olika marknadsföringssatsningar. I det här exemplet hittar segmentdefinitionen alla personer som:

   - Har associerade möjligheter (mellan ALLA konton) som överstiger 1 miljon dollar i värde
   - OCH
   - Har besökt produktsidan den senaste månaden

- Skapa en målgrupp som är de mest effektiva mottagarna av Bodeas nya marknadsföringskampanj. I det här exemplet, RT-CDP, hjälper B2B edition marknadsföraren att identifiera `p2@townsend.com` som rätt mål för den här marknadsföringskampanjen.

Genom att använda Marketo Engage och LinkedIn har Bodea en heltäckande lösning för hantering av kundupplevelser (CXM) för sitt marknadsföringsteam. Publiken som skapas i Experience Platform flyttas till Marketo-målet där det visas som en statisk lista. Den här målgruppen läggs sedan automatiskt till i en marknadsföringskampanj från Marketo. Samtidigt kan målgruppen även skickas till en LinkedIn-marknadsföringskampanj av RT-CDP B2B edition.

## Nästa steg

Genom att läsa det här dokumentet har du nu fått en introduktion till de typer av mål och problem som kan lösas med Real-Time CDP B2B edition.

Följande dokumentation rekommenderas för att förbättra din förståelse av B2B-specifika funktioner:

- [Real-Time Customer Data Platform B2B edition - en komplett självstudiekurs](./b2b-tutorial.md)
- [Källor i Real-Time Customer Data Platform B2B edition](./sources/b2b.md)
- [Scheman i Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
- [Exempel på B2B-segmentering](./segmentation/b2b.md)
- [Kontoprofiler - översikt](./accounts/account-profile-overview.md)
- [Destinationer i Real-Time Customer Data Platform B2B edition](./destinations/b2b.md)
- [Konfigurera ett LinkedIn Matched Auditions-mål](../destinations/catalog/social/linkedin.md)
