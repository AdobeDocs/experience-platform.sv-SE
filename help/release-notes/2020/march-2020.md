---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 11 mars 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 mars 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] gör det möjligt för företag att samla data från flera företagssystem för att bättre kunna identifiera, förstå och engagera kunder. [!DNL Experience Platform] omfattar en infrastruktur för total datastyrning som säkerställer korrekt användning av data inom [!DNL Platform] och när de delas mellan system.

Adobe Experience Platform [!DNL Data Governance] är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och regler som gäller för dataanvändning följs. Det spelar en viktig roll på [!DNL Experience Platform] olika nivåer, bland annat i fråga om katalogisering, datalinje, etikettering av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

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

Adobe Experience Platform har en omfattande uppsättning funktioner för att importera alla typer av data och fördröjningar. Adobe Experience Platform [!DNL Data Ingestion] erbjuder flera alternativ för datainhämtning, inklusive API:er för gruppbearbetning, API:er för direktuppspelning, Adobe-anslutningar, dataintegrationspartners eller Adobe Experience Platform användargränssnitt.

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Partiellt batchintag | Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som felaktiga data grupperas separat. Information läggs till i misslyckade batchar för att förklara varför de inte klarade valideringen. Mer information om partiell batchförbrukning finns i dokumentationen för [partiell batchförbrukning](../../ingestion/batch-ingestion/partial.md). |

**Kända fel**

* Ingen

Mer information om hur du hämtar data till Platform finns i dokumentationen [för](../../ingestion/home.md)datainmatning.


## Mål {#destinations}

I kunddataplattformen [i](../../rtcdp/overview.md)realtid är mål färdiga integreringar med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Det finns nya destinationer där du kan aktivera dina Adobe Experience Platform-data. Mer information finns nedan:

| Destination | Beskrivning |
|--- | ---|
| Lagringsmål i molnet | CDP kan nu leverera era segment som datafiler till era [!DNL Amazon S3] - eller SFTP-molnlagringsplatser i realtid. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer. |
| Annonsmål | Målkortet är nu [!DNL Google] uppdelat i tre destinationskort för de tre olika [!DNL Google] plattformar som för närvarande stöds i CDP i realtid: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Mer information finns på [destinationsöversikten](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrat privat diagram | Funktionen för privata diagram har förbättrats för att minska tidsfördröjningen för generering av diagram från veckovis batchbearbetning till ett dagligt uppdaterat diagram, så att [!DNL Identity Service] kunderna kan få tillgång till mer aktuella identitetsdiagram och länkar. |

**Kända fel**

* Ingen

Mer information om [!DNL Identity Service]finns i [Översikt över](../../identity-service/home.md)identitetstjänsten.

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Undertryckta signaler för Adobe Audience Manager Connector | Signalnivådata från Audience Manager kommer inte längre att skickas. Observera att segmentmedlemskap för Traits and Segments fortfarande inkluderas. Till följd av den här ändringen kommer inkommande datauppsättningar inte längre att genereras. |
| Ändrade namn på datauppsättningar | Datauppsättningar som genereras av Audience Manager-kopplingen har uppdaterade namn och beskrivningar. |
| Aktivera [!DNL Profile] växling i Audience Manger | [!DNL Profile] växlingsknappen kan aktiveras eller inaktiveras för att befordra datauppsättningen till [!DNL Real-time Customer Profile]. Växla aktiveras som standard. |
| Användargränssnittsstöd för molnlagringssystem | Ny källkoppling för [!DNL Azure Data Lake Storage Gen2] i användargränssnittet. |
| Gränssnittsstöd för CRM-system | Ny källkoppling för [!DNL HubSpot], [!DNL Salesforce Service Cloud]och [!DNL ServiceNow] i användargränssnittet. |
| Användargränssnittsstöd för databassystem | Ny källkoppling för [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]och [!DNL MySQL] i användargränssnittet. |

**Kända fel**

* Ingen

Mer information om källor finns i [Källöversikt](../../sources/home.md).