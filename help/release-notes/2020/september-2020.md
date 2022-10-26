---
title: Adobe Experience Platform Release Notes september 2020
description: Versionsinformation för september 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 september 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datastyrning](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Datastyrning {#governance}

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Det spelar en nyckelroll inom [!DNL Experience Platform] på olika nivåer, inklusive katalogisering, datalinje, märkning av dataanvändning, dataåtkomstregler och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av användargränssnittet för datauppsättningar | Flera nya sorterings- och filtreringskontroller har lagts till i användargränssnittet för datauppsättningar för att göra det enklare att arbeta med stora scheman: <ul><li>Sortera fält i alfabetisk ordning baserat på den fullständiga schemasökvägen.</li><li>Utför delsökningar på fältsökvägsnamn.</li><li>Filtrera fält utan etiketter, en markerad etikett eller en etikettkategori.</li></ul> |

Se [Datastyrning - översikt](../../data-governance/home.md) för mer information om tjänsten.

## Mål  {#destinations}

I [Real-time Customer Data Platform](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| UX-förbättringar | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Se [målarbetsyta](../../destinations/ui/destinations-workspace.md) för mer information. |

Mer information finns på [destinationer, översikt](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] gör att ni kan övervaka aktiviteter på Adobe Experience Platform med hjälp av statistik och händelsemeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Adobe I/O-händelsemeddelanden | [!DNL Observability Insights] använder Adobe I/O Events för att skapa händelsemeddelanden för flera Experience Platform-tjänster. Meddelandenyttolaster skickas till en konfigurerad webkrok som du sedan kan använda för att automatisera ytterligare processer längre fram i kedjan. |

Se [[!DNL Observability Insights] översikt](../../observability/home.md) för mer information om tjänsten.

## [!DNL Privacy Service] {#privacy}

Flera juridiska och organisatoriska bestämmelser ger användarna rätt att få tillgång till eller ta bort sina personuppgifter från era datalager på begäran. Adobe Experience Platform [!DNL Privacy Service] innehåller ett RESTful-API och användargränssnitt som hjälper dig att hantera dessa dataförfrågningar från dina kunder. Med [!DNL Privacy Service]kan du skicka in förfrågningar om åtkomst till och radering av privata eller personliga kunddata från Adobe Experience Cloud-program, vilket underlättar automatiserad efterlevnad av juridiska och organisatoriska sekretessregler.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för LGPD (Brasilien) | Integritetsjobb kan nu skapas i Brasilien [!DNL Lei Geral de Proteção de Dados] LGPD-regler. Dessa jobb spåras enligt regelkoden `lgpd_bra`. |

Se [Översikt över Privacy Servicen](../../privacy-service/home.md) för mer information om tjänsten.

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-time Customer Profile]kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Profilvisningsprogram | Profilvisningsprogrammet i plattformsgränssnittet har uppdaterats till att vara en kontrollpanel med fullständig anpassning. Användaren kan nu göra följande: <ul><li>Uppdatera de valda standardattributen och anpassade attribut i widgeten för grundläggande information.</li><li>Skapa, redigera och ta bort anpassade widgetar</li><li>Ändra storlek på och ordna om widgetar</li></ul> |

Mer information om [!DNL Real-time Customer Profile], inklusive självstudiekurser och metodtips för att arbeta med [!DNL Profile] data, läs [Översikt över kundprofiler i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform Segmentation Service har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper från din [!DNL Real-time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform], så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Exportera jobb | En flagga lades till för att tillåta att segment utvärderas som en del av ett exportjobb. Det innebär att användare kan köra både segmentering och export i ett enda jobb. |
| Sammanfoga profiler | Flera sammanfogningspolicyer kan inkluderas i ett enda batchsegmenteringsjobb. |

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md)

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatisk mappning | [!DNL Platform] tillhandahåller intelligenta rekommendationer för automatisk mappning under arbetsflödet för dataöverföring, baserat på ett målschema eller en datamängd som användaren valt. Du kan justera reglerna för automatisk mappning manuellt så att de passar dina behov. |
| UX-förbättringar | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Se [övervaka dataflöden](../../sources/tutorials/ui/monitor.md) för mer information. |

Mer information om källor finns i [källöversikt](../../sources/home.md).
