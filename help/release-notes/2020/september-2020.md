---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 9 september 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 64b6b59923d549cdcbf35d2e375529aec8cf81b8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 9 september 2020**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!DNL-mål]](#destinations)
* [[!DNL-källor]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Det spelar en viktig roll på [!DNL Experience Platform] olika nivåer, bland annat i fråga om katalogisering, datalinje, etikettering av dataanvändning, dataåtkomstprinciper och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar av användargränssnittet för datauppsättningar | Flera nya sorterings- och filtreringskontroller har lagts till i användargränssnittet för datauppsättningar för att göra det enklare att arbeta med stora scheman: <ul><li>Sortera fält i alfabetisk ordning baserat på den fullständiga schemasökvägen.</li><li>Utför delsökningar på fältsökvägsnamn.</li><li>Filtrera fält utan etiketter, en markerad etikett eller en etikettkategori.</li></ul> |

Mer information om tjänsten finns i [datastyrningsöversikten](../../data-governance/home.md) .

## Mål {#destinations}

I [Adobe kunddataplattform](../../rtcdp/overview.md)i realtid är destinationer färdigbyggda integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| UX-förbättringar | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Mer information finns i dokumentet för [målarbetsytan](../../rtcdp/destinations/destinations-workspace.md) . |

Mer information finns på [destinationsöversikten](../../rtcdp/destinations/destinations-overview.md)

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Automatisk mappning | [!DNL Platform] tillhandahåller intelligenta rekommendationer för automatisk mappning under arbetsflödet för dataöverföring, baserat på ett målschema eller en datamängd som användaren valt. Du kan justera reglerna för automatisk mappning manuellt så att de passar dina behov. |
| UX-förbättringar | Användare kan komma åt textbundna tabellåtgärder för enklare åtkomst till primära åtgärder som att lägga till data, redigera schemaläggning och lägga till segment. Mer information finns i dokumentet [för övervakning av dataflöden](../../sources/tutorials/ui/monitor.md) . |

Mer information om källor finns i [Källöversikt](../../sources/home.md).