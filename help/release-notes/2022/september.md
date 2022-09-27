---
title: Adobe Experience Platform Release Notes september 2022
description: Versionsinformation för september 2022 för Adobe Experience Platform.
source-git-commit: db4f04c0af98fe053fbb770b2301f7d3e9d2bb1a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 28 september 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Identitetstjänst](#identity-service)
- [Källor](#sources)

## Identitetstjänst {#identity-service}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för borttagning av datauppsättningar | Identitetstjänsten har nu stöd för borttagning av datauppsättningar vid begäran via [Katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), användargränssnittet eller datahygien. Läs guiden på [ta bort datauppsättningar i användargränssnittet](../../catalog/datasets/user-guide.md#delete-a-dataset) för mer information. |

Mer information om identitetstjänsten finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Audience Manager segmentpopulationens påverkan på kundprofilen i realtid | Intag av stora Audience Manager-segmentpopulationer har en direkt inverkan på det totala antalet profiler när du för första gången skickar ett Audience Manager-segment till plattformen via Audience Manager. Det innebär att om du väljer alla segment kan det eventuellt leda till ett profilantal som överskrider licensanvändningsbehörigheten. Mer information finns i [Översikt över Audience Manager-källa](../../sources/connectors/adobe-applications/audience-manager.md). Mer information om licensanvändningen finns i dokumentationen om [med kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md). |

Läs mer om källor i [källöversikt](../../sources/home.md).