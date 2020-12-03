---
keywords: Experience Platform;home;popular topics;Audience Manager connector;Audience manager;audience manager
solution: Experience Platform
title: Audience Manager-kontakt
topic: overview
description: Adobe Audience Manager dataanslutning strömmar data från första part som samlats in i Adobe Audience Manager till Adobe Experience Platform. Kopplingen Audience Manager importerar tre datakategorier till plattformen.
translation-type: tm+mt
source-git-commit: e51f750dae2a76cd05076edfe8c6423efe949891
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Audience Manager-kontakt

Adobe Audience Manager dataanslutning strömmar data från första part som samlats in i Adobe Audience Manager till Adobe Experience Platform. Kopplingen Audience Manager importerar tre kategorier data till plattformen:

- **Realtidsdata:** Data som samlats in i realtid på Audience Manager datainsamlingsserver. Dessa data används i Audience Manager för att fylla i regelbaserade egenskaper och kommer att visas i plattformen på kortast möjliga latenstid.
- **Profildata:** Audience Manager använder realtidsdata och inbyggda data för att ta fram kundprofiler. De här profilerna används för att fylla i identitetsdiagram och egenskaper för segmentimplementeringar.

Kopplingen Audience Manager mappar dessa datakategorier till XDM-schemat (Experience Data Model) och skickar dem till Platform. Realtidsdata skickas som XDM ExperienceEvent-data, medan profildata skickas som enskilda XDM-profiler.

Instruktioner om hur du skapar en anslutning med Adobe Audience Manager med hjälp av användargränssnittet för plattformen finns i självstudiekursen [för](../../tutorials/ui/create/adobe-applications/audience-manager.md)Audience Manager-anslutningen.

## Vad är Experience Data Model (XDM)?

XDM är en öppet dokumenterad specifikation som tillhandahåller ett standardiserat ramverk genom vilket Platform organiserar kundupplevelsedata.

Genom att följa XDM-standarder kan kundupplevelsedata integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om hur XDM används i Experience Platform finns i [XDM-systemöversikten](../../../xdm/home.md). Mer information om hur XDM-scheman som Profile och ExperienceEvent är strukturerade finns i [grunderna för schemakomposition](../../../xdm/schema/composition.md).

## XDM-scheman - exempel

Nedan visas exempel på Audience Manager-strukturen som är mappad till XDM ExperienceEvent och XDM Individual Profile i Platform.

### ExperienceEvent - för realtidsdata och inbyggda data

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Individuell XDM-profil - för profildata

![](images/aam-profile-xdm-for-profile-data.png)

## Hur mappas fält från Adobe Audience Manager till XDM?

Mer information finns i dokumentationen för mappningsfält [för](./mapping/audience-manager.md) Audience Manager.

## Datahantering på plattformen

### Datauppsättningar

Datauppsättningar är en lagrings- och hanteringskonstruktion för en samling data, vanligtvis en tabell, som innehåller schema (kolumner) och fält (rader) och som görs tillgängliga via en dataanslutning. Audience Manager data består av realtidsdata, inkommande data och profildata. Om du vill hitta dina datauppsättningar för Audience Manager använder du sökfunktionen i användargränssnittet med de namnkonventioner som anges för varje datatyp.

Audience Manager-datauppsättningar är inaktiverade som standard för Profil och användare kan aktivera eller inaktivera datauppsättningar baserat på användningsfall. Vi rekommenderar inte att du inaktiverar datauppsättningar som ska användas för segmentmedlemskap i profilen.

| Namn på datauppsättning | Beskrivning |
| ------------ | ----------- |
| Audience Manager i realtid | Den här datauppsättningen innehåller data som samlats in med direktträffar på Audience Manager DCS-slutpunkter och identitetskartor för Audience Manager-profiler. Låt den här datauppsättningen vara aktiverad för profilinmatning. |
| Profiluppdateringar i realtid för Audience Manager | Med den här datauppsättningen kan ni målinrikta Audience Manager-egenskaper och -segment i realtid. Det innehåller information om Edge regional routning, egenskaper och segmentmedlemskap. Låt den här datauppsättningen vara aktiverad för profilinmatning. Data visas inte som batchar i datauppsättningen. Du kan aktivera växlingsknappen Profil om du vill importera data direkt till Profil. |
| Data för Audience Manager-enheter | Enhetsdata med ECID:n och motsvarande segmentimplementeringar samlade i Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera växlingsknappen Profil om du vill importera data direkt till Profil. |
| Audience Manager-profildata | Används för diagnostik av anslutning till Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera växlingsknappen Profil om du vill importera data direkt till Profil. |
| Audience Manager-autentiserade profiler | Den här datauppsättningen innehåller Audience Manager-autentiserade profiler. Data visas inte som batchar i datauppsättningen. Du kan aktivera växlingsknappen Profil om du vill importera data direkt till Profil. |
| Metadata för autentiserade profiler i Audience Manager | Används för diagnostik av Audience Manager Connector. Data visas inte som batchar i datauppsättningen. Du kan aktivera växlingsknappen Profil om du vill importera data direkt till Profil. |

### Anslutningar

Adobe Audience Manager skapar en anslutning i katalogen: Audience Manager Connection. Katalog är det system som används för att lagra och lagra data inom Adobe Experience Platform. En anslutning är ett katalogobjekt som är en kundspecifik instans av Connectors. Mer information om kataloger, anslutningar och anslutningar finns i översikten [för](../../../catalog/home.md) katalogtjänsten.

## Vilken fördröjning förväntas för Audience Manager Data on Platform?

| Audience Manager data | Latens | Anteckningar |
| --- | --- | --- |
| Realtidsdata | &lt; 35 minuter. | Tiden från att hämtas på noden Audience Manager Edge till att visas på Data Lake för plattformen. |
| Profildata | &lt; 2 dagar | Tid från att hämtas via DCS/PCS Edge-data och on-board-data, bearbetas till en användarprofil, till att sedan visas i profilen. Dessa data landar inte direkt på Platform Data Lake idag. Profilväxling kan aktiveras för datauppsättningar i Audience Manager-profiler för att importera dessa data direkt till profilen. |