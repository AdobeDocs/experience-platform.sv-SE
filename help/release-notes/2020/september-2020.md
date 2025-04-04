---
title: Versionsinformation om Adobe Experience Platform september 2020
description: Versionsinformationen för Adobe Experience Platform från september 2020.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 35%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 september 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Dataförvaltning](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Dataförvaltning {#governance}

Dataförvaltning i Adobe Experience Platform är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Den spelar en viktig roll inom [!DNL Experience Platform] på olika nivåer, bland annat katalogföring, datahärkomst, märkning av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av användargränssnittet för datauppsättningar | Flera nya sorterings- och filtreringskontroller har lagts till i användargränssnittet för datauppsättningar för att göra det enklare att arbeta med stora scheman: <ul><li>Sortera fält i alfabetisk ordning baserat på den fullständiga schemasökvägen.</li><li>Utför delsökningar på fältsökvägsnamn.</li><li>Filtrera fält utan etiketter, en markerad etikett eller en etikettkategori.</li></ul> |

Mer information om tjänsten finns i [Datastyrningsöversikten](../../data-governance/home.md).

## Mål {#destinations}

I [Real-Time Customer Data Platform](../../rtcdp/overview.md) är mål färdiga integreringar med målplattformar som aktiverar data till dessa partner på ett smidigt sätt.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av UX | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Mer information finns i dokumentet [målarbetsyta](../../destinations/ui/destinations-workspace.md). |

Mer information finns på [målöversikten](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

Med [!DNL Observability Insights] kan du övervaka aktiviteter på Adobe Experience Platform med hjälp av statistik och händelsemeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Adobe I/O-händelsemeddelanden | [!DNL Observability Insights] använder Adobe I/O Events för att skapa händelsemeddelanden för flera Experience Platform-tjänster. Meddelandenyttolaster skickas till en konfigurerad webkrok som du sedan kan använda för att automatisera ytterligare processer längre fram i kedjan. |

Mer information om tjänsten finns i [[!DNL Observability Insights] översikten](../../observability/home.md).

## [!DNL Privacy Service] {#privacy}

Flera juridiska och organisatoriska bestämmelser ger användare rätt att på begäran få tillgång till eller radera sina personuppgifter från dina datalager. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service] kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-applikationer, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för LGPD (Brasilien) | Sekretessjobb kan nu skapas enligt Brasiliens [!DNL Lei Geral de Proteção de Dados] (LGPD)-reglering. Dessa jobb registreras under regelkoden `lgpd_bra`. |

Mer information om tjänsten finns i [översikten över Privacy Service](../../privacy-service/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med [!DNL Real-Time Customer Profile] kan du se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med [!DNL Profile] kan du konsolidera dina olika kunddata till en enhetlig vy som ger ett åtgärdbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Profilvisningsprogram | Profilvisningsprogrammet i Experience Platform-gränssnittet har uppdaterats till att vara en kontrollpanel med fullständig anpassning. Användaren kan nu göra följande: <ul><li>Uppdatera de valda standardattributen och anpassade attribut i widgeten för grundläggande information.</li><li>Skapa, redigera och ta bort anpassade widgetar</li><li>Ändra storlek på och ordna om widgetar</li></ul> |

Mer information om [!DNL Real-Time Customer Profile], inklusive självstudiekurser och metodtips för att arbeta med [!DNL Profile]-data, finns i [Kundprofilöversikt i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-Time Customer Profile]-data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Experience Platform], vilket gör dem tillgängliga för alla Adobe-program.

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportera jobb | En flagga lades till för att tillåta att segment utvärderas som en del av ett exportjobb. Det innebär att användare kan köra både segmentering och export i ett enda jobb. |
| Sammanfoga profiler | Flera sammanfogningspolicyer kan inkluderas i ett enda batchsegmenteringsjobb. |

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md)

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som du kan strukturera, etikettera och förbättra data med hjälp av [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatisk mappning | [!DNL Experience Platform] ger intelligenta rekommendationer för automatisk mappning under arbetsflödet för datahämtning, baserat på ett målschema eller en datamängd som användaren valt. Du kan justera reglerna för automatisk mappning manuellt så att de passar dina behov. |
| Förbättringar av UX | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Mer information finns i dokumentet [Övervaka dataflöden](../../sources/tutorials/ui/monitor.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
