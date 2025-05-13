---
keywords: Experience Platform;användargränssnitt;användargränssnitt;anpassning;kontrollpanel för licensanvändning;kontrollpanel;licensanvändning;berättigande;förbrukning
title: Kontrollpanel för licensanvändning
description: Adobe Experience Platform tillhandahåller en kontrollpanel där du kan visa viktig information om din organisations licensanvändning.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '3292'
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
>abstract="Beräkningstimmar mäter den tid som Query Service-motorer lägger på att läsa, bearbeta och skriva data när gruppfrågor körs.<br>Användningen kan nå det licensierade antalet. Om du vill utvärdera eller minska användningen går du till Frågor > Logg och granskar frågehistoriken. Om du inte har åtkomst till arbetsytan Frågor kontaktar du administratören."
>additional-url="https://experience.adobe.com/#/platform/query/log.html" text="Arbetsytan Frågelogg"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="Förutsedd adresserbar publik"
>abstract="Den adresserbara målgruppen är den uppsättning personprofiler i kundprofilen i realtid som din organisation har rätt att engagera. Detta mätresultat inkluderar både direkt identifierbara och pseudonyma profiler.<br>Användningen kan nå det licensierade antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="Förutsägda engagerande profiler"
>abstract="Engagerande profiler är personprofiler i realtidskundprofilen som din organisation har försökt att använda Journey Optimizer under de senaste 12 månaderna.<br>Användningen kan nå det licensierade antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="Profil för predicerad affärsperson"
>abstract="Affärspersonprofiler är poster i realtidskundprofil som representerar individer i B2B-sammanhang.<br>Användningen kan nå det licensierade antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="Förväntade kärntimmar"
>abstract="Kärntimmarna representerar bearbetningstid som förbrukas av Experience Platform tjänster.<br>Användningen kan nå det licensierade antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="Förväntad total datavolym"
>abstract="Total datavolym är den mängd data som finns tillgängliga i kundprofilen i realtid för användning i engagemangs- och personaliseringsarbetsflöden.<br>Användningen kan nå det licensierade antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="Förutsedda CJA-rader tillgängliga"
>abstract="Tillgängliga CJA-rader avser de dagliga genomsnittliga dataraderna som är tillgängliga för analys i Customer Journey Analytics.<br>Användningen kan nå det licensierade antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_addressableaudience"
>title="Förutsedd adresserbar publik"
>abstract="Den adresserbara målgruppen är den uppsättning personprofiler i kundprofilen i realtid som din organisation har rätt att engagera. Detta inkluderar både direkt identifierbara och pseudonyma profiler.<br>Användningen har överskridit det tillåtna antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_engageableprofiles"
>title="Förutsägda engagerande profiler"
>abstract="Engagerande profiler är personprofiler i realtidskundprofilen som din organisation har försökt att använda Journey Optimizer under de senaste 12 månaderna.<br>Användningen har överskridit det tillåtna antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_businesspersonprofile"
>title="Profil för predicerad affärsperson"
>abstract="Affärspersonprofiler är poster i realtidskundprofil som representerar individer i B2B-sammanhang.<br>Användningen har överskridit det tillåtna antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_corehours"
>title="Förväntade kärntimmar"
>abstract="Kärntimmarna representerar bearbetningstid som förbrukas av Experience Platform tjänster.<br>Användningen har överskridit det tillåtna antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_totaldatavolume"
>title="Förväntad total datavolym"
>abstract="Total datavolym är den mängd data som finns tillgängliga i kundprofilen i realtid för användning i engagemangs- och personaliseringsarbetsflöden.<br>Användningen har överskridit det tillåtna antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_cjaRowsAvailable"
>title="Förutsedda CJA-rader tillgängliga"
>abstract="Tillgängliga CJA-rader avser de dagliga genomsnittliga dataraderna som är tillgängliga för analys i Customer Journey Analytics.<br>Användningen har överskridit det tillåtna antalet. Om du vill minska användningen konfigurerar du datauppsättningen eller pseudonyma utgångsdatum för profildata."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="Förfallodatum för upplevelsehändelser"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

Du kan visa viktig information om din organisations licensanvändning via Adobe Experience Platform [!UICONTROL License usage]-kontrollpanelen. Den information som visas här fångas in vid en daglig ögonblicksbild av din Experience Platform-instans.

Licensanvändningsrapporter ger en hög grad av granularitet. De flesta mätvärden delas mellan flera produkter och återspeglar den samlade användningen för alla produkter som använder dem, inte för summor per produkt. Kontrollpanelen tillhandahåller konsoliderad användning av dessa mått i alla produktions- eller utvecklingssandlådor samt användningsmått från en viss sandlåda. Följande Experience Platform-program kan spåras med användningsstatistik: Real-Time Customer Data Platform, Adobe Journey Optimizer och Customer Journey Analytics.

I den här handboken beskrivs hur du får åtkomst till och arbetar med kontrollpanelen för licensanvändning i användargränssnittet och den innehåller mer information om de visualiseringar som visas på kontrollpanelen.

En allmän översikt över användargränssnittet i Experience Platform finns i [användargränssnittshandboken för Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL License usage] instrumentpanelsdata

Kontrollpanelen [!UICONTROL License usage] visar en lista över alla Experience Platform-produkter som du har köpt och eventuella tillägg för dessa produkter. Från den här kontrollpanelen hittar du en ögonblicksbild av din organisations licensrelaterade data för Experience Platform i alla associerade sandlådor.

Informationen i den här instrumentpanelen visas exakt som den såg ut vid den specifika tidpunkten när ögonblicksbilden togs. Det är inte en uppskattning eller ett exempel, men instrumentpanelen uppdateras inte i realtid.

>[!NOTE]
>
>De flesta mätvärden på kontrollpanelen uppdateras dagligen utifrån en ögonblicksbild av din Experience Platform-instans. [!UICONTROL CJA Rows Available] är ett undantag och uppdateras varje månad. Mätvärden som är märkta med &quot;paket&quot;, som [!UICONTROL Adhoc Query Service Users Packs], [!UICONTROL Profile Richness No of Packs] och [!UICONTROL Streaming Segmentation No of Packs], återspeglar licensberättiganden för tilläggserbjudanden och spårar inte pågående användning. Ändringar som görs efter ögonblicksbilden visas inte förrän nästa ögonblicksbild tas.

## Utforska kontrollpanelen för licensanvändning {#explore}

Om du vill navigera till kontrollpanelen för licensanvändning i Experience Platform-användargränssnittet väljer du **[!UICONTROL License usage]** i den vänstra listen. Kontrollpanelen innehåller två flikar: **[!UICONTROL Metrics]** och **[!UICONTROL Products]**.

>[!NOTE]
>
>Kontrollpanelen för licensanvändning är inte aktiverad som standard. Användarna måste ha behörigheten Visa kontrollpanel för licensanvändning för att kunna visa kontrollpanelen. Anvisningar om hur du beviljar åtkomstbehörigheter finns i [handboken om behörigheter på kontrollpanelen](../permissions.md).

## Fliken [!UICONTROL Metrics] {#metrics-tab}

Fliken **[!UICONTROL Metrics]** ger en centraliserad vy över alla användningsvärden för licenser i organisationen. Eftersom de flesta mätvärden delas mellan olika produkter finns det ingen separat uppdelning per produkt för dessa mätvärden.

Mättabellen innehåller följande kolumner:

| Kolumnnamn | Beskrivning |
|---|---|
| **[!UICONTROL Metric Name]** | Namnet på användningsmåttet för licensen. Varje post innehåller en informationsikon (`ⓘ`) som visar en beskrivning och en lista över associerade produkter. |
| **[!UICONTROL Licensed]** | Antalet enheter som din organisation har rätt att använda, enligt definitionen i ditt avtal. Det här måttet är samma värde som **licensbeloppet** på fliken Produkter. |
| **[!UICONTROL Measured]** | Mängden mätvärden som används av organisationen. |
| **[!UICONTROL Usage %]** | Procentandelen av ditt licensierade värde som används för närvarande. |
| **[!UICONTROL Predicted Usage %]** | Prognostiserat intervall med mätvärden under de kommande 6 veckorna. |

Använd växlingsknappen för sandlådan **[!UICONTROL Production]** eller **[!UICONTROL Development]** för att filtrera mätvärden som visas av sandlådor.

>[!NOTE]
>
>Förbrukningsrapporteringen är kumulativ per sandlådetyp. Om du väljer [!UICONTROL Production] eller [!UICONTROL Development] visas kombinerad användning i alla sandlådor av den typen.

![På kontrollpanelen för licensanvändning visas en lista med mått, licensbelopp och användningsdata.](../images/license-usage/metrics-tab.png)

>[!WARNING]
>
>Behörighet att visa kontrollpanelen för licensanvändning måste anges på sandlådenivå. Lägg till behörigheter i varje enskild sandlåda för att visa dem på kontrollpanelen. Denna begränsning kommer att åtgärdas i en framtida version. Under tiden finns följande lösning:
>
>1. Skapa en produktprofil i Adobe Admin Console.
>2. Under Behörighet i kategorin Sandbox lägger du till alla sandlådor som du vill visa på kontrollpanelen för licensanvändning.
>3. Lägg till behörigheten Visa kontrollpanel för licensanvändning under behörighetskategorin för användarinstrumentpanelen.

### Visa måttinformation {#view-metric-details}

Om du vill visa användningsinformation för ett visst mått väljer du ett måttnamn i listan. En detaljerad vy av måttet visas, inklusive:

- Ett historiskt linjediagram som visar användning över tid
- En jämförelse av licensierade och uppmätta värden
- Användning via enskild sandlåda
- En sandlådeväljare för att filtrera data
- Ett exportalternativ för CSV-nedladdning

Med den här visualiseringen kan du spåra trender, förstå hur varje sandlåda bidrar till den övergripande användningen och exportera data för offlineanalys.

Varje diagram innehåller listrutor för att filtrera data. Använd listrutan för datumintervall för att justera uppslagsperioden (standard: senaste 30 dagar) eller använd listrutan i sandlådan för att visa användningen för en viss produktions- eller utvecklingssandlåda.

![Detaljvyn för adresserbara målgruppsmätningar med historikanvändningsdiagram, sandlådetabell och exportknapp.](../images/license-usage/metric-details-view.png)

Du kan också välja en **[!UICONTROL Custom date]** för att välja den tidsperiod som visas.

![Fliken Översikt över kontrollpanelen för licensanvändning med alternativen för anpassat datumintervall markerade.](../images/license-usage/custom-date-range.png)

### CSV-export {#export-metric-usage-data}

Du kan exportera historiska användningsdata för det valda måttet och sandlådan som en CSV-fil direkt från måttdetaljvyn. Välj ikonen **[!UICONTROL Export]** om du vill hämta diagrammets data i tabellformat. Den exporterade CSV-filen gör det enkelt att analysera trender offline eller dela användningsinformation mellan olika team.

## Fliken [!UICONTROL Products] {#products-tab}

På fliken **[!UICONTROL Products]** visas licensanvändningsdata grupperade efter inköpta produkter och eventuella associerade tillägg. Fliken [!UICONTROL Products] innehåller två tabeller:

- **[!UICONTROL Core products]table**: Den här tabellen visar de viktigaste Adobe Experience Platform-produkterna som licensierats av din organisation. Varje produkt listar sitt primära mätvärde, användningsspårning och förväntad användning.
- **[!UICONTROL Add-ons]table**: Visar fyllnadsartiklar vars licensbelopp bidrar till kärnproduktstatistik. Tillägg har inte olika mätvärden, men förbättrar användningsspårningen för de kärnprodukter de är kopplade till.

| Kolumnnamn | Beskrivning |
|---|---|
| **[!UICONTROL Product]** | Adobe-lösningen som licensieras av er organisation. |
| **[!UICONTROL Primary Metric]** | Det primära mätvärde som används för spårning inom den produkten. |
| **[!UICONTROL License Amount]** | Det avtalade värdet för den maximala mängden av det primära mätvärdet. |
| **[!UICONTROL Usage]** | Mängden av ditt primära mått som används. |
| **[!UICONTROL Usage %]** | Procentandelen av det primära mätvärdet som används i enlighet med licensbeloppet. |
| **[!UICONTROL Predicted Usage]** | Prognostiserad användningsprocent för det primära mätvärdet. |

>[!NOTE]
>
>[!UICONTROL License Amount] för tillägg ingår i kärnproduktens totala licensbelopp. Tillägg spåras inte separat utan förbättrar möjligheterna i deras tillhörande produkter. Om du till exempel köper ett paket med fem sandlådor som tillägg läggs beloppet till i basproduktens paket. Tilläggstabellen visar en [!UICONTROL License Amount] specifik för tillägget, men den faktiska användningen spåras genom basprodukten.

![Kontrollpanelen för licensanvändning - fliken Produkter med tabeller för kärnprodukter och tillägg.](../images/license-usage/products-tab.png)

### Förutsedd användning {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Förutsedd användning"
>abstract="Förutsättningarna baseras på användningen under de senaste 6-7 månaderna och genereras varje vecka varje fredag. Observera att prognoserna för licensanvändning är approximationer baserade på tidigare användning. Du ansvarar för att förstå hur din organisation faktiskt används och se till att användningen inte går utanför räckvidden för din organisations licens med Adobe. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="Automatiska förfallodatum för datauppsättningar"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Förutsedd användning"
>abstract="Förutsättningarna baseras på användningen under de senaste 6-7 månaderna och genereras den 15:e varje månad. Observera att prognoserna för licensanvändning är approximationer baserade på tidigare användning. Du ansvarar för att förstå hur din organisation faktiskt används och se till att användningen inte går utanför räckvidden för din organisations licens med Adobe. För att minska användningen kan du konfigurera datauppsättningar eller pseudonyma utgångsdatum för profildata för sandlådor och datauppsättningar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="Automatiska förfallodatum för datauppsättningar"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Förfallodatum för pseudonyma profiler"

Hantera och optimera era licensresurser proaktivt med korrekta och aktuella användningsprognoser. Kolumnen [!UICONTROL Predicted Usage] prognostiserar framtida licensanvändning på sandlådenivå för alla produktions- och utvecklingssandlådor för alla köpta produkter. Prediktionerna uppdateras nu varje vecka och innehåller en prognos för sex veckor baserat på de senaste användningsdata. Varje förutsägelse omfattar både en nedre och övre gräns för att stödja välinformerad planering.

>[!IMPORTANT]
>
>Förutsättningarna uppdateras varje vecka varje fredag. Uppdateringsdatumet ingår i en informationsikon (![Den här informationsikonen.](../images/license-usage/info-icon.png)) ovanför kolumnrubriken.

Visa en sammanfattning av en produkts tillståndsanvändning på fliken [!UICONTROL Product] under tabellen [!UICONTROL Core products].

![Fliken [!UICONTROL License usage] [!UICONTROL Product] med en produkt och den förväntade användningskolumnen markerad.](../images/license-usage/product-predicted-usage.png)

>[!NOTE]
>
>Observera att prognoserna för licensanvändning är approximationer baserade på tidigare användning. Du ansvarar för att förstå hur din organisation faktiskt används och se till att användningen inte går utanför räckvidden för din organisations licens med Adobe.

Procentandelen av förväntad användning bestäms enligt följande:

- Om de nedre och övre gränserna är avsevärt olika visas de som ett intervall (till exempel 32-35 %).
- Om de nedre och övre gränserna är nästan identiska och inte noll visas de som ett approximativt värde (till exempel ~34 %).
- Om de nedre och övre gränserna är nästan identiska och noll visas de som exakt 0 %.

>[!NOTE]
>
>&quot;Nästan identiska&quot; betyder i detta sammanhang att värdena är statistiskt signifikanta för två decimaler (till exempel är den nedre gränsen 0,342 och den övre gränsen 0,344 avrundas båda till 34 %).

Funktionen för förväntad användning har stöd för följande mått:

- [!UICONTROL Addressable audience]
- [!UICONTROL Businessperson profiles]
- [!UICONTROL Compute hours]
- [!UICONTROL Customer Journey Audience number of rows]
- [!UICONTROL Engageable profiles]
- [!UICONTROL Total Data Volume]

## Tillgängliga mått {#available-metrics}

>[!IMPORTANT]
>
>Från och med den 20 augusti såg kunder med berättiganden för [!UICONTROL Average Profile Richness] och [!UICONTROL Total Storage] i stället [!UICONTROL Total Data Volume] i kontrollpanelen för licensanvändning. Inga förändringar i kundens rättigheter, utan bara en förenkling av spårningsstatistiken. [!UICONTROL Total Data Volume] representerar de data som är tillgängliga i kundprofilen i realtid för engagemangs- och personaliseringsarbetsflöden. Detta förenklade mätresultat förbättrade hanteringen och mätningen av kundprofilanvändningen i realtid. Kunderna uppmanas att kontakta sin Adobe-representant för att få ytterligare information om denna förändring.

Kontrollpanelen för licensanvändning rapporterar om flera unika mätvärden som gäller för flera produkter i organisationen. Tillgängliga mätvärden är:

| Mått | Beskrivning |
|---|---|
| [!UICONTROL Audience Activation Size] | Den totala storleken på profiler som har aktiverats för ett filbaserat mål på ett år. Obs! Detta inkluderar inte profiler som skickas via direktuppspelningsmål. |
| [!UICONTROL Addressable Audience] | Den uppsättning personprofiler i kundprofilen i realtid som din organisation har rätt att använda, inklusive både direkt identifierbara och pseudonyma profiler. Dessa profiler kan innehålla attribut, beteenden och data om segmentmedlemskap. Profilvolymer beräknas med Adobe Experience Platform standarddeterministiska identitetsdiagram och betraktas som en delad funktion. |
| [!UICONTROL Adhoc Query Service Users Packs] | Ett tillägg som ökar dina behörigheter för samtidiga frågetjänstanvändare med ytterligare fem samtidiga frågetjänstanvändare och ytterligare en ad hoc-fråga som körs samtidigt per paket. Flera ytterligare Ad hoc-frågeanvändarpaket kan licensieras. |
| [!UICONTROL Average profile richness] | **Borttagen** - Summan av alla produktionsdata som lagras i navprofiltjänsten vid någon tidpunkt, dividerat med fem gånger antalet auktoriserade affärspersonsprofiler. [!UICONTROL Average profile richness] är en delad funktion. |
| [!UICONTROL CJA Rows Available] | De dagliga genomsnittliga dataraderna som är tillgängliga för analys inom Customer Journey Analytics. |
| [!UICONTROL Computed Attributes] | Samlade profilbeteendedata baserade på upplevelsehändelser som konverteras till ett profilattribut och kan inkluderas i en personprofil. |
| [!UICONTROL Consumer Audience] | Antalet personprofiler som identifieras som&quot;Konsumentpublik&quot; på försäljningsordern. |
| [!UICONTROL Data Export Size] | Mängden data som skickas via datauppsättningsaktiveringar under ett år. |
| [!UICONTROL Data Exports] | Den totala storleken på datauppsättningar som kan exporteras till andra lösningar än Adobe (direkt eller indirekt) under ett år. |
| [!UICONTROL Data Lake Storage] | Den kvantitet som används i analysdatalagret i Adobe Experience Platform. |
| [!UICONTROL Engageable Audience] | En grupp personprofiler i kundprofilen i realtid som du har försökt att engagera under de senaste 12 månaderna med Journey Optimizer funktioner för att skapa, fatta beslut, leverera, experimentera eller orkestrera. |
| [!UICONTROL Look-alike Audiences] | En konsumentlookalike-målgrupp är en målgrupp som genereras genom att modellera en befintlig konsumentpublik för att identifiera personprofiler med liknande attribut eller beteenden. |
| [!UICONTROL Number of AMM Models] | Antal maskininlärningsmodeller (inbyggda Adobe Mix Modeler) som används för att mäta och/eller förutsäga ett specifikt resultat baserat på dina investeringar. |
| [!UICONTROL Number of Sandboxes] | Antalet logiska separationer i din instans av en Adobe On-demand-tjänst som använder Adobe Experience Platform för att isolera data och åtgärder. |
| [!UICONTROL Profile Richness No of Packs] | En ökning av din auktoriserade totala datavolym med 25 kB per profil för varje ytterligare profilnoggrannhetspaket. |
| [!UICONTROL Query Service Compute Hours] | Ett mått på hur lång tid det tar för frågetjänstmotorerna att läsa, bearbeta och skriva data tillbaka till datasjön när en batchfråga körs. |
| [!UICONTROL Streaming Segmentation No of Packs] | Paketuppdateringssegmentmedlemskapet för en personprofil när nya data matas in i segmenteringstjänsten via ett strömningsflöde. Segmentmedlemskap utvärderas baserat på attributen för den aktuella personprofilen och värdet för den aktuella händelsen, utan hänsyn till historiskt beteende. Direktuppspelningssegmentering är en delad funktion. |
| [!UICONTROL Total Data Volume] | Den totala mängden data som är tillgängliga för kundprofil i realtid som kan användas i engagemangsarbetsflöden. Total datavolym beräknas med följande formel: **Total datavolym = adresserbar publik × genomsnittlig profilnoggrannhet**. Detta mätresultat återger data som bara lagras i Profile Store och utesluter lagring av data Lake. Det ger en mer fokuserad bild av data som är relevanta för profilbaserat engagemang. Läs [vanliga frågor om Total Data Volume](../../landing/license-usage-and-guardrails/total-data-volume.md) om du vill veta mer. |
| [!UICONTROL Total Volume of Data Egress] | Den sammanlagda årliga datavolymen som exporteras från Adobe Experience Platform till datalager från tredje part. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Du kan kontrollera dina licensrättigheter i din försäljningsorder för att beräkna mätvärden som din &#39;Lagringstilldelning&#39;.<br>Exempel:<ul><li>Lagringsutrymme = Antalet &quot;auktoriserade profiler&quot; i ditt kontrakt X Genomsnittlig profilnoggrannhet</li></ul>

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

Om du vill veta mer om andra funktioner som är tillgängliga i användargränssnittet för Experience Platform kan du läsa [användargränssnittshandboken för Experience Platform](../../landing/ui-guide.md).
