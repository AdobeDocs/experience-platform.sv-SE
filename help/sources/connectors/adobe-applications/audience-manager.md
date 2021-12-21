---
keywords: Experience Platform;hem;populära ämnen;Audience Manager-koppling;Målgruppshanterare;målgruppshanterare
solution: Experience Platform
title: Översikt över Audience Manager Source Connector
topic-legacy: overview
description: Adobe Audience Manager källanslutning strömmar förstahandsdata som samlats in i Audience Manager till Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: d0b6885b6e8606692cfe1173b75c7d3537800a5f
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Audience Manager-kontakt

Adobe Audience Manager dataanslutning strömmar förstahandsdata som samlats in i Adobe Audience Manager till Adobe Experience Platform. Kopplingen Audience Manager importerar två typer av data till plattformen:

- **Realtidsdata:** Data som samlats in i realtid på Audience Manager datainsamlingsserver. Dessa data används i Audience Manager för att fylla i regelbaserade egenskaper och kommer att visas i plattformen på kortast möjliga latenstid.
- **Profildata:** Audience Manager använder realtids- och interndata för att ta fram kundprofiler. De här profilerna används för att fylla i identitetsdiagram och egenskaper för segmentimplementeringar.

Kopplingen Audience Manager mappar dessa datakategorier till XDM-schemat (Experience Data Model) och skickar dem till Platform. Realtidsdata skickas som XDM ExperienceEvent-data, medan profildata skickas som enskilda XDM-profiler.

Instruktioner om hur du skapar en anslutning med Adobe Audience Manager via plattformsgränssnittet finns i [Audience Manager-anslutning, genomgång](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Vad är Experience Data Model (XDM)?

XDM är en öppet dokumenterad specifikation som tillhandahåller ett standardiserat ramverk genom vilket Platform organiserar kundupplevelsedata.

Genom att följa XDM-standarder kan kundupplevelsedata integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om hur XDM används i Experience Platform finns i [XDM - systemöversikt](../../../xdm/home.md). Mer information om hur XDM-scheman som Profile och ExperienceEvent struktureras finns i [grunderna för schemakomposition](../../../xdm/schema/composition.md).

## XDM-scheman - exempel

Nedan visas exempel på Audience Manager-strukturen som är mappad till XDM ExperienceEvent och XDM Individual Profile i Platform.

### ExperienceEvent - för realtidsdata och inbyggda data

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Individuell XDM-profil - för profildata

![](images/aam-profile-xdm-for-profile-data.png)

## Hur mappas fält från Adobe Audience Manager till XDM?

Se dokumentationen för [Mappningsfält för Audience Manager](./mapping/audience-manager.md) för mer information.

## Datahantering på plattformen

### Datauppsättningar

Datauppsättningar är en lagrings- och hanteringskonstruktion för en samling data, vanligtvis en tabell, som innehåller schema (kolumner) och fält (rader) och som görs tillgängliga via en dataanslutning. Audience Manager data består av realtidsdata, inkommande data och profildata. Om du vill hitta dina datauppsättningar för Audience Manager använder du sökfunktionen i användargränssnittet med de namnkonventioner som anges för varje datatyp.

Audience Manager-datauppsättningar är inaktiverade som standard för Profil och användare kan aktivera eller inaktivera datauppsättningar baserat på användningsfall. Vi rekommenderar inte att du inaktiverar datauppsättningar som ska användas för segmentmedlemskap i profilen.

>[!NOTE]
>
>AAM i realtid är den enda datauppsättningen som går till [!DNL Data Lake]. Alla andra datauppsättningar för Audience Manager går till [!DNL Profile], om de är aktiverade för [!DNL Profile]. Om de inte är aktiverade för [!DNL Profile], så får de inga data och de visas som tomma.

| Namn på datauppsättning | Beskrivning | Klass |
| --- | --- | --- |
| AAM realtid | Den här datauppsättningen innehåller data som samlats in med direktträffar på Audience Manager DCS-slutpunkter och identitetskartor för Audience Manager-profiler. Låt den här datauppsättningen vara aktiverad för profilinmatning. | Experience event |
| AAM profiluppdateringar i realtid | Med den här datauppsättningen kan ni målinrikta Audience Manager-egenskaper och -segment i realtid. Det innehåller information om Edge regional routning, egenskaper och segmentmedlemskap. Låt den här datauppsättningen vara aktiverad för profilinmatning. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM | Enhetsdata med ECID:n och motsvarande segmentimplementeringar samlade i Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM enhetsprofildata | Används för diagnostik av anslutning till Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM autentiserade profiler | Den här datauppsättningen innehåller Audience Manager-autentiserade profiler. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| Metadata för AAM autentiserade profiler | Används för diagnostik av Audience Manager Connector. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM Devices Data Backfill | Datauppsättning från att hämta data från tidigare enheter. Detta innehåller ECID och motsvarande segmentrealiseringar som aggregerats i Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** växla till att direkt importera data till profilen. | Post |
| AAM för autentiserade profiler | Datauppsättning från att hämta in tidigare autentiserade data. Detta innehåller Audience Manager-autentiserade profiler. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** växla till att direkt importera data till profilen. | Post |

### Anslutningar

Adobe Audience Manager skapar en anslutning i katalogen: Audience Manager Connection. Katalog är det system som används för att lagra och lagra data inom Adobe Experience Platform. En anslutning är ett katalogobjekt som är en kundspecifik instans av Connectors. Se [Katalogtjänst - översikt](../../../catalog/home.md) om du vill ha mer information om katalog, anslutningar och anslutningar.

## Vilken fördröjning förväntas för Audience Manager Data on Platform?

| Audience Manager data | Latens | Anteckningar |
| --- | --- | --- |
| Realtidsdata | &lt; 35 minuter. | Tiden från att hämtas på noden Audience Manager Edge till att visas på Data Lake för plattformen. |
| Profildata | &lt; 2 dagar | Tid från att hämtas via DCS/PCS Edge-data och on-board-data, bearbetas till en användarprofil, till att sedan visas i profilen. Dessa data landar inte direkt på Platform Data Lake idag. Profilväxling kan aktiveras för datauppsättningar i Audience Manager-profiler för att importera dessa data direkt till profilen. |
