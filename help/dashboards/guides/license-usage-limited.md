---
keywords: Experience Platform;användargränssnitt;användargränssnitt;anpassning;kontrollpanel för licensanvändning;kontrollpanel;licensanvändning;berättigande;förbrukning
title: Handbok för kontrollpanel för licensanvändning
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om din organisations licensanvändning.
type: Documentation
hide: true
hidefromtoc: true
source-git-commit: 25f57b1bfbcb2ec95f88afb69386a10deb600125
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Kontrollpanel för licensanvändning (begränsad version) {#license-usage-dashboard-limited-release}

>[!IMPORTANT]
>
>Den uppdaterade [!UICONTROL License usage] instrumentpanelen är för närvarande tillgänglig i en **Endast begränsad version** och inte är tillgängligt för alla kunder.

Du kan visa viktig information om din organisations licensanvändning via Adobe Experience Platform [!UICONTROL License usage] kontrollpanel. Den information som visas här fångas in under en daglig ögonblicksbild av din Platform-instans.

Licensanvändningsrapporter ger en hög grad av granularitet över era användningsvärden för licenser. Kontrollpanelen tillhandahåller användningsstatistik för varje köpt produkt, konsoliderad användning av statistik i alla produktions- eller utvecklingssandlådor samt användningsstatistik från en viss sandlåda. Följande Experience Platform-program kan spåras med användningsstatistik: Kunddataprofil i realtid, Adobe Journey Optimizer och Customer Journey Analytics.

I den här handboken beskrivs hur du får åtkomst till och arbetar med kontrollpanelen för licensanvändning i användargränssnittet och den innehåller mer information om de visualiseringar som visas på kontrollpanelen.

En allmän översikt över användargränssnittet för plattformen finns i [Användargränssnittsguide för Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL License usage] instrumentpanelsdata

The [!UICONTROL License usage] På kontrollpanelen visas en lista med alla Experience Platform-produkter som du har köpt. I den här listan hittar du en ögonblicksbild av din organisations licensrelaterade data för Experience Platform i alla associerade sandlådor.

Informationen i den här instrumentpanelen visas exakt som den visas vid den specifika tidpunkt då ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och instrumentpanelen uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska kontrollpanelen för licensanvändning {#explore}

Om du vill navigera till kontrollpanelen för licensanvändning i plattformsgränssnittet väljer du **[!UICONTROL License usage]** till vänster. The [!UICONTROL Overview] öppnas, visa en lista med tillgängliga produkter.

>[!NOTE]
>
>Kontrollpanelen för licensanvändning är inte aktiverad som standard. Användarna måste beviljas[!UICONTROL View License Usage Dashboard]&quot; behörighet att visa kontrollpanelen. Anvisningar om hur du beviljar åtkomstbehörigheter för att visa kontrollpanelen för licensanvändning finns i [behörighetsguide för instrumentpanel](../permissions.md).

![Kontrollpanelens översiktsflik för licensanvändning, med licensanvändningen markerad i den vänstra navigeringslisten.](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Overview] tab {#overview-tab}

På den här kontrollpanelen visas alla licensierade Adobe Experience Platform-produkter, inklusive tillägg, i ett tabellformat. Tabellen innehåller viktig information om licensanvändningen för alla tillgängliga profiler.

| Kolumnnamn | Beskrivning |
|---|---|
| **[!UICONTROL Product]** | Adobe-lösningen som licensieras av er organisation. |
| **[!UICONTROL Primary Metric]** | Det primära mätvärdet som används för spårning inom produkten. |
| **[!UICONTROL Licence Amount]** | Det avtalade värdet för det maximala beloppet för primärt mått enligt villkoren i produktlicensavtalet. |
| **[!UICONTROL Usage]** | Mängden av ditt primära mått som används. Det här värdet anger den totala användningen av det måttet i alla sandlådor, antingen produktion eller utveckling. |
| **[!UICONTROL Usage %]** | Procentandelen av det primära mätvärdet som används i enlighet med licensbeloppet. |

>[!NOTE]
>
>Tillägg till [!UICONTROL Licence Amount] som ett resultat av tillägg läggs till ovanpå [!UICONTROL Licence Amount] för basprodukter som Real-Time Customer Data Profile, Adobe Journey Optimizer och Customer Journey Analytics. Användningen av det licensierade beloppet (efter tilläggen) spåras genom basprodukterna. Om du till exempel köper ett paket med fem sandlådor läggs kvantiteten på fem till basproduktens. I det här fallet visas en [!UICONTROL Licence Amount] av ett, och användningen för det tillägget är&quot;tom&quot; när användningen spåras genom basprodukten.

Tabellen visar det primära måttet för varje produkt, eftersom varje produkt kan spåra flera mätvärden. Välj ett produktnamn i listan om du vill se fler mätvärden och detaljerade insikter om hur produktlicensen används. The [!UICONTROL Summary] visas.

## [!UICONTROL Summary] tab {#summary-tab}

Alla tillgängliga mått visas på [!UICONTROL Summary] -fliken. Vilka mätvärden som är tillgängliga beror på vilken produkt som är licensierad. Den här vyn innehåller **en samlad vy över alla mätvärden i alla produktions- eller utvecklingssandlådor**. Samma analysnivå erbjuds för både produktions- och utvecklingssandlådor.

![Sammanfattningsvyn för en plattformsprodukt som visar alla tillgängliga mätvärden för den produkten.](../images/license-usage/summary-tab.png)

På fliken Sammanfattning innehåller tabellen [!UICONTROL Metric] kolumn. Dessa beskrivningar som kan läsas av människor visar alla mätvärden som används för den typen av sandlåda.

### Markera en sandlåda {#select-sandbox}

Om du vill ändra vyn mellan sandlådetyperna produktion och utveckling väljer du antingen [!UICONTROL Production sandboxes] eller [!UICONTROL Development sandboxes]. Den valda sandlådetypen indikeras av alternativknappen bredvid namnet på sandlådan.

Konsumtionsrapportering för sandlådor är kumulativ för alla sandlådor av samma typ. med andra ord, markera [!UICONTROL Production] eller [!UICONTROL Development] innehåller förbrukningsrapporter för alla produktions- respektive utvecklingssandlådor.

![Sammanfattningsvyn för en plattformsprodukt med produktionssandlådor och utvecklingssandlådor markerade.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>Behörighet att visa kontrollpanelen för licensanvändning måste anges på sandlådenivå. Du måste lägga till behörigheter i varje enskild sandlåda för att kunna visa dem på kontrollpanelen. Denna begränsning kommer att åtgärdas i en framtida version. Under tiden finns följande lösning:
>
>1. Skapa en produktprofil i Adobe Admin Console.
>2. Under Behörighet i kategorin Sandbox lägger du till alla sandlådor som du vill visa på kontrollpanelen för licensanvändning.
>3. Lägg till behörigheten Visa kontrollpanel för licensanvändning under Behörighetskategorin för användarinstrumentpanelen.

## The [!UICONTROL Details] tab {#details-tab}

För att se **ett visst användningsmått från en viss sandlåda**, navigera till [!UICONTROL Details] -fliken. The [!UICONTROL Details] visas alla tillgängliga sandlådor i antingen produktions- eller utvecklingssandlådan.

![Fliken Information på kontrollpanelen för licensanvändning.](../images/license-usage/details-tab.png)

I den här vyn kan du välja ![Ikonen Inspektera.](../images/license-usage/inspect-icon.png) bredvid namnet på en sandlåda för att visa visualiseringen för det måttet. En dialogruta öppnas med en visualisering för det måttet.

### Visualiseringar {#visualizations}

Varje visualiseringswidget innehåller följande aspekter:

- Ett linjediagram som spårar måttförändringen över tid
- En tangent för linjediagrammet
- Namn på sandlådan
- En listruta där du kan justera tidsperioden för linjediagrammet

I linjediagrammen jämförs organisationens användarnummer med det totala antalet som finns tillgängligt med din organisations licens och en procentandel av den totala användningen.

![Visualisering av ett mätresultat.](../images/license-usage/visualization.png)

Analysperioden kan justeras i listrutan. Standardvärdet för de senaste 30 dagarna

Om du vill välja ett datumintervall kan du använda listrutan för datumintervall och välja vilken tidsperiod som ska visas på instrumentpanelen. Det finns flera tillgängliga alternativ, bland annat standardvärdet för de senaste 30 dagarna.

![Visualiseringsdialogrutan med listrutan för datumintervall markerad.](../images/license-usage/date-range.png)

Du kan också välja **[!UICONTROL Custom date]** för att välja den tidsperiod som visas.

![Kontrollpanelens översiktsflik för licensanvändning med anpassade datumintervallalternativ markerade.](../images/license-usage/custom-date-range.png)

## Tillgängliga mått

Kontrollpanelen för licensanvändning rapporterar om flera unika mätvärden som gäller för flera produkter i organisationen. Tillgängliga mätvärden är:

- [!UICONTROL Number of sandboxes]
- [!UICONTROL Addressable Audience]
- [!UICONTROL Average profile richness]
- [!UICONTROL Core hours]
- [!UICONTROL Data lake storage]
- [!UICONTROL Data scanned per segmentation ratio]
- [!UICONTROL Engageable audience]
- [!UICONTROL Total consumed storage]
- [!UICONTROL Total storage]
- [!UICONTROL Query Service Compute Hours]

Vilka mätvärden som är tillgängliga och vilken definition som finns för varje mätvärde varierar beroende på vilken licensiering din organisation har köpt. Detaljerade definitioner av mätvärdena finns i produktbeskrivningsdokumentationen:

| Licens | Produktbeskrivning |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, App Services och Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT KUNDDATAPLATTFORM:OD</li><li>RT KUNDDATAPLATTFORM:OD PRFL TILL 10 MB</li><li>RT KUNDDATAPLATTFORM:OD PRFL TO 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD-AKTIVERING</li><li>AEP:OD ACTIVATION PRFL TO 10M</li><li>AEP:OD ACTIVATION PRFL UPP TILL 50 MB</li></ul> | [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:ORDNING AV OD-PROFIL</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Kontrollpanelen för licensanvändning rapporterar bara den senaste licensen som har etablerats för din organisation. Om den senaste licensen för din organisation inte visas i tabellen ovan kanske kontrollpanelen för licensanvändning inte visas korrekt. Stöd för ytterligare licenser och flera licenser i en och samma organisation planeras för en framtida release.

## Nästa steg

När du har läst det här dokumentet kan du hitta kontrollpanelen för licensanvändning och visa användningsstatistik för varje köpt produkt, för alla produktions- eller utvecklingssandlådor och för en viss sandlåda. Du kan hitta mer information om tillgängliga mätvärden för din organisation, baserat på vilken licensiering din organisation har köpt.

Mer information om andra funktioner i användargränssnittet i Experience Platform finns i [Användargränssnittshandbok för plattformen](../../landing/ui-guide.md).
