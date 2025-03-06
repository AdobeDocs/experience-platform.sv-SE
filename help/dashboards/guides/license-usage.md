---
keywords: Experience Platform;användargränssnitt;användargränssnitt;anpassning;kontrollpanel för licensanvändning;kontrollpanel;licensanvändning;berättigande;förbrukning
title: Kontrollpanel för licensanvändning
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om din organisations licensanvändning.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 1c31ef58eec727638cab28202afc762da0e226a2
workflow-type: tm+mt
source-wordcount: '2990'
ht-degree: 0%

---

# Kontrollpanel för licensanvändning {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Testdialogruta som inte ska visas"
>abstract="Objektet {name} visas på {date}."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Tabell över kärnprodukter"
>abstract="De kärnprodukter som listas i tabellen har egna mätvärden, användningsspårning och detaljerade vyer på sandlådenivå. Dessa kärnprodukter ger nyckelmätvärden för spårning, och eventuella tillägg ingår i dessa mätvärden."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Register för tillägg"
>abstract="I tilläggstabellen listas produkter vars licensbelopp kombineras med de värden som stöds av kärnprodukterna. Tilläggen har inte olika mätvärden, men förbättrar användningsspårningen för de kärnprodukter de är kopplade till."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Kontrollpanel för licensanvändning"
>abstract="Kontrollpanelen för licensanvändning ger dig insikt i vilka Adobe Experience Platform-produkter du har köpt. I översikten på kontrollpanelen visas de primära mätvärdena för dina produkter, inklusive din användning för var och en av de primära mätvärdena och ditt avtalade licensbelopp. På arbetsytan Detaljer visas en beskrivning av dina mätvärden för varje produkt i specifika sandlådor."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="Automatiska förfallodatum för datauppsättningar"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Kontrollpanel för licensanvändning"
>abstract="Kontrollpanelen för licensanvändning ger dig insikt i vilka Adobe Experience Platform-produkter du har köpt. I översikten på kontrollpanelen visas de primära mätvärdena för dina produkter, inklusive din användning för var och en av de primära mätvärdena och ditt avtalade licensbelopp. På arbetsytan Detaljer visas en beskrivning av dina mätvärden för varje produkt i specifika sandlådor."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="Automatiska förfallodatum för datauppsättningar"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_computehours"
>title="Förutsagda beräkningstimmar"
>abstract="Användningen kan nå den tillåtna mängden. Om du vill utvärdera eller minska beräkningstiden går du till Frågor > Logg och granskar frågehistoriken. Om du inte har behörighet att komma åt arbetsytan Frågor kontaktar du administratören."
>additional-url="https://experience.adobe.com/#/platform/query/log.html" text="Arbetsytan Frågelogg"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="Förutsedd adresserbar publik"
>abstract="Användningen kan nå den tillåtna mängden. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="Förutsägda engagerande profiler"
>abstract="Användningen kan nå den tillåtna mängden. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="Profil för predicerad affärsperson"
>abstract="Användningen kan nå den tillåtna mängden. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="Förväntade kärntimmar"
>abstract="Användningen kan nå den tillåtna mängden. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="Förväntad total datavolym"
>abstract="Användningen kan nå den tillåtna mängden. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="Förutsedda CJA-rader tillgängliga"
>abstract="Användningen kan nå den tillåtna mängden. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

Du kan visa viktig information om din organisations licensanvändning via Adobe Experience Platform [!UICONTROL License usage]-kontrollpanelen. Den information som visas här fångas in vid en daglig ögonblicksbild av din Platform-instans.

Licensanvändningsrapporter ger en hög grad av granularitet över era användningsvärden för licenser. Kontrollpanelen tillhandahåller användningsstatistik för varje köpt produkt (och tillhörande tillägg), konsoliderad användning av statistik i alla produktions- eller utvecklingssandlådor samt användningsstatistik från en specifik sandlåda. Följande Experience Platform-program kan spåras med användningsstatistik: Real-Time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics.

I den här handboken beskrivs hur du får åtkomst till och arbetar med kontrollpanelen för licensanvändning i användargränssnittet och den innehåller mer information om de visualiseringar som visas på kontrollpanelen.

En allmän översikt över användargränssnittet för plattformen finns i [användargränssnittshandboken för Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL License usage] instrumentpanelsdata

Kontrollpanelen [!UICONTROL License usage] visar en lista över alla Experience Platform-produkter som du har köpt och eventuella tillägg för dessa produkter. Från den här kontrollpanelen hittar du en ögonblicksbild av din organisations licensrelaterade data för Experience Platform i alla associerade sandlådor.

Informationen i den här instrumentpanelen visas exakt som den visas vid den specifika tidpunkt då ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och instrumentpanelen uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

## Utforska kontrollpanelen för licensanvändning {#explore}

Om du vill navigera till kontrollpanelen för licensanvändning i plattformsgränssnittet väljer du **[!UICONTROL License usage]** i den vänstra listen. Fliken [!UICONTROL Overview] öppnas och visar en lista över tillgängliga produkter.

>[!NOTE]
>
>Kontrollpanelen för licensanvändning är inte aktiverad som standard. Användarna måste beviljas behörigheten &quot;Visa kontrollpanel för licensanvändning&quot; för att kunna visa kontrollpanelen. Anvisningar om hur du beviljar åtkomstbehörigheter för att visa kontrollpanelen för licensanvändning finns i [behörighetsguiden för kontrollpanelen](../permissions.md).

![Fliken Översikt över kontrollpanelen för licensanvändning, med licensanvändningen markerad i det vänstra navigeringsfältet.](../images/license-usage/dashboard-overview.png)

## Fliken [!UICONTROL Overview] {#overview-tab}

Kontrollpanelen [!UICONTROL License Usage] visar två separata tabeller: **Core products** och **Add-ons**.

- **[!UICONTROL Core products]table**: Den här tabellen visar de viktigaste Adobe Experience Platform-produkterna som licensierats av din organisation. Varje kärnprodukt har egna mått, användningsspårning och detaljerade vyer på sandlådenivå. Dessa kärnprodukter ger nyckelmätvärden för spårning, och eventuella tillägg ingår i dessa mätvärden.

- **[!UICONTROL Add-ons]table**: Den här tabellen visar ytterligare produkter vars licensbelopp kombineras med de värden som stöds av kärnprodukterna. Tillägg har inte olika mätvärden, men förbättrar användningsspårningen för de kärnprodukter de är kopplade till.

| Kolumnnamn | Beskrivning |
|---|---|
| **[!UICONTROL Product]** | Adobe-lösningen som licensieras av er organisation. |
| **[!UICONTROL Primary Metric]** | Det primära mätvärde som används för spårning inom den produkten. |
| **[!UICONTROL License Amount]** | Det avtalade värdet för det maximala beloppet för primärt mått enligt villkoren i produktlicensavtalet. |
| **[!UICONTROL Usage]** | Mängden av ditt primära mått som används. Det här värdet anger den totala användningen av det måttet i alla sandlådor, antingen produktion eller utveckling. |
| **[!UICONTROL Usage %]** | Procentandelen av det primära mätvärdet som används i enlighet med licensbeloppet. |
| **[!UICONTROL Prediction Usage]** | Prognostiserad användningsprocent av det primära mätvärdet enligt licensbeloppet. |

>[!NOTE]
>
>Licensbelopp för tillägg ingår i [!UICONTROL License Amount] för kärnprodukterna. Om du till exempel köper ett paket med fem sandlådor som tillägg läggs beloppet till i basproduktens paket. Tilläggstabellen visar en [!UICONTROL License Amount] specifik för tillägget, men den faktiska användningen spåras genom basprodukten.

Tabellerna anger det primära måttet för varje produkt, eftersom varje produkt kan spåra flera mätvärden.

### Förutsedd användning {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Förutsedd användning"
>abstract="Förutsättningarna baseras på användningen under de senaste 6-7 månaderna och genereras den 15:e varje månad. Observera att prognoserna för licensanvändning är approximationer baserade på tidigare användning. Du ansvarar för att förstå hur din organisation faktiskt används och se till att användningen inte går utanför räckvidden för din organisations licens med Adobe. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="Automatiska förfallodatum för datauppsättningar"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Förutsedd användning"
>abstract="Förutsättningarna baseras på användningen under de senaste 6-7 månaderna och genereras den 15:e varje månad. Observera att prognoserna för licensanvändning är approximationer baserade på tidigare användning. Du ansvarar för att förstå hur din organisation faktiskt används och se till att användningen inte går utanför räckvidden för din organisations licens med Adobe. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="Automatiska förfallodatum för datauppsättningar"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

Hantera och optimera era licensieringsresurser proaktivt baserat på insiktsfulla användningsprognoser. Kolumnen [!UICONTROL Predicted Usage] förutsäger exakt framtida licensanvändning på sandlådenivå, för alla produktions- och utvecklingssandlådor, för alla köpta produkter. Denna varningsfunktion ger en prognos över licensanvändningen för sex veckor i framtiden, baserat på din användning fram till den 15 i den här kalendermånaden. Förutsägelser har en nedre och en övre gräns.

>[!IMPORTANT]
>
>Förutsättningarna uppdateras varje månad. Uppdateringsdatumet ingår i en informationsikon (![Den här informationsikonen.](../images/license-usage/info-icon.png)) ovanför kolumnrubriken.

Om du vill se en sammanfattning av en produkts tillståndsanvändning väljer du en produkt i tabellen [!UICONTROL Core products].

![[!UICONTROL License usage] [!UICONTROL Overview] med en produkt och den förväntade användningskolumnen markerad.](../images/license-usage/product-predicted-usage.png)

Fliken Sammanfattning visas. Du kan använda de detaljerade förutsägelser som finns på flikarna [!UICONTROL Summary] och [!UICONTROL Details] för att säkerställa ett välgrundat beslutsfattande för effektiv licensanvändning.

>[!NOTE]
>
>Observera att prognoserna för licensanvändning är approximationer baserade på tidigare användning. Du ansvarar för att förstå hur din organisation faktiskt används och se till att användningen inte går utanför räckvidden för din organisations licens med Adobe.

![Sammanfattningsvyn för en plattformsprodukt med den förväntade användningskolumnen markerad.](../images/license-usage/summary-predicted-usage.png)

Procentandelen av förväntad användning bestäms enligt följande:

- Om de nedre och övre gränserna är avsevärt olika visas de som ett intervall (till exempel 32-35 %).
- Om de nedre och övre gränserna är nästan identiska och inte noll visas de som ett approximativt värde (till exempel ~34 %).
- Om de nedre och övre gränserna är nästan identiska och noll visas de som exakt 0 %.

>[!NOTE]
>
>&quot;Nästan identiska&quot; betyder i detta sammanhang att värdena är statistiskt signifikanta för två decimaler (till exempel är den nedre gränsen 0,342 och den övre gränsen 0,344 avrundas båda till 34 %).

Funktionen för förväntad användning har stöd för följande mått:

- [!UICONTROL Addressable audience]
- [!UICONTROL Compute hours]
- [!UICONTROL Customer Journey Audience number of rows]
- [!UICONTROL Total Data Volume]

## Fliken [!UICONTROL Summary] {#summary-tab}

Välj ett produktnamn i listan om du vill se fler mätvärden och detaljerade insikter om hur produktlicensen används. Vyn [!UICONTROL Summary] för den produkten visas. Alla tillgängliga mått visas på fliken [!UICONTROL Summary]. Vilka mätvärden som är tillgängliga beror på vilken produkt som är licensierad. Den här vyn ger **en konsoliderad vy över alla mått i alla produktions- eller utvecklingssandlådor**. Samma analysnivå erbjuds för både produktions- och utvecklingssandlådor.

![Sammanfattningsvyn för en plattformsprodukt som visar alla tillgängliga mätvärden för den produkten.](../images/license-usage/summary-tab.png)

På sammanfattningsfliken innehåller tabellen kolumnen [!UICONTROL Metric]. Dessa beskrivningar som kan läsas av människor visar alla mätvärden som används för den typen av sandlåda.

### Markera en sandlåda {#select-sandbox}

Om du vill ändra vyn mellan sandlådetyperna för produktion och utveckling väljer du antingen [!UICONTROL Production sandboxes] eller [!UICONTROL Development sandboxes]. Den valda sandlådetypen indikeras av alternativknappen bredvid namnet på sandlådan.

Konsumtionsrapportering för sandlådor är kumulativ för alla sandlådor av samma typ. Det innebär att om du väljer [!UICONTROL Production] eller [!UICONTROL Development] visas förbrukningsrapporter för alla produktions- respektive utvecklingssandlådor.

![Sammanfattningsvyn för en plattformsprodukt med produktionssandlådor och utvecklingssandlådor markerade.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>Behörighet att visa kontrollpanelen för licensanvändning måste anges på sandlådenivå. Lägg till behörigheter i varje enskild sandlåda för att visa dem på kontrollpanelen. Denna begränsning kommer att åtgärdas i en framtida version. Under tiden finns följande lösning:
>
>1. Skapa en produktprofil i Adobe Admin Console.
>2. Under Behörighet i kategorin Sandbox lägger du till alla sandlådor som du vill visa på kontrollpanelen för licensanvändning.
>3. Lägg till behörigheten Visa kontrollpanel för licensanvändning under behörighetskategorin för användarinstrumentpanelen.

## Fliken [!UICONTROL Details] {#details-tab}

Om du vill visa **ett visst användningsmått från en viss sandlåda** går du till fliken [!UICONTROL Details]. Fliken [!UICONTROL Details] visar alla tillgängliga sandlådor i antingen produktions- eller utvecklingssandlådan.

![Fliken Information på kontrollpanelen för licensanvändning.](../images/license-usage/details-tab.png)

I den här vyn kan du välja ![Ikonen Inspektera.](/help/images/icons/inspect.png) bredvid ett sandlådenamn för att visa visualiseringen för det måttet. En dialogruta öppnas med en visualisering för det måttet.

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

![Fliken Översikt över kontrollpanelen för licensanvändning med alternativen för anpassat datumintervall markerade.](../images/license-usage/custom-date-range.png)

## Tillgängliga mått {#available-metrics}

>[!IMPORTANT]
>
>Från och med den 20 augusti såg kunder med berättiganden för [!UICONTROL Average Profile Richness] och [!UICONTROL Total Storage] i stället [!UICONTROL Total Data Volume] i kontrollpanelen för licensanvändning. Inga förändringar i kundens rättigheter, utan bara en förenkling av spårningsstatistiken. [!UICONTROL Total Data Volume] representerar de data som är tillgängliga i Adobe Experience Platform Profile Service för interaktions- och personaliseringsarbetsflöden. Detta förenklade mätresultat förbättrade hanteringen och mätningen av användningen av profiltjänsten. Kunderna uppmanades att kontakta sin Adobe-representant för att få ytterligare information om denna förändring.

Kontrollpanelen för licensanvändning rapporterar om flera unika mätvärden som gäller för flera produkter i organisationen. Tillgängliga mätvärden är:

| Mått | Beskrivning |
|---|---|
| [!UICONTROL Audience Activation Size] | Den totala storleken på profiler som har aktiverats för ett filbaserat mål på ett år. Obs! Detta inkluderar inte profiler som skickas via direktuppspelningsmål. |
| [!UICONTROL Addressable Audience] | Summan av er rätt till företagspass och rätt till rätt målgrupp. En konsumentpublik definieras som antalet personprofiler som identifieras som en&quot;konsumentpublik&quot; på försäljningsordern. En målgrupp definieras som antalet affärspersonsprofiler som identifieras som&quot;affärsmålgrupp&quot; på försäljningsordern. |
| [!UICONTROL Adhoc Query Service Users Packs] | Ett tillägg som ökar dina behörigheter för samtidiga frågetjänstanvändare med ytterligare fem samtidiga frågetjänstanvändare och ytterligare en ad hoc-fråga som körs samtidigt per paket. Flera ytterligare Ad hoc-frågeanvändarpaket kan licensieras. |
| [!UICONTROL Average profile richness] | **Borttagen** - Summan av alla produktionsdata som lagras i navprofiltjänsten vid någon tidpunkt, dividerat med fem gånger antalet auktoriserade affärspersonsprofiler. [!UICONTROL Average profile richness] är en delad funktion. |
| [!UICONTROL CJA Rows Available] | De dagliga genomsnittliga dataraderna som är tillgängliga för analys inom Customer Journey Analytics. |
| [!UICONTROL Computed Attributes] | Det totala antalet aggregerade profilbeteendedata. Sammanlagda profilbeteendedata baseras på upplevelsehändelser som konverteras till ett profilattribut och kan inkluderas i en personprofil eller en företagsprofil. |
| [!UICONTROL Consumer Audience] | Antalet personprofiler som identifieras som&quot;Konsumentpublik&quot; på försäljningsordern. |
| [!UICONTROL Data Export Size] | Mängden data som skickas via datauppsättningsaktiveringar under ett år. |
| [!UICONTROL Data Exports] | Den totala storleken på datauppsättningar som kan exporteras till andra lösningar än Adobe (direkt eller indirekt) under ett år. |
| [!UICONTROL Data Lake Storage] | Den kvantitet som används i analysdatalagret i Adobe Experience Platform. |
| [!UICONTROL Engageable Audience] | Det här måttet avser målgruppen med profiler som kan användas. En engagerande profil är ett register med information som representerar en individ och representeras i profiltjänsten. Dessa poster är profiler som du har försökt att använda Journey Optimizer funktioner för att skapa, fatta beslut, leverera, experimentera eller orkestrera under de senaste 12 månaderna. |
| [!UICONTROL Look-alike Audiences] | Antalet målgrupper som genereras genom att en befintlig konsumentmålgrupp modelleras för att identifiera personprofiler som liknar den befintliga konsumentmålgruppen. |
| [!UICONTROL Number of AMM Models] | Antal maskininlärningsmodeller (inbyggda Adobe Mix Modeler) som används för att mäta och/eller förutsäga ett specifikt resultat baserat på dina investeringar. |
| [!UICONTROL Number of Sandboxes] | Antalet logiska separationer i din instans av en Adobe On-demand-tjänst som använder Adobe Experience Platform för att isolera data och åtgärder. |
| [!UICONTROL Profile Richness No of Packs] | En ökning av din auktoriserade totala datavolym med 25 kB per profil för varje ytterligare profilnoggrannhetspaket. |
| [!UICONTROL Query Service Compute Hours] | Ett mått på hur lång tid det tar för frågetjänstmotorerna att läsa, bearbeta och skriva data tillbaka till datasjön när en batchfråga körs. |
| [!UICONTROL Streaming Segmentation No of Packs] | Paketuppdateringssegmentmedlemskapet för en personprofil när nya data matas in i segmenteringstjänsten via ett strömningsflöde. Segmentmedlemskap utvärderas baserat på attributen för den aktuella personprofilen och värdet för den aktuella händelsen, utan hänsyn till historiskt beteende. Direktuppspelningssegmentering är en delad funktion. |
| [!UICONTROL Total Data Volume] | Den totala mängden data som är tillgängliga för Adobe Experience Platform Profile Service för användning i engagemangsarbetsflöden. Läs [vanliga frågor om Total Data Volume](../../landing/license-usage-and-guardrails/total-data-volume.md) om du vill veta mer. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Du kan kontrollera dina licensrättigheter i din försäljningsorder för att beräkna mått som din &#39;Lagringsersättning&#39;.<br>Exempel:<ul><li>Lagringsutrymme = Antalet &quot;auktoriserade profiler&quot; i ditt kontrakt X Genomsnittlig profilnoggrannhet</li></ul>

Vilka mätvärden som är tillgängliga och vilken definition som finns för varje mätvärde varierar beroende på vilken licensiering din organisation har köpt. Detaljerade definitioner av mätvärdena finns i produktbeskrivningsdokumentationen:

| Licens | Produktbeskrivning |
| --- | --- |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, App Services och Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT KUNDDATAPLATTFORM:OD</li><li>RT KUNDDATAPLATTFORM:OD PRFL TILL 10 MB</li><li>RT KUNDDATAPLATTFORM:OD PRFL TO 50M</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD-AKTIVERING</li><li>AEP:OD ACTIVATION PRFL TO 10M</li><li>AEP:OD ACTIVATION PRFL UPP TILL 50 MB</li></ul> | [Adobe Experience Platform-aktivering](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:ORDNING AV OD-PROFIL</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Kontrollpanelen för licensanvändning rapporterar bara den senaste licensen som har etablerats för din organisation. Om den senaste licensen för din organisation inte visas i tabellen ovan kanske kontrollpanelen för licensanvändning inte visas korrekt. Stöd för ytterligare licenser och flera licenser i en och samma organisation planeras för en framtida release.

## Nästa steg

När du har läst det här dokumentet kan du hitta kontrollpanelen för licensanvändning och visa användningsstatistik för varje köpt produkt, för alla produktions- eller utvecklingssandlådor och för en viss sandlåda. Du kan hitta mer information om tillgängliga mätvärden för din organisation, baserat på vilken licensiering din organisation har köpt.

Mer information om andra funktioner i Experience Platform-gränssnittet finns i [användargränssnittshandboken för plattformen](../../landing/ui-guide.md).
