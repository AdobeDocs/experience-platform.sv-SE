---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 9 september 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 312794af2cdb111fb81c0aa226dec68db2cbc374
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 september 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Governance]](#governance)
- [[!DNL-mål]](#destinations)
- [[!DNL-observabilitetsinsikter]](#observability)
- [[!DNL-Privacy Service]](#privacy)
- [[!DNL-kundprofil i realtid]](#profile)
- [[!DNL-segmenteringstjänst]](#segmentation)
- [[!DNL-källor]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Det spelar en viktig roll på [!DNL Experience Platform] olika nivåer, bland annat i fråga om katalogisering, datalinje, etikettering av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av användargränssnittet för datauppsättningar | Flera nya sorterings- och filtreringskontroller har lagts till i användargränssnittet för datauppsättningar för att göra det enklare att arbeta med stora scheman: <ul><li>Sortera fält i alfabetisk ordning baserat på den fullständiga schemasökvägen.</li><li>Utför delsökningar på fältsökvägsnamn.</li><li>Filtrera fält utan etiketter, en markerad etikett eller en etikettkategori.</li></ul> |

Mer information om tjänsten finns i översikten över [](../../data-governance/home.md) datastyrning.

## Mål {#destinations}

I [Adobe kunddataplattform](../../rtcdp/overview.md)i realtid är destinationer färdigbyggda integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| UX-förbättringar | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Mer information finns i dokumentet för [målarbetsytan](../../rtcdp/destinations/destinations-workspace.md) . |

Mer information finns på [destinationsöversikten](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] gör att ni kan övervaka aktiviteter på Adobe Experience Platform med hjälp av statistik och händelsemeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Adobe I/O-händelsemeddelanden | [!DNL Observability Insights] använder Adobe I/O-händelser för att skapa händelsemeddelanden för flera Experience Platform-tjänster. Meddelandenyttolaster skickas till en konfigurerad webkrok som du sedan kan använda för att automatisera ytterligare processer längre fram i kedjan. Mer information finns i [meddelandeöversikten](../../observability/notifications/overview.md) . |

Mer information om tjänsten finns i [[!DNL Observability Insights] översikten](../../observability/home.md) .

## [!DNL Privacy Service] {#privacy}

Flera juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] tillhandahåller ett RESTful API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service]kan ni skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessbestämmelser.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för LGPD (Brasilien) | Privacy job can now be created under Brazil&#39;s [!DNL Lei Geral de Proteção de Dados] (LGPD) Regulation. Dessa jobb spåras enligt föreskriftskoden `lgpd_bra`. |

Mer information om tjänsten finns i översikten över [](../../privacy-service/home.md) Privacy Servicen.

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-time Customer Profile]det kan ni få en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Profilvisningsprogram | Profilvisningsprogrammet i plattformsgränssnittet har uppdaterats till att vara en kontrollpanel med fullständig anpassning. Användaren kan nu göra följande: <ul><li>Uppdatera de valda standardattributen och anpassade attribut i widgeten för grundläggande information.</li><li>Skapa, redigera och ta bort anpassade widgetar</li><li>Ändra storlek på och ordna om widgetar</li></ul> |

Mer information om [!DNL Real-time Customer Profile]bland annat självstudiekurser och bästa metoder för att arbeta med [!DNL Profile] data finns i [Kundprofilöversikt](../../profile/home.md)i realtid.

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform segmenteringstjänst tillhandahåller ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-time Customer Profile] data. Dessa segment konfigureras och underhålls centralt [!DNL Platform]så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportera jobb | En flagga lades till för att tillåta att segment utvärderas som en del av ett exportjobb. Det innebär att användare kan köra både segmentering och export i ett enda jobb. |
| Sammanfoga profiler | Flera sammanfogningspolicyer kan inkluderas i ett enda batchsegmenteringsjobb. |

Mer information om [!DNL Segmentation Service]segmentering finns i [segmenteringsöversikten](../../segmentation/home.md)

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatisk mappning | [!DNL Platform] tillhandahåller intelligenta rekommendationer för automatisk mappning under arbetsflödet för dataöverföring, baserat på ett målschema eller en datamängd som användaren valt. Du kan justera reglerna för automatisk mappning manuellt så att de passar dina behov. |
| UX-förbättringar | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Mer information finns i dokumentet [för övervakning av dataflöden](../../sources/tutorials/ui/monitor.md) . |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
