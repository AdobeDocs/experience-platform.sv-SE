---
title: Versionsinformation om Adobe Experience Platform september 2024
description: Versionsinformationen för Adobe Experience Platform från september 2024.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 33d1305aef7c763e7b0bd8c6db6a1a9417cc2a9d
workflow-type: ht
source-wordcount: '2196'
ht-degree: 100%

---

# Versionsinformation om Adobe Experience Platform

**Releasedatum: 24 september 2024**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [Aviseringar](#alerts)
- [Kontrollpaneler](#dashboards)
- [Dataförberedelse](#data-prep)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Frågetjänst](#query-service)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för sandlåda för utveckling | Du kan nu [prenumerera på aviseringar](../../observability/alerts/ui.md) i både produktions- och utvecklingssandlådor, vilket möjliggör sömlös övervakning i alla miljöer. |
| E-postmallar | [E-postaviseringar](../../observability/alerts/ui.md) innehåller nu detaljerad resursinformation, vilket garanterar att du har all viktig information nära till hands. |
| Förbättrad anpassning | Du kan nu konfigurera [aviseringströsklar](../../observability/alerts/ui.md#alert-threshold) vilket ger större flexibilitet att skräddarsy aviseringar efter dina specifika behov för följande aviseringstyper:<br><ul><li>Fördröjning av segmentjobb</li><li>Fördröjning av segmentexport</li><li>Körningsfördröjning för destinationsflöde</li><li>Körningsfördröjning för identitetstjänstens flöde</li><li>Körningsfördröjning för profilflöde</li><li>Körningsfördröjning för källflöde</li><li>Frågekörningsfördröjning</li><li>Överhoppningsfrekvens för aktivering överskriden</li><li>Felfrekvens för källinmatning har överskridits</ul> |
| Utökade aviseringar | Informationsaviseringar om granskningshändelser är nu tillgängliga för prenumeration för följande [aviseringsregler](../../observability/alerts/rules.md):<br><ul><li>Skapa målgrupp</li><li>Målgruppsuppdatering</li><li>Målgruppsborttagning</li><li>Skapa datauppsättning</li><li>Uppdatering av datauppsättning</li><li>Ta bort datauppsättning</li><li>Skapa schema</li><li>Schemauppdatering</li><li>Ta bort schema. |

{style="table-layout:auto"}

Mer information om aviseringar finns i avsnittet [[!DNL Observability Insights] översikt](../../observability/home.md).

## Kontrollpaneler {#dashboards}

Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Register för licensanvändningstillägg | Få detaljerad insyn i licensanvändningen och hantera dina plattformsresurser med dedikerade tabeller för kärnprodukter och tillägg. Spåra och analysera nyckeltal för varje kärnprodukt med genomgångsvyer på sandlådenivå. Tilläggsstatistik integreras sömlöst med kärnproduktens mätningar och ger en heltäckande bild av användningen. Förbättrad synlighet hjälper dig att optimera licenshanteringen och anpassa resurserna till organisationens behov. Se [[!UICONTROL License Usage] guiden för kontrollpanelen](../../dashboards/guides/license-usage.md#overview-tab) för mer information. |
| Query Pro-läge - globala filteruppgraderingar | Förbättra analysen med det nya datumfiltret i Query Pro-läget. Förfina insikterna med dynamiska datumparametrar i dina SQL-frågor och filtrera data efter specifika tidsramar. Välj förinställda eller anpassade datumintervall med ett intuitivt användargränssnitt, så att kontrollpanelerna blir relevanta för alla användare. Förenkla arbetsflödena, bibehåll precisionen och fatta vältajmade beslut. Läs [guiden om hur du skapar datumfilter](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md) för mer information. |
| Query Pro-lägen - detaljnivå | Få djupare insikter med Query Pro Mode&#39;s detaljnivåfunktion och navigera sömlöst från diagram på hög nivå till detaljerade kontrollpaneler. Använd den här funktionen för att enkelt gå från sammanfattningar till djupgående analyser och utforska trender, kundbeteenden och nyckeltal. Automatiska genomströmningar av filter och detaljnivå på flera nivåer håller data konsekventa, vilket ger en smidig utforskning. Förenkla arbetsflöden, håll rätt sammanhang och snabba upp beslutsfattandet. Läs [steg-för-steg-guiden om hur du skapar fördjupningar](../../dashboards/data-distiller/query-pro-mode/drill-through.md) för mer information. |
| Query Pro-läge - avancerade tabellattribut | Använd Query Pro Mode för avancerade tabellattribut för att effektivisera datavisualisering, förbättra arbetsflödets effektivitet och förbättra tydlighet i data. Lägg till automatisk sortering, storleksändring och sidnumrering i tabellerna direkt från anpassade kontrollpaneler. Sortera kolumner för att prioritera nyckeldata, ändra storlek för optimal läsbarhet och navigera smidigt i stora datauppsättningar utan att ändra SQL-frågorna. Läs guiden ”[Visa mer](../../dashboards/data-distiller/query-pro-mode/view-more.md)” för att lära dig hur du integrerar dessa funktioner och förbättrar dina datainsikter. |
| Total datavolym | Måttet ”Genomsnittlig profilnoggrannhet” har ersatts med måttet ”Total datavolym”. Total datavolym avser den totala mängden tillgängliga data som kan användas med kundprofil i realtid för arbetsflöden för engagemang och personalisering. Mer information om den här ändringen finns i guiden [Total datavolym](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Läs [översikt över kontrollpaneler](../../dashboards/home.md) för mer information om kontrollpaneler, bland annat hur du beviljar åtkomstbehörigheter och skapar anpassade widgetar.

## Dataförberedelse {#data-prep}

Använd dataförberedelse för att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} Nya funktioner för dataförberedelser som kan användas i Destinationer | Nu kan du använda följande matrisfunktioner för Destinationer:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Mer information finns i [funktionsguiden för dataförberedelse](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Mer information om dataförberedelse finns i [översikten över dataförberedelse](../../data-prep/home.md).

## Mål {#destinations}

**Uppdaterad: 30 september 2024**

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | Septemberversionen 2024 lägger till mappningsalternativet för att exportera `countryCode` parametern till Amazon Ads. Använd `countryCode` i [mappningssteget](/help/destinations/catalog/advertising/amazon-ads.md#map) om du vill förbättra identitetsmatchningsfrekvensen med Amazon. |
| [[!BADGE B2B]{type=Informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | Använd den här destinationen för att aktivera dina kontomålgrupper för användningsfall inom Account-Based Marketing (ABM). Annonsera till relevanta personas och roller i dina målgruppskonton via DemandBases B2B Demand Side Platform (DSP). Målgruppskonton kan också berikas med tredjepartsdata från Demandbase, för andra användningsfall i senare led av marknadsförings- och säljprocessen. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar i [ datauppsättningsexport](/help/destinations/ui/export-datasets.md) | Septemberversionen 2024 av Experience Platform innehåller flera förbättringar av funktionerna för export av datauppsättningar för att bättre stödja olika användningsfall för utmatning av data. Bland de här funktionsförbättringarna finns: <ul><li>Nya konfigureringsalternativ för datamappar, inklusive alternativet att lägga till och ta bort undermappar.</li><li>Nya exportalternativ inklusive fullständig filexport (en gång) och möjligheten att ange slutdatum</li><li>Obs! Adobe inför också ett standardslutdatum som är 1 maj 2025 för alla exportdataflöden av datauppsättningar som skapats före septemberversionen. För dessa dataflöden måste kunderna uppdatera slutdatumet i dataflödet manuellt före slutdatumet, annars avbryts exporten på det här datumet.</li></ul> <br> ![Bild av användargränssnittet för Experience Platform som visar alternativen Redigera schema och mappar i schemaläggningssteget.](../2024/assets/september/edit-schedule-folders.png "Redigera schema- och mappalternativ i schemaläggningssteget."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Mer information finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättringar i schemaläggaren | Ta kontroll över dina schemarelationer med ett uppdaterat relationsarbetsflöde i schemaredigeraren. Uppdatera eller ta bort befintliga relationer direkt från gränssnittet i Experience Platform, vilket gör schemahanteringen smidigare och mer intuitiv. Justera referensscheman och byt namn på relationer med säkerhet, vilket säkerställer sömlös dataintegritet över segmentering och andra viktiga processer. Mer information om effektiv hantering av schemarelationer finns i guiderna om [definiera relationsfält i användargränssnittet](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) och om [B2B-relationer](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

För mer information om XDM, läs [Systemöversikt för XDM](../../xdm/home.md).

## Identitetstjänst {#identity-service}

Använd identitetstjänsten för Adobe Experience Platform för att skapa en heltäckande bild av dina kunder och deras beteenden genom att skapa en bro mellan identiteter på olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| --- | --- |
| Begränsad tillgänglighet för länkningsregler till identitetsdiagram | Regler för länkning av identitetsdiagram är en uppsättning verktyg i identitetstjänsten som du kan använda för att säkerställa korrekt personalisering för dina användare. <ul><li>Du kan nu använda [algoritmen för identitetsoptimering](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) för att se till att ett identitetsdiagram representerar en enskild person och förhindrar därför oönskad sammanslagning av identiteter i kundprofilen i realtid.</li><li>Konfigurera [prioriteter för namnrymd](../../identity-service/identity-graph-linking-rules/namespace-priority.md) för att definiera vikten av respektive namnrymd och påverka hur profilerna formateras och segmenteras.</li><li>Använd [verktyget för diagramsimulering i användargränssnittet](../../identity-service/identity-graph-linking-rules/graph-simulation.md) för att simulera identitetsdiagram med olika konfigurationer.</li><li>Använd [gränssnittet för identitetsinställningar](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) för att ange din unika namnrymd och ange prioriteter för alla namnutrymder i organisationen.</li><li>Gå till [identitetspanelen](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) om du vill ha statistik och trender om dina diagramdata.</li></ul> Om du vill testa länkningsregler för identitetsdiagram kontaktar du ditt Adobe-kontoteam för att få tillgång till utvecklingssandlådor. |

**Uppdaterad dokumentation**

| Funktion | Beskrivning |
| --- | --- |
| Felsökningsguide för länkningsregler för identitetsdiagram | Läs den nya [felsökningsguiden för länkningsregler för identitetsdiagram](../../identity-service/identity-graph-linking-rules/troubleshooting.md) för metoder och felsökningslösningar som du kan använda för att lösa vanliga problem som du kan stöta på när du arbetar med länkningsregler för identitetsdiagram. |
| Vanliga frågor om länkningsregler för identitetsdiagram | Läs de nya [vanliga frågeställningarna om länkningsregler för identitetsdiagram](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) för en lista med svar på vanliga frågor om namnrymdsprioritet, algoritmen för identitetsoptimering och andra aspekter av länkningsregler för identitetsgrafer. |

{style="table-layout:auto"}

Mer information om identitetstjänsten finns i [översikten över identitetstjänsten](../../identity-service/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL data lake]. Du kan koppla samman alla datauppsättningar från datasjön och fånga upp sökresultaten som en ny datauppsättning för användning i rapportering, arbetsyta för datavetenskap eller för inmatning i kundprofil i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Data Distiller-målgrupper | Skapa, hantera och aktivera enkelt målgrupper med SQL-målgruppstillägget i Experience Platforms Data Distiller. Definiera målgruppssegment med SQL-kommandon direkt från datasjön, utan att behöva använda rådata i profiler. Förfina målgruppsstrategier och synkronisera automatiskt målgrupper till filbaserade destinationer med detta flexibla, datadrivna tillvägagångssätt. Effektivisera arbetsflöden, optimera målgruppshantering och frigör datas fulla potential. Läs [guiden om hur du använder SQL:s målgruppstillägg](../../query-service/data-distiller-audiences/overview.md) för att förbättra dina målgruppsstrategier. |
| Data Distiller-statistik - Hyperkuber | Optimera big data-analyser med hyperkuber. Hantera komplexa beräkningar - som distinkta beräkningar och flerdimensionell analys - utan att behöva bearbeta historiska data på nytt. Uppdatera data stegvis, effektivisera arbetsflöden och minska bearbetningstiden samtidigt som du behåller noggrannhet och effektivitet. Få snabbare, skalbara och kostnadseffektiva insikter som förändrar beslutsfattandet. Utforska [guiden om hur du använder hyperkuber](../../query-service/hypercubes/overview.md) för att låsa upp avancerad analys. |
| Frågeredigerarens objektutforskare | Öka frågans effektivitet med den nya objektutforskaren i Frågeredigeraren. Sök, filtrera och kom snabbt åt datauppsättningar för att skriva och förfina frågor snabbare. Med schemauppdateringar i realtid och omedelbara tabellmetadata kan du effektivisera arbetsflöden, minska navigeringstiden och förbättra din frågeupplevelse. Frigör potentialen i era data och optimera analysen. Läs [guiden om hur du använder objektutforskaren](../../query-service/ui/user-guide.md#object-browser) om du vill ha mer information. |
| Beräkna timmar | Få kontroll över resursanvändningen med det nya synliga måttet Beräkningstider för schemalagda frågor. Visa beräkna timmar på frågekörningsnivå för att övervaka och optimera resursanvändningen för CTAS/ITAS-gruppfrågor. Spåra starttider, slutförandestatus och beräkningstid för varje frågekörning. Finjustera prestanda och minska kostnaderna utan problem. Läs [guiden om att beräkna timmar](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) om du vill ha mer information om hur du maximerar frågeeffektivitet. |

{style="table-layout:auto"}

Om du vill veta mer om frågetjänsten kan du läsa [Översikt över frågetjänst](../../query-service/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatering av kriterier för segmentering av strömning | Från och med september 2024-versionen har kriterierna för att dina målgrupper ska vara berättigade till segmentering av strömning uppdaterats. Mer information om de här ändringarna finns i [uppdatering av kriterier för strömningssegmentering](../../segmentation/eligibility-criteria-update.md). |
| Implementering av enhetlig sökning | Sökbeteendet i Segment Builder kommer nu att använda enhetlig sökning. Detta ger en mer robust upplevelse när du hanterar och söker efter målgrupper som kan återanvändas för segmentmedlemskap. Mer information om den här ändringen finns i [guiden för Segment Builder](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

För mer information om [!DNL Segmentation Service], läs [segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} Stöd för krypterad datainmatning i användargränssnittet | Du kan nu fylla på krypterade data från en gruppkälla för molnlagring med hjälp av arbetsytan Källor i användargränssnittet för Experience Platform. Läs handledningen om [inmatning av krypterade data i användargränssnittet](../../sources/tutorials/ui/encryped-ingestion.md) för mer information. |
| Allmän tillgänglighet för källan [!DNL Snowflake Streaming] | Källan [!DNL Snowflake Streaming] finns nu i GA. Använd den här källan för att strömma data från ditt [!DNL Snowflake]-konto till Experience Platform. Läs [[!DNL Snowflake Streaming] overview](../../sources/connectors/databases/snowflake-streaming.md)för mer information. |
| Stöd för autentisering av tjänstekonto i [!DNL Google BigQuery] | Du kan nu ansluta ditt [!DNL Google BigQuery]-konto till Experience Platform med hjälp av autentisering av tjänstekonto. Läs [[!DNL Google BigQuery] översikten](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) för mer information. <br> ![Bild av användargränssnittet för Experience Platform som visar alternativen Redigera schema och mappar i schemaläggningssteget.](../2024/assets/september/service_auth.png "Tjänstautentisering för Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Stöd för att hoppa över förhandsgranskning av exempeldata | Du kan nu välja att hoppa över förhandsgranskning av data när du skapar en källanslutning med följande källor: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Du kan hoppa över förhandsgranskning av data för att kringgå en timeout som kan uppstå när stora gruppdata importeras. Om du gör det kan det förhindra automatisk validering av beräknade och obligatoriska fält. Om du väljer att hoppa över förhandsgranskning av data kan du behöva validera beräknade och obligatoriska fält manuellt under mappningen. |
| Stöd för att inaktivera chunkning i [!DNL SFTP] | Du kan nu konfigurera en inställning som gör att du kan inaktivera chunkning i källan [!DNL SFTP]. Läs [[!DNL SFTP] översikten](../../sources/connectors/cloud-storage/sftp.md) för mer information. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).
