---
title: Versionsinformation om Adobe Experience Platform – november 2020
description: Versionsinformationen för Adobe Experience Platform från november 2020.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 8%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 11 november 2020**

Nya funktioner i Adobe Experience Platform:

- [Adobe Experience Platform Data Lake-migrering](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Uppdateringar av befintliga funktioner:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [Tjänsten [!DNL Destinations]](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake-migrering {#migration}

Medan Adobe migrerar datasjön från Gen1 till Gen2 kan användare läsa från datasjön, men alla funktioner som skriver till datasjön påverkas. Adobe kommer att kontakta systemadministratörer för att diskutera effekten av migreringen i detalj och för att bekräfta migreringsdatum och -tider för specifika organisationer.

Mer information finns i [Datasjömigreringsguiden](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] använder [Adobe Admin Console](https://adminconsole.adobe.com)-produktprofiler för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd olika Experience Platform-funktioner, inklusive datamodellering, profilhantering och sandlådeadministration.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Behörigheter | På fliken [!DNL Admin Console] i en [!DNL Experience Platform] -produktprofil kan du anpassa vilka [!DNL Experience Platform]-funktioner som är tillgängliga för användarna som är kopplade till profilen. Tillgängliga behörighetskategorier är: **[!UICONTROL Data Modeling]**, **[!UICONTROL Data Management]**, **[!UICONTROL Profile Management]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Data Monitoring]**, **[!UICONTROL Sandbox Administration]**, **[!UICONTROL Destinations]**, **[!UICONTROL Data Ingestion]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Query Service]** och **[!UICONTROL Data Governance]**. |
| Åtkomst till sandlådor | Fliken **[!UICONTROL Permissions]** i en [!DNL Experience Platform]-produktprofil kan ge användare åtkomst till specifika sandlådor. Mer information finns i avsnittet om [sandlådor](#sandboxes) nedan. |

Mer information finns i [åtkomstkontrollsöversikten](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] är en programtjänst integrerad med [!DNL Experience Platform]. Det gör att du kan utnyttja [!DNL Experience Platform] för att leverera det bästa erbjudandet och upplevelsen till dina kunder via alla kontaktytor vid rätt tidpunkt.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Centraliserat erbjudande | Gränssnittet där du skapar och hanterar de olika elementen som utgör erbjudandena och definierar deras regler och begränsningar. |
| Beslutsmotor för erbjudande | Beslutsmotorn för erbjudandet utnyttjar [!DNL Experience Platform] data och [!DNL Real-Time Customer Profiles], tillsammans med erbjudandebiblioteket, för att välja rätt tid, kunder och kanaler som erbjudandena ska levereras till. |

Mer information finns i dokumentationen för [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=sv).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] har byggts för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller [!DNL Experience Platform] sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Produktionssandlåda | [!DNL Experience Platform] innehåller en enda produktionssandlåda som inte kan tas bort eller återställas. Det totala antalet tillgängliga sandlådor, produktion och icke-produktion, bestäms av den licensierade licensen. |
| Sandlådor utan produktion | Flera icke-produktionssandlådor kan skapas för en enskild [!DNL Experience Platform]-instans, vilket gör att du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. |
| Sandlådeväxlare | I användargränssnittet [!DNL Experience Platform] kan du växla mellan tillgängliga sandlådor via en nedrullningsbar meny med sandlådeväxlaren i skärmens övre vänstra hörn. Sandlådeväxlaren innehåller också en sökfunktion som gör att du kan filtrera igenom tillgängliga sandlådor. |
| `x-sandbox-name` huvud | Alla anrop till [!DNL Experience Platform] API:er måste nu inkludera den nya `x-sandbox-name`-rubriken, vars värde refererar till attributet `name` för sandlådan som åtgärden ska utföras i. |

Mer information finns i översikten över [sandlådor](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Interaktiva åtgärder | [!DNL Data Prep] Mapper har nu stöd för iterativa åtgärder i en hierarki. |
| Mappningsfunktion | [!DNL Data Prep] Mapper kan nu **inte** kopiera ett attribut från källan till mål-XDM. |

Mer information finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## Arbetsyta för datavetenskap {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era datatillgångar i alla Adobe lösningar. Ett sätt som datavetenskapen Workspace kan uppnå detta är genom att använda [!DNL JupyterLab]. [!DNL JupyterLab] är ett webbaserat användargränssnitt för [[!DNL Project Jupyter]](https://jupyter.org/) och är nära integrerat med Adobe Experience Platform. Den innehåller en interaktiv utvecklingsmiljö där datavetare kan arbeta med [!DNL Jupyter] bärbara datorer, kod och data.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Mallen [!DNL JupyterLab] Recipe Builder | Anteckningsbok för att hämta information om krav på användning och versioner har uppdaterats. [!DNL Python] ML-runtime-basbilden har uppdaterats så att endast [!DNL Python] 3.6.7 och en [!DNL Conda] -miljö används. |

Mer information finns i dokumentet om att [skapa ett recept med Jupyter-anteckningsböcker](../../data-science-workspace/jupyterlab/create-a-model.md).

## Tjänsten [!DNL Destinations] {#destinations}

I [Real-Time Customer Data Platform](../../rtcdp/overview.md) är mål färdiga integreringar med målplattformar som aktiverar data till dessa partner på ett smidigt sätt.

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| Braze | Braze är en heltäckande plattform för kundengagemang som driver relevanta och minnesvärda upplevelser mellan kunder och de varumärken de älskar. |
| Microsoft Bing | Microsoft Bing-målet hjälper er att genomföra återannonsering och målgruppsanpassade digitala kampanjer i Microsoft Display Advertising. |
| The Trade Desk | Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer för olika annonser, videoklipp och mobila inventeringskällor. |

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| UX-uppdateringar för målinformation | Real-Time CDP målarbetsflöde innehåller nu intern övervakning så att du kan se vilka gruppaktiveringar som har slutförts. Med den här funktionen kan användare lösa problem direkt i arbetsflödet för batchdestinationer via aviseringar och en kontrollpanel för övervakning för att spåra fel i bearbetningsprocessen. |
| Filkryptering | För filbaserade mål kan användare nu lägga till kryptering i de exporterade filerna. |
| Filplanering | För både e-postbaserade och molnbaserade lagringsplatser kan användare skapa en engångs export eller skapa dagliga ögonblicksbilder. |
| Obligatoriska fält | Användarna kan markera fält som obligatoriska och se till att endast fält som innehåller det obligatoriska fältet exporteras. |

Mer information finns i [Målöversikt](../../destinations/home.md).

## Intelligenta tjänster {#intelligent-services}

Intelligenta tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskap.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Consumer Experience Events (CEE) dataset | När du skapar en CEE-datauppsättning har du nu stöd för att lägga till identitetsfält i datauppsättningen med Schemaredigeraren. Attribution AI och Customer AI använder den primära identiteten för att kombinera händelser. |

Mer information finns i avsnittet om att [lägga till identitetsfält i en datamängd](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) i guiden för dataförberedelse för intelligenta tjänster.

### Attribution AI

Attribution AI, som en del av Intelligent Services är en flerkanalig algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner i förhållande till angivna resultat.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Länk till datakälla | Länken till den ursprungliga datakällan kan visas och navigeras till från den högra listen i en vald tjänstinstans. |
| Redigera instansnamn | Nu kan du ändra namnet på en befintlig Attribution AI-instans. |
| Kloninstans | Kopierar den valda tjänstinstansinställningen och tillåter ändringar. |
| Ändra parametrar för instanskonfiguration | Du kan nu ändra konfigurationen för en befintlig Attribution AI-instans om den inte har börjat betygsätta än. |
| Enkelt att poängsätta | Du kan nu aktivera ad hoc-modellbedömning i dina Attribution AI-instanser. |
| Genomför kolumner | Nu kan du konfigurera ytterligare kolumner som ska läggas till i filerna för utdataskalning för att lägga till ytterligare dimensioner till vyer för BI-verktyg. |
| Instansaktivering och inaktivering | Du kan nu aktivera och inaktivera den schemalagda modellutbildningen och poängsättningen för dina AI-instanser för attribuering. |
| Tillståndsspårning | Du kan hitta den totala mängden attribueringsinsikter som används av ditt konto i Skapa instansbehållare. |
| Uppdelning efter position | En ny insiktsgraf som ger en analys av kontaktytor genom konvertering av banpositioner. |
| De vanligaste konverteringsbanorna | Ett nytt insiderdiagram finns på fliken Sökvägsanalys. Diagrammet innehåller en lista över de fem populäraste konverteringssökvägarna som visar sekvensen av kontaktytor i marknadsföringskanalen som ledde till de flesta konverteringar. |
| Pekpunktseffektivitet | Innehåller djupgående insikter om de tre viktigaste variablerna som din modell mäter kontaktytans effektivitet med. Variablerna är förhållandet mellan positiva och negativa banor, kontaktpunktseffektivitet och kontaktytpunktsvolym. |

Mer information finns i [AI-översikten för attribuering](../../intelligent-services/attribution-ai/overview.md).

### Kund-AI

Kundens AI, som en del av de intelligenta tjänsterna, ger marknadsförarna möjlighet att generera kundprognoser på individnivå med förklaringar. Med hjälp av inflytelserika faktorer kan kundens AI tala om för er vad en kund kan tänkas göra och varför. Dessutom kan marknadsförarna dra nytta av kundernas AI-prognoser och insikter för att personalisera kundupplevelser genom att leverera de lämpligaste erbjudandena och budskapen.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Länk till datakälla | Länken till den ursprungliga datakällan kan visas och navigeras till från den högra listen i en vald tjänstinstans. |
| Redigera instansnamn | Du kan ändra namnet på en befintlig Kundens AI-instans. |
| Ändra parametrar för instanskonfiguration | Du kan nu ändra konfigurationen för en befintlig kundens AI-instans om den inte har påbörjat en poängsättning än. |
| Kloninstans | Kopierar den valda tjänstinstansinställningen och tillåter ändringar. |
| Tillståndsspårning | Du kan hitta det totala antalet profiler som Kund-AI har klassificerat för ditt konto i Skapa instansbehållare. |
| Förutsägelsemål | Flexibiliteten när det gäller att skapa ett förutsägelsemål har ökat med nya alternativ för att förutsäga om något kommer att hända eller inte. Dessutom finns alternativ för att förutsäga om alla händelser inträffar eller om någon av händelserna inträffar när flera händelser har lagts till. |
| Influensafaktor-drilldown | De viktigaste inflytelserika faktorbuckarna innehåller nu borrningar. Nedbrytning är en djupare nivåsammanfattning av värden för var och en av de viktigaste inflytelserika faktorerna inom en benägenhetspyts. |

Mer information finns i [Översikt över AI för kunder](../../intelligent-services/customer-ai/overview.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med [!DNL Profile] kan du konsolidera dina olika kunddata till en enhetlig vy som ger ett åtgärdbart, tidsstämplat konto för varje kundinteraktion.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdaterat arbetsflöde för sammanslagningsprinciper | Experience Platform har uppgraderat konfigurationen av sammanfogningsprincipen till ett nytt stegvis arbetsflöde. Med det här arbetsflödet kan användarna sammanföra datafragment från flera profildatauppsättningar och ange prioritet för hur data sammanfogas över dessa datauppsättningar för att skapa en heltäckande bild av varje individ. Användare kan sammanfoga markerade XDM-datauppsättningar för enskilda profiler genom att välja lämplig sammanfogningsmetod (prioritetsordning för tidsstämpling eller datauppsättning) och lägga till ExperienceEvent-datauppsättningar i profildatauppsättningarna. |
| Unionsschemavy | I användargränssnittet i Experience Platform kan användare enklare hitta information om alla scheman och datauppsättningar som bidrar till unionsschemat samt attribut för ytnycklar som identitets- och relationsfält. Dessa uppdateringar förbättrar möjligheten att felsöka och verifiera att profiler är korrekt konfigurerade, identiteterna är korrekt sammanfogade och data har importerats. |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa praxis för att arbeta med [!DNL Profile]-data, finns i [Kundprofilöversikt i realtid](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor samtidigt som du kan strukturera, etikettera och förbättra data med hjälp av [!DNL Experience Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya källor**

| Funktion | Beskrivning |
| ------- | ----------- |
| [!DNL Shopify] | Du kan nu ansluta [!DNL Shopify] till [!DNL Experience Platform] med API:t [!DNL Flow Service] eller gränssnittet. Mer information finns i översikten för [Förminska koppling](../../sources/connectors/ecommerce/shopify.md). |

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera anslutningsinformation | Du kan nu uppdatera namn, beskrivningar och autentiseringsuppgifter för befintliga batchanslutningar med API:t [!DNL Flow Service] och gränssnittet. Mer information finns i självstudiekursen om att [uppdatera anslutningar med API:t för Flow Service ](../../sources/tutorials/api/update.md) och [redigera kontoinformation med gränssnittet](../../sources/tutorials/ui/monitor.md). |
| Ta bort anslutningar | Batchanslutningar som innehåller fel eller har blivit onödiga kan nu tas bort med API:t [!DNL Flow Service] och användargränssnittet. Mer information finns i självstudiekursen om att [ta bort anslutningar med API:t för flödestjänst](../../sources/tutorials/api/delete.md) och [ta bort konton med gränssnittet](../../sources/tutorials/ui/delete-accounts.md). |
| Hierarkisk mappning | Du kan förhandsgranska en hierarkisk källfil, till exempel JSON eller Parquet, under dataöverföringsprocessen. Mer information finns i självstudiekursen [Konfigurera ett dataflöde för molnlagringsanslutningar i användargränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |
| API-stöd för mappning i strömningskällor | Nu kan du använda API:er för att utföra mappningsfunktioner med strömningskällor. |
| API-stöd för anpassade avgränsare för molnlagringskällor | Nu kan du samla in filer som inte är CSV-avgränsade med molnlagringskällor. Du kan använda valfri kolumnavgränsare, t.ex. tabb, komma, pipe, semikolon eller hash, för att samla platta filer i alla format. |
| Stöd för sandlåda i Adobe Audience Manager Connector | Audience Manager-anslutningen är nu sandlådebaserad. Användare kan aktivera anslutningen för att dirigera Audience Manager-datauppsättningar till valfri sandlåda (inklusive icke-produktionssandlådor). Konfigurationen är begränsad till en sandlåda per organisation. |
| Förbättringar av UX | Filbaserad inmatning är nu tillgängligt via källkatalogen. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
