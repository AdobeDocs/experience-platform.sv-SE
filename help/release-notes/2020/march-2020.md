---
title: Versionsinformation om Adobe Experience Platform mars 2020
description: Versionsinformationen för Adobe Experience Platform i mars 2020.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: Versionsinformation.
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 15%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 mars 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [Dataförvaltning](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Dataförvaltning {#governance}

Med [!DNL Experience Platform] kan företag samla data från flera företagssystem för att bättre kunna identifiera, förstå och engagera kunder. [!DNL Experience Platform] innehåller en komplett datastyrningsinfrastruktur för att säkerställa att data används på rätt sätt i [!DNL Experience Platform] och när de delas mellan system.

Dataförvaltning i Adobe Experience Platform är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Den spelar en viktig roll inom [!DNL Experience Platform] på olika nivåer, bland annat katalogföring, datahärkomst, märkning av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

>[!NOTE]
>
>Vissa av följande nya funktioner är för närvarande betaversioner och är inte tillgängliga för alla användare. Beta funktioner kan komma att ändras.

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatisk tvingande av dataanvändningsprinciper för [!DNL Real-Time Customer Data Platform] | Dataanvändningsprinciper används nu i arbetsflödet för att aktivera data till mål. Datastyrning bäddas också in och tillämpas när du gör ändringar som påverkar befintliga aktiveringar (t.ex. ändringar i datauppsättningsrubriker, sammanfogningsprinciper, segmentdefinitioner). |
| Datalinje för verkställighet | När en dataanvändningsprincip överträds i Real-Time CDP visas ett meddelande i användargränssnittet som innehåller information om datalinjerna så att användaren kan förstå varför policyer överträds och vad de kan göra för att åtgärda överträdelsen. |


**Kända fel**

* Ingen

Mer information om datastyrning finns i [Översikt över datastyrning](../../data-governance/home.md).

## Datainmatning {#ingestion}

Adobe Experience Platform har en omfattande uppsättning funktioner för att importera alla typer av data och fördröjningar. Adobe Experience Platform [!DNL Data Ingestion] innehåller flera alternativ för inmatning av data, bland annat API:er för gruppbearbetning, API:er för direktuppspelning, inbyggda Adobe-anslutningar, dataintegrationspartners eller Adobe Experience Platform användargränssnitt.

**Nya funktioner**

| Funktion | Beskrivning |
|------- | -----------|
| Partiellt batchintag | Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till en viss tröskel. Med den här funktionen kan användare importera alla korrekta data till Adobe Experience Platform samtidigt som felaktiga data grupperas separat. Information läggs till i misslyckade batchar för att förklara varför de inte klarade valideringen. Mer information om partiell gruppinmatning finns i [dokumentationen om partiell gruppinmatning](../../ingestion/batch-ingestion/partial.md). |

**Kända fel**

* Ingen

Mer information om hur du importerar data till Experience Platform finns i [dokumentationen för datainmatning](../../ingestion/home.md).


## Mål {#destinations}

I [Real-Time Customer Data Platform](../../rtcdp/overview.md) är mål färdiga integreringar med målplattformar som aktiverar data till dessa partner på ett smidigt sätt.

**Nya mål**

Det finns nya destinationer där du kan aktivera dina Adobe Experience Platform-data. Mer information finns nedan:

| Mål | Beskrivning |
|--- | ---|
| Lagringsmål i molnet | Real-Time CDP kan nu leverera dina segment som datafiler till dina [!DNL Amazon S3]- eller SFTP-molnlagringsplatser. Detta gör att du kan skicka målgrupper och deras profilattribut till dina interna system via CSV eller tabbavgränsade filer. |
| Advertising destinationer | Målkortet [!DNL Google] delas nu upp i tre målkort för de tre olika [!DNL Google]-plattformar som för närvarande stöds i Real-Time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Mer information finns på [målöversikten](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper dig att få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrat privat diagram | Funktionen för privata diagram har förbättrats för att minska fördröjningen för diagramgenerering från en gruppbearbetning varje vecka till ett dagligt uppdaterat diagram, vilket ger [!DNL Identity Service] kunder tillgång till mer aktuella identitetsdiagram och länkar. |

**Kända fel**

* Ingen

Mer information om [!DNL Identity Service] finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som du kan strukturera, etikettera och förbättra data med hjälp av [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Undertryckta signaler för Adobe Audience Manager Connector | Signalnivådata från Audience Manager kommer inte längre att skickas. Observera att segmentmedlemskap för Traits and Segments fortfarande kommer att inkluderas. Till följd av den här ändringen kommer inkommande datauppsättningar inte längre att genereras. |
| Ändrade namn på datauppsättningar | Datauppsättningar som genereras av Audience Manager-kopplingen har uppdaterade namn och beskrivningar. |
| Aktivera växlingen [!DNL Profile] i Audience Manager | [!DNL Profile]-växlingen kan aktiveras eller inaktiveras för att höja datauppsättningen till [!DNL Real-Time Customer Profile]. Växla aktiveras som standard. |
| Användargränssnittsstöd för molnlagringssystem | Ny källkoppling för [!DNL Azure Data Lake Storage Gen2] i användargränssnittet. |
| Gränssnittsstöd för CRM-system | Ny källkoppling för [!DNL HubSpot], [!DNL Salesforce Service Cloud] och [!DNL ServiceNow] i användargränssnittet. |
| Användargränssnittsstöd för databassystem | Ny källkoppling för [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] och [!DNL MySQL] i användargränssnittet. |

**Kända fel**

* Ingen

Mer information om källor finns i [Källöversikt](../../sources/home.md).
