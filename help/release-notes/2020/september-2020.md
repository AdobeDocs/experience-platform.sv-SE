---
title: Adobe Experience Platform Release Notes september 2020
description: Versionsinformation för september 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 september 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datastyrning](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Datastyrning {#governance}

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Den spelar en nyckelroll inom [!DNL Experience Platform] på olika nivåer, bland annat katalog, datalinje, etikettering av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av användargränssnittet för datauppsättningar | Flera nya sorterings- och filtreringskontroller har lagts till i användargränssnittet för datauppsättningar för att göra det enklare att arbeta med stora scheman: <ul><li>Sortera fält i alfabetisk ordning baserat på den fullständiga schemasökvägen.</li><li>Utför delsökningar på fältsökvägsnamn.</li><li>Filtrera fält utan etiketter, en markerad etikett eller en etikettkategori.</li></ul> |

Mer information om tjänsten finns i [Datastyrningsöversikten](../../data-governance/home.md).

## Mål  {#destinations}

I [Real-time Customer Data Platform](../../rtcdp/overview.md) är mål färdiga integreringar med målplattformar som aktiverar data till dessa partner på ett smidigt sätt.

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
| Adobe I/O-händelsemeddelanden | [!DNL Observability Insights] använder Adobe I/O-händelser för att skapa händelseaviseringar för flera Experience Platform-tjänster. Meddelandenyttolaster skickas till en konfigurerad webkrok som du sedan kan använda för att automatisera ytterligare processer längre fram i kedjan. |

Mer information om tjänsten finns i [[!DNL Observability Insights] översikten](../../observability/home.md).

## [!DNL Privacy Service] {#privacy}

Flera juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service] kan du skicka förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för LGPD (Brasilien) | Sekretessjobb kan nu skapas enligt Brasiliens [!DNL Lei Geral de Proteção de Dados]-regel (LGPD). Dessa jobb spåras under regelkoden `lgpd_bra`. |

Mer information om tjänsten finns i [Privacy Servicen overview](../../privacy-service/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-Time Customer Profile] kan du se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med [!DNL Profile] kan du konsolidera dina olika kunddata till en enhetlig vy som ger ett åtgärdbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Profilvisningsprogram | Profilvisningsprogrammet, i plattformsgränssnittet, har uppdaterats till att vara en kontrollpanel med fullständig anpassning. Användaren kan nu göra följande: <ul><li>Uppdatera de valda standardattributen och anpassade attribut i widgeten för grundläggande information.</li><li>Skapa, redigera och ta bort anpassade widgetar</li><li>Ändra storlek på och ordna om widgetar</li></ul> |

Mer information om [!DNL Real-Time Customer Profile], inklusive självstudiekurser och metodtips för att arbeta med [!DNL Profile]-data, finns i [Kundprofilöversikt i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-Time Customer Profile]-data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform], vilket gör dem tillgängliga för alla Adobe-program.

[!DNL Segmentation Service] definierar en viss delmängd av profiler genom att beskriva kriterierna som särskiljer en marknadsföringsbar grupp av personer inom din kundbas. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportera jobb | En flagga lades till för att tillåta att segment utvärderas som en del av ett exportjobb. Det innebär att användare kan köra både segmentering och export i ett enda jobb. |
| Sammanfoga profiler | Flera sammanfogningspolicyer kan inkluderas i ett enda batchsegmenteringsjobb. |

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md)

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som du kan strukturera, etikettera och förbättra data med hjälp av [!DNL Platform]-tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatisk mappning | [!DNL Platform] ger intelligenta rekommendationer för automatisk mappning under arbetsflödet för datahämtning, baserat på ett målschema eller en datamängd som användaren valt. Du kan justera reglerna för automatisk mappning manuellt så att de passar dina behov. |
| Förbättringar av UX | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Mer information finns i dokumentet [Övervaka dataflöden](../../sources/tutorials/ui/monitor.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
