---
keywords: Experience Platform;hem;populära ämnen;Audience Manager-koppling;Målgruppshanterare;målgruppshanterare
solution: Experience Platform
title: Översikt över Audience Manager-källa
description: Adobe Audience Manager-källan strömmar förstahandsdata som samlats in i Audience Manager till Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 8ef9fedcc77f39707ef5191988a5b7360e1118cc
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Audience Manager source

>[!IMPORTANT]
>
>Vid den första konfigurationen returnerar Adobe Audience Manager-källan ett felmeddelande som förklarar att ett identitetsnamnutrymme med en viss `namespaceCode={VALUE}` finns inte. **Anteckning**: I bakänden, `namespaceCode` används för att referera till identitetssymbol. För att slutföra integreringen måste du:
>
>- [Skapa ett anpassat namnutrymme i identitetstjänsten](../../../identity-service/features/namespaces.md#create-custom-namespaces) med den angivna identitetssymbolen (`VALUE`) .
>- Importera dina data igen.

Adobe Audience Manager-källan strömmar förstahandsdata som samlats in i Adobe Audience Manager för aktivering i Adobe Experience Platform. Källan för Audience Manager importerar två typer av data till plattformen:

- **Realtidsdata:** Data som samlats in i realtid på Audience Manager datainsamlingsserver. Dessa data används i Audience Manager för att fylla i regelbaserade egenskaper och kommer att visas i plattformen på kortast möjliga latenstid.
- **Profildata:** Audience Manager använder realtidsdata och inbyggda data för att ta fram kundprofiler. De här profilerna används för att fylla i identitetsdiagram och egenskaper för segmentimplementeringar.

Audience Manager-källan mappar dessa datatyper till ett XDM-schema (Experience Data Model) och skickar dem sedan till plattformen. Realtidsdata skickas som XDM ExperienceEvent-data, medan profildata skickas som enskilda XDM-profildata.

Mer information finns i guiden [skapa en Audience Manager källanslutning i användargränssnittet](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Vad är Experience Data Model (XDM)?

XDM är en öppet dokumenterad specifikation som tillhandahåller ett standardiserat ramverk genom vilket Platform organiserar kundupplevelsedata.

Genom att följa XDM-standarder kan kundupplevelsedata integreras enhetligt, vilket gör det enklare att leverera data och samla in information.

Mer information om hur XDM används i Experience Platform finns i [XDM - systemöversikt](../../../xdm/home.md). Läs mer om hur XDM-scheman är strukturerade mellan profiler och händelser i [grunderna för schemakomposition](../../../xdm/schema/composition.md).

## XDM-scheman - exempel

Nedan visas exempel på Audience Manager-strukturen som är mappad till XDM ExperienceEvent och XDM Individual Profile i Platform.

### ExperienceEvent - för realtidsdata och inbyggda data

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Individuell XDM-profil - för profildata

![](images/aam-profile-xdm-for-profile-data.png)

Mer information om hur fält mappas från Audience Manager till XDM finns i dokumentationen om [Mappningsfält för Audience Manager](./mapping/audience-manager.md).

## Datahantering på plattformen

### Datauppsättningar

En datauppsättning är en lagrings- och hanteringskonstruktion för en datainsamling, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader) och som görs tillgängliga via en dataanslutning. Audience Manager data består av realtidsdata, inkommande data och profildata. Om du vill hitta dina datauppsättningar för Audience Manager använder du sökfunktionen i användargränssnittet med de namnkonventioner som anges för varje datatyp.

Audience Manager-datauppsättningar är inaktiverade som standard för Profil och användare kan aktivera eller inaktivera datauppsättningar baserat på användningsfall. Vi rekommenderar inte att du inaktiverar datauppsättningar som ska användas för segmentmedlemskap i profilen.

>[!NOTE]
>
>AAM i realtid är den enda datauppsättningen som går till datasjön. Alla andra datauppsättningar för Audience Manager går till [!DNL Profile], om de är aktiverade för [!DNL Profile]. Om de inte är aktiverade för [!DNL Profile], så får de inga data och de visas som tomma.

| Namn på datauppsättning | Beskrivning | Klass |
| --- | --- | --- |
| AAM i realtid | Den här datauppsättningen innehåller data som samlats in med direktträffar på Audience Manager DCS-slutpunkter och identitetskartor för Audience Manager-profiler. Låt den här datauppsättningen vara aktiverad för profilinmatning. | Experience event |
| AAM profiluppdateringar i realtid | Med den här datauppsättningen kan ni målinrikta Audience Manager-egenskaper och -segment i realtid. Det innehåller information om Edge regional routning, egenskaper och segmentmedlemskap. Låt den här datauppsättningen vara aktiverad för profilinmatning. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM | Enhetsdata med ECID:n och motsvarande segmentimplementeringar samlade i Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM enhetsprofildata | Används för diagnostik av anslutning till Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM autentiserade profiler | Den här datauppsättningen innehåller Audience Manager-autentiserade profiler. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| Metadata för AAM autentiserade profiler | Används för diagnostik av Audience Manager Connector. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM Devices Data Backfill | Datauppsättning från att hämta in tidigare enhetsdata. Detta innehåller ECID:n och motsvarande segmentrealiseringar som aggregerats i Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** växla till att direkt importera data till profilen. | Post |
| AAM för autentiserade profiler | Datauppsättning från att hämta in tidigare autentiserade data. Detta innehåller Audience Manager-autentiserade profiler. Data visas inte som batchar i datauppsättningen. Du kan aktivera **[!UICONTROL Profile]** växla till att direkt importera data till profilen. | Post |

### Anslutningar

Adobe Audience Manager skapar en anslutning i Katalog: Audience Manager Connection. Katalog är det system som används för att lagra och lagra data inom Adobe Experience Platform. En anslutning är ett katalogobjekt som är en kundspecifik instans av anslutningar. Läs [Katalogtjänst - översikt](../../../catalog/home.md) om du vill ha mer information om katalog, anslutningar och anslutningar.

### Segmentpopulation som påverkar profilen

Storleken på segmentpopulationer har en direkt inverkan på profilnumren när du skickar ett Audience Manager-segment till plattformen för första gången. Det innebär att om du väljer alla segment kan det potentiellt orsaka profilöverskridningar som överskrider din behörighet för licensanvändning. Plattformen skiljer också på nya data från historiska data för profilinmatning. Ett segment med 100 förstahandsbaserade identiteter skapar 100 profiler. Om populationen i samma segment höjdes till 150 och sattes in på Platform kommer antalet profiler endast att öka med 50, eftersom det bara finns 50 nya profiler.

Du kan även kontrollera profilanvändningen som ditt konto har tillgängligt via [Kontrollpanel för licensanvändning](../../../dashboards/guides/license-usage.md).

## Vilken fördröjning förväntas för Audience Manager Data on Platform?

| Audience Manager data | Typ | Latens | Anteckningar |
| --- | --- | --- | --- |
| Realtidsdata | Händelser | &lt;25 minuter | Tiden från att samlas in på noden Audience Manager Edge till att visas i datarjön. |
| Realtidsdata | Profiluppdateringar | &lt;10 minuter | Det är dags att lägga in kundprofilen i realtid. |
| Realtid och onboarddata | Profiluppdateringar | 24 till 36 timmar | Tid från att hämtas via DCS/PCS Edge-data och onboarddata, bearbetas till en användarprofil, till att sedan visas i kundprofilen i realtid. För närvarande landar dessa data inte direkt i datasjön. Profilväxling kan aktiveras för datauppsättningar i Audience Manager-profiler för att importera dessa data direkt till kundprofilen i realtid. |
