---
title: Versionsinformation om Adobe Experience Platform mars 2020
description: Versionsinformation mars 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: Versionsinformation.
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 mars 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [Datastyrning](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Datastyrning {#governance}

[!DNL Experience Platform] gör det möjligt för företag att samla data från flera företagssystem för att bättre kunna identifiera, förstå och engagera kunder. [!DNL Experience Platform] omfattar en infrastruktur för datastyrning från början till slut som säkerställer korrekt användning av data inom [!DNL Platform] och när de delas mellan system.

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Det spelar en nyckelroll inom [!DNL Experience Platform] på olika nivåer, inklusive katalogisering, datalinje, märkning av dataanvändning, dataåtkomstregler och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

>[!NOTE]
>
>Vissa av följande nya funktioner är för närvarande betaversioner och är inte tillgängliga för alla användare. Betafunktionerna kan komma att ändras.

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatiserad tillämpning av dataanvändningsprinciper för [!DNL Real-Time Customer Data Platform] | Dataanvändningsprinciper används nu i arbetsflödet för att aktivera data till mål. Datastyrning bäddas också in och tillämpas när du gör ändringar som påverkar befintliga aktiveringar (t.ex. ändringar i datauppsättningsrubriker, sammanfogningsprinciper, segmentdefinitioner). |
| Datalinje för verkställighet | När en dataanvändningsprincip överträds i Real-Time CDP visas ett meddelande i användargränssnittet som innehåller information om datalinjerna så att användaren kan förstå varför policyer överträds och vad de kan göra för att åtgärda överträdelsen. |


**Kända fel**

* Ingen

Mer information om datastyrning finns i [Datastyrning - översikt](../../data-governance/home.md).

## Datainmatning {#ingestion}

Adobe Experience Platform har en omfattande uppsättning funktioner för att importera alla typer av data och fördröjningar. Adobe Experience Platform [!DNL Data Ingestion] innehåller flera alternativ för inmatning av data, bland annat API:er för grupper av filer, API:er för direktuppspelning, inbyggda Adobe-anslutningar, dataintegrationspartners eller Adobe Experience Platform användargränssnitt.

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Partiellt batchintag | Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som felaktiga data grupperas separat. Information läggs till i misslyckade batchar för att förklara varför de inte klarade valideringen. Mer information om partiell gruppinmatning finns i [dokumentation om partiell batchimport](../../ingestion/batch-ingestion/partial.md). |

**Kända fel**

* Ingen

Läs mer om hur du hämtar in data till Platform på [Dokumentation för datainmatning](../../ingestion/home.md).


## Mål  {#destinations}

I [Real-time Customer Data Platform](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

Det finns nya destinationer där du kan aktivera dina Adobe Experience Platform-data. Mer information finns nedan:

| Destination | Beskrivning |
|--- | ---|
| Lagringsmål i molnet | Real-Time CDP kan nu leverera era segment som datafiler till [!DNL Amazon S3] eller lagringsplatser för SFTP i molnet. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer. |
| Annonsmål | The [!DNL Google] destinationskortet delas nu upp i tre destinationskort för de tre olika [!DNL Google] plattformar som för närvarande stöds i Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Mer information finns på [destinationer, översikt](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrat privat diagram | Funktionen för privata diagram har förbättrats för att minska tidsfördröjningen för diagramgenerering från en gruppbearbetning varje vecka till ett dagligt uppdaterat diagram, vilket gör att [!DNL Identity Service] kunder för att få tillgång till mer aktuella identitetsdiagram och länkar. |

**Kända fel**

* Ingen

Mer information om [!DNL Identity Service], se [Översikt över identitetstjänsten](../../identity-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Undertryckta signaler för Adobe Audience Manager Connector | Signalnivådata från Audience Manager kommer inte längre att skickas. Observera att segmentmedlemskap för Traits and Segments fortfarande inkluderas. Till följd av den här ändringen kommer inkommande datauppsättningar inte längre att genereras. |
| Ändrade namn på datauppsättningar | Datauppsättningar som genereras av Audience Manager-kopplingen har uppdaterade namn och beskrivningar. |
| Aktivera [!DNL Profile] växla i Audience Manger | [!DNL Profile] växlingsknappen kan aktiveras eller inaktiveras för att höja upp datauppsättningen till [!DNL Real-Time Customer Profile]. Växla aktiveras som standard. |
| Användargränssnittsstöd för molnlagringssystem | Ny källkoppling för [!DNL Azure Data Lake Storage Gen2] i användargränssnittet. |
| Gränssnittsstöd för CRM-system | Ny källkoppling för [!DNL HubSpot], [!DNL Salesforce Service Cloud]och [!DNL ServiceNow] i användargränssnittet. |
| Användargränssnittsstöd för databassystem | Ny källkoppling för [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]och [!DNL MySQL] i användargränssnittet. |

**Kända fel**

* Ingen

Mer information om källor finns i [källöversikt](../../sources/home.md).
