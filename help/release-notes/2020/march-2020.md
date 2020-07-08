---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 mars 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [Datastyrning](#governance)
* [Dataintag](#ingestion)
* [Mål](#destinations)
* [Identitetstjänst](#identity)
* [Källor](#sources)

## Datastyrning {#governance}

Med Experience Platform kan företag samla data från flera affärssystem för att bättre kunna identifiera, förstå och engagera kunder. Experience Platform har en komplett infrastruktur för datastyrning, inklusive märkning och verkställighet av data (DULE), för att säkerställa att data används på rätt sätt inom Platform och när de delas mellan system.

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en nyckelroll på olika nivåer inom Experience Platform, bland annat för katalogisering, datalinje, märkning av dataanvändning, dataåtkomstregler och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

>[!NOTE]
>
>Vissa av följande nya funktioner är för närvarande betaversioner och är inte tillgängliga för alla användare. Betafunktionerna kan komma att ändras.

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatiserad tillämpning av dataanvändningsprinciper för kunddata i realtid Platform | Dataanvändningsprinciper används nu i arbetsflödet för att aktivera data till mål. Datastyrning bäddas också in och tillämpas när du gör ändringar som påverkar befintliga aktiveringar (t.ex. ändringar i datauppsättningsrubriker, sammanfogningsprinciper, segmentdefinitioner). |
| Datalinje för verkställighet | När en dataanvändningsprincip överträds i CDP i realtid visar gränssnittet ett meddelande som innehåller information om datalänkning som hjälper användaren att förstå varför policyer överträds och vad de kan göra för att åtgärda överträdelsen. |


**Kända fel**

* Ingen

Mer information om datastyrning finns i översikten över [datastyrning](../../data-governance/home.md).

## Dataintag {#ingestion}

Adobe Experience Platform har en mängd funktioner för att importera alla typer av data och fördröjningar. Adobe Experience Platform Data Ingtake erbjuder flera alternativ för datainhämtning, inklusive Batch-API:er, direktuppspelnings-API:er, inbyggda Adobe-anslutningar, dataintegrationspartners eller användargränssnittet i Adobe Experience Platform.

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Partiellt batchintag | Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som alla felaktiga data grupperas separat. Information läggs till i misslyckade batchar för att förklara varför de inte klarade valideringen. Mer information om partiell batchförbrukning finns i dokumentationen för [partiell batchförbrukning](../../ingestion/batch-ingestion/partial.md). |

**Kända fel**

* Ingen

Läs mer om hur du importerar data till Platform i dokumentationen för [datainmatning](../../ingestion/home.md).


## Mål {#destinations}

I [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Det finns nya destinationer där du kan aktivera data från Adobe Experience Platform. Mer information finns nedan:

| Destination | Beskrivning |
|--- | ---|
| Lagringsmål i molnet | Adobe CDP kan nu i realtid leverera era segment som datafiler till Amazon S3- eller SFTP-molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer. |
| Annonsmål | Googles målkort är nu uppdelat i tre målkort för de tre olika Google-plattformarna som för närvarande stöds i Adobe Real-time CDP: Google Ads, Google Ad Manager, Google Display och Video 360. |

Mer information finns på [destinationsöversikten](../../rtcdp/destinations/destinations-overview.md)

## Identity Service {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrat privat diagram | Funktionen för privata diagram har förbättrats för att minska tidsfördröjningen för diagramgenerering från en gruppbearbetning varje vecka till ett dagligt uppdaterat diagram, så att identitetstjänstkunder kan få tillgång till mer aktuella identitetsdiagram och länkar. |

**Kända fel**

* Ingen

Mer information om identitetstjänsten finns i Översikt över [identitetstjänsten](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Undertryckta signaler för koppling till Adobe Audience Manager | Signalnivådata från Audience Manager kommer inte längre att skickas. Observera att segmentmedlemskap för Traits and Segments fortfarande inkluderas. Till följd av den här ändringen kommer inkommande datauppsättningar inte längre att genereras. |
| Ändrade namn på datauppsättningar | Datauppsättningar som genereras av Audience Manager-kopplingen har uppdaterade namn och beskrivningar. |
| Aktivera profilväxling i Audience Manger | Profilväxling kan aktiveras eller inaktiveras för att befordra datauppsättningen till kundprofilen i realtid. Växla aktiveras som standard. |
| Användargränssnittsstöd för molnlagringssystem | Ny källanslutning för Azure Data Lake Storage Gen2 i gränssnittet. |
| Gränssnittsstöd för CRM-system | Ny källanslutning för HubSpot, Salesforce Service Cloud och ServiceNow i användargränssnittet. |
| Användargränssnittsstöd för databassystem | Ny källanslutning för AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server och MySQL i användargränssnittet. |

**Kända fel**

* Ingen

Mer information om källor finns i [Källöversikt](../../sources/home.md).