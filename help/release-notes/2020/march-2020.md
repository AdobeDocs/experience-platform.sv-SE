---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 mars 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [!DNL Data Governance](#governance)
* [!DNL Data Ingestion](#ingestion)
* [!DNL Destinations](#destinations)
* [!DNL Identity Service](#identity)
* [!DNL Sources](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] gör det möjligt för företag att samla data från flera företagssystem för att bättre kunna identifiera, förstå och engagera kunder. [!DNL Experience Platform] omfattar en infrastruktur för datastyrning från början till slut, inklusive märkning och verkställighet av data (DULE), för att säkerställa att data används på rätt sätt inom [!DNL Platform] och när de delas mellan system.

Adobe Experience Platform [!DNL Data Governance] är ett antal strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Det spelar en viktig roll på [!DNL Experience Platform] olika nivåer, bland annat i fråga om katalogisering, datalinje, etikettering av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

>[!NOTE]
>
>Vissa av följande nya funktioner är för närvarande betaversioner och är inte tillgängliga för alla användare. Betafunktionerna kan komma att ändras.

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatiserad tillämpning av dataanvändningsprinciper för [!DNL Real-time Customer Data Platform] | Dataanvändningsprinciper används nu i arbetsflödet för att aktivera data till mål. [!DNL Data Governance] är också inbäddat och framtvingat när du gör ändringar som påverkar befintliga aktiveringar (t.ex. ändringar i datauppsättningsrubriker, sammanfogningsprinciper, segmentdefinitioner). |
| Datalinje för verkställighet | När en dataanvändningsprincip överträds i CDP i realtid visar gränssnittet ett meddelande som innehåller information om datalänkning som hjälper användaren att förstå varför policyer överträds och vad de kan göra för att åtgärda överträdelsen. |


**Kända fel**

* Ingen

Mer information om [!DNL Data Governance]finns i översikten över [datastyrning](../../data-governance/home.md).

## Dataintag {#ingestion}

Adobe Experience Platform har en mängd funktioner för att importera alla typer av data och fördröjningar. Adobe Experience Platform [!DNL Data Ingestion] erbjuder flera alternativ för datainhämtning, inklusive API:er för gruppbearbetning, API:er för direktuppspelning, inbyggda Adobe-anslutningar, dataintegrationspartners eller användargränssnittet för Adobe Experience Platform.

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
| Lagringsmål i molnet | Adobe CDP kan nu i realtid leverera era segment som datafiler till era [!DNL Amazon S3] - eller SFTP-molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer. |
| Annonsmål | Målkortet delas nu upp i tre destinationskort för de tre olika [!DNL Google] [!DNL Google] plattformar som för närvarande stöds i Adobe Real-time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Mer information finns på [destinationsöversikten](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteterna mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid. [!DNL Identity Service]

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrat privat diagram | Funktionen för privata diagram har förbättrats för att minska tidsfördröjningen för generering av diagram från veckovis batchbearbetning till ett dagligt uppdaterat diagram, så att [!DNL Identity Service] kunderna kan få tillgång till mer aktuella identitetsdiagram och länkar. |

**Kända fel**

* Ingen

Mer information om [!DNL Identity Service]finns i [Översikt över](../../identity-service/home.md)identitetstjänsten.

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Undertryckta signaler för koppling till Adobe Audience Manager | Signalnivådata från Audience Manager kommer inte längre att skickas. Observera att segmentmedlemskap för Traits and Segments fortfarande inkluderas. Till följd av den här ändringen kommer inkommande datauppsättningar inte längre att genereras. |
| Ändrade namn på datauppsättningar | Datauppsättningar som genereras av Audience Manager-kopplingen har uppdaterade namn och beskrivningar. |
| Aktivera [!DNL Profile] växling i Audience Manger | [!DNL Profile] växlingsknappen kan aktiveras eller inaktiveras för att befordra datauppsättningen till [!DNL Real-time Customer Profile]. Växla aktiveras som standard. |
| Användargränssnittsstöd för molnlagringssystem | Ny källkoppling för [!DNL Azure Data Lake Storage Gen2] i användargränssnittet. |
| Gränssnittsstöd för CRM-system | Ny källkoppling för [!DNL HubSpot], [!DNL Salesforce Service Cloud]och [!DNL ServiceNow] i användargränssnittet. |
| Användargränssnittsstöd för databassystem | Ny källkoppling för [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]och [!DNL MySQL] i användargränssnittet. |

**Kända fel**

* Ingen

Mer information om källor finns i [Källöversikt](../../sources/home.md).