---
title: Versionsinformation om Adobe Experience Platform oktober 2024
description: Versionsinformationen för Adobe Experience Platform i oktober 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f30a124a40928abf69366d311131e353c2779191
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 29 oktober 2024**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)
- [Datainsamling](#data-collection-)
- [Mål ](#destinations)
- [Segmenteringstjänst](#segmentation-service)
- [Sandlådor](#sandboxes)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Distiller-mallar för data | Utforska flera mallar för att få strukturerade insikter om målgruppsdata. Använd instrumentpaneler som **Avancerat[!UICONTROL Audience Overlaps]**, **[!UICONTROL Audience Comparison]**, **[!UICONTROL Audience Trends]** och **[!UICONTROL Audience Identity Overlaps]** för att fatta datadrivna beslut, optimera segmentering och förbättra engagemangsstrategier. Mer information finns i [guiden för Distiller-mallar](../../dashboards/sql-insights-query-pro-mode/templates/overview.md). |
| Avancerade målgruppsöverlappningar | Analysera snabbt olika målgruppsprofiler för specifika målgrupper eller se alla överlappningar för att hitta värdefulla insikter i hela er målgruppsuppsättning. Använd dessa insikter för att förfina segmenteringen, minska antalet redundanta meddelanden och skapa mer målinriktade kampanjer för ökad marknadsföringseffektivitet. Mer information finns i guiden [Avancerad publiköverlappning](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md). |
| Förbättringar av målgruppsjämförelse | Visa en jämförelse sida vid sida av nyckelvärden mellan olika målgruppsgrupper med kontrollpanelen **Måljämförelse**. Med den här kontrollpanelen kan du välja specifika tidsramar och nyckeltal, som målgruppsstorlek och identitetssammansättning, för att fatta mer välgrundade beslut om målgruppssegmentering och målinriktningsstrategier. Läs [Målgruppsjämförelseguiden](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) om du vill ha mer information. |
| Visualisering av målgruppstrender | Analysera målgruppsmått över tid med kontrollpanelen **[!UICONTROL Audience Trends]**. Visualisera trender för målgruppsstorlek, antal identiteter och antal enskilda identitetsprofiler för att hjälpa er att övervaka målgruppsutvecklingen, mäta tillväxt och förfina era engagemangsstrategier. Mer information finns i [handboken om målgruppstrender](../../dashboards/sql-insights-query-pro-mode/templates/trends.md). |
| Analys av identitetsåsidosättningar | Analysera identitetsöverlappningar i valda målgrupper med kontrollpanelen **[!UICONTROL Audience Identity Overlaps]**. Visa identitetstrender och uppdelningar för att förstå hur olika identitetstyper relaterar inom er målgrupp, förbättra sammanslagningen av identiteter och förbättra kundsegmenteringens precision. Mer information finns i guiden [Överlappning av publikidentitet](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md). |

{style="table-layout:auto"}

Mer information om kontrollpaneler, inklusive hur du ger åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa [översikten för kontrollpaneler](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en rad olika tekniker som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Taggar och tillägg | Vy av Adobe Analytics JSON | Nu kan du använda taggtillägget Adobe Analytics för att undersöka inställningar för eVars, props och händelser som JSON, som nu kan inkluderas i Web SDK-tillägget och exporteras och redigeras. Du kan också överföra eller kopiera dessa data och lagra dem på din enhet. Se [dokumentationen för Adobe Analytics-tillägget](../../tags/extensions/client/analytics/overview.md) för mer information. |

{style="table-layout:auto"}

Mer information finns i [översikten över datainsamling](../../collection/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| ----------- | ----------- |
| [Stöd för matrisexport är tillgängligt för alla](../../destinations/ui/export-arrays-calculated-fields.md) | Alla kunder kan nu använda alternativet **[!UICONTROL Add calculated field]** när målgrupper aktiveras *till filbaserade mål* för att exportera hela matriser eller element med matriser. Observera att du fortfarande måste använda funktionen `array_to_string` för att förenkla matrisen till en sträng i målfilen. <br> ![Lägg till beräknad fältmarkering med funktioner och fält.](../2024/assets/october/array-export.gif "Lägg till beräknat fält med en markering av funktionen array_to_string och organisationsmatrisen."){width="250" align="center" zoomable="yes"} |
| [Förbättringar av rapporteringsnoggrannhet för strömningsmål](/help/destinations/ui/export-datasets.md) | Från och med oktober 2024 lanserar Adobe en uppdatering som ökar rapporteringsnoggrannheten för strömningsmål. Förbättringen tillför bättre justering mellan rapporteringen för Experience Platform och målplattformarna. <br> Före den här uppdateringen innehöll **[!UICONTROL Identities failed]** alla aktiveringsåterförsök. Efter den här uppdateringen inkluderas endast det senaste aktiveringsåterförsöket i det totala antalet. <br> Förbättringen gäller för närvarande för [Google Customer Match-mål](../../destinations/catalog/advertising/google-customer-match.md), men den kommer gradvis att lanseras till andra strömningsmål för Experience Platform. Efter förbättringen kan användare av [Google Customer Match-mål](../../destinations/catalog/advertising/google-customer-match.md) se färre **[!UICONTROL Identities failed]**, vilket är helt normalt. |
| Flexibla implikationer för målgruppsutvärderingar för [gruppaktivering av målgrupper](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Om du kör [flexibel målgruppsutvärdering](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) för målgrupper som redan är inställda på att aktiveras efter segmentutvärderingen kommer målgrupperna att aktiveras så snart det flexibla målgruppsutvärderingsjobbet har slutförts, oavsett om det utförts tidigare dagliga aktiveringsjobb. <br> Detta kan leda till att målgrupper exporteras flera gånger om dagen baserat på vilka åtgärder du kör. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| [!BADGE Begränsad tillgänglighet]{type=Informative} Flexibel målgruppsutvärdering | Med flexibel målgruppsutvärdering kan ni snabbt skapa nya målgrupper på begäran för tidskänslig kommunikation. Mer information om den nya funktionen finns i [dokumentationen för målgruppsportalen](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

För mer information om [!DNL Segmentation Service] kan du läsa [segmenteringsöversikten](../../segmentation/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Platform-sinstans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Dela verktygspaket för sandlådan | Nu kan du använda verktyg i sandlådan för att enkelt exportera och importera sandlådekonfigurationer mellan sandlådor från olika organisationer. Det finns nu två kategorier med delade paket:<br><ul><li>**[Privat paket](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** Använd privat paketdelning med organisationer som har godkänt delningsbegäran från källorganisationen.</li><li>**[Offentligt paket](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** Offentliga paket kan delas utan ytterligare godkännanden och kan enkelt importeras med paketets nyttolast.</li></ul><br>Se guiden om att [dela paket mellan organisationer](../../sandboxes/ui/sharing-packages-across-orgs.md) för mer information. |
| [Paketdelning](https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) i API för verktyg i sandlådan | Använd API för verktyg i sandlådan för att göra förfrågningar till två nya slutpunkter,`/handshake` och `/transfer` för att dela mellan organisationer, samt hämta och skapa av begäranden om paketdelning. En ytterligare begäran har lagts till i slutpunkten `/packages` för att hämta nyttolasten från ett paket. |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för filtrering av standardenheter för aktivitet i [!DNL Marketo Engage] | Du kan använda [!DNL Flow Service] API för att filtrera standardenheter för aktivitet när du hämtar data från källan [!DNL Marketo Engage]. Läs guiden om att [filtrera [!DNL Marketo] standardaktivitetsdata](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage) för mer information. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).