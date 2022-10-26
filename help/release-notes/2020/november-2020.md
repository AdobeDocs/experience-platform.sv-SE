---
title: Versionsinformation om Adobe Experience Platform november 2020
description: Versionsinformation november 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2161'
ht-degree: 2%

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
- [[!DNL Destinations] Tjänst](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake-migrering {#migration}

Medan Adobe migrerar datasjön från Gen1 till Gen2 kan användare läsa från datasjön, men alla funktioner som skriver till datasjön påverkas. Adobe kommer att kontakta systemadministratörer för att diskutera effekten av migreringen i detalj och för att bekräfta migreringsdatum och -tider för specifika IMS-organisationer.

Mer information finns i [Migreringsguide för datasjöer](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] hävstångar [Adobe Admin Console](https://adminconsole.adobe.com) produktprofiler för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd plattformsfunktioner, inklusive datamodellering, profilhantering och sandlådeadministration.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Behörigheter | I [!DNL Admin Console], fliken i en [!DNL Platform] Med produktprofilen kan du anpassa vilken [!DNL Platform] funktioner är tillgängliga för de användare som är kopplade till den profilen. Tillgängliga behörighetskategorier är: **[!UICONTROL Data Modeling]**, **[!UICONTROL Data Management]**, **[!UICONTROL Profile Management]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Data Monitoring]**, **[!UICONTROL Sandbox Administration]**, **[!UICONTROL Destinations]**, **[!UICONTROL Data Ingestion]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Query Service]** och **[!UICONTROL Data Governance]**. |
| Åtkomst till sandlådor | The **[!UICONTROL Permissions]** en flik i en [!DNL Platform] produktprofilen kan ge användare åtkomst till specifika sandlådor. Se avsnittet om [sandlådor](#sandboxes) nedan om du vill ha mer information. |

Mer information finns i [åtkomstkontroll - översikt](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] är en programtjänst som är integrerad med [!DNL Experience Platform]. Det gör att ni kan utnyttja [!DNL Platform] för att leverera det bästa erbjudandet och upplevelsen till era kunder via alla kontaktytor vid rätt tidpunkt.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Centraliserat erbjudandebibliotek | Gränssnittet där du skapar och hanterar de olika elementen som utgör erbjudandena och definierar deras regler och begränsningar. |
| Beslutsmotor för erbjudande | Beslutsmotorn för erbjudandet utnyttjar [!DNL Platform] data och [!DNL Real-time Customer Profiles], tillsammans med erbjudandebiblioteket, för att välja rätt tidpunkt, kunder och kanaler som erbjudandena ska levereras till. |

Mer information finns i [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) dokumentation.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] är byggt för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov [!DNL Experience Platform] innehåller sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Produktionssandlåda | [!DNL Experience Platform] innehåller en enda produktionssandlåda som inte kan tas bort eller återställas. Det totala antalet tillgängliga sandlådor, produktion och icke-produktion, bestäms av den licensierade licensen. |
| Sandlådor utan produktion | Flera icke-produktionssandlådor kan skapas för en enda [!DNL Platform] kan du till exempel testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. |
| Sandlådeväxlare | I [!DNL Experience Platform] i användargränssnittet gör sandlådeväxlaren i skärmens övre vänstra hörn att du kan växla mellan tillgängliga sandlådor via en nedrullningsbar meny. Sandlådeväxlaren innehåller också en sökfunktion som gör att du kan filtrera igenom tillgängliga sandlådor. |
| `x-sandbox-name` header | Alla samtal till [!DNL Experience Platform] API:erna måste nu innehålla de nya `x-sandbox-name` header, vars värde refererar till `name` i sandlådan där åtgärden ska utföras. |

Mer information finns i [översikt över sandlådor](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Interaktiva åtgärder | [!DNL Data Prep] Mapper har nu stöd för iterativa åtgärder i en hierarki. |
| Mappningsfunktion | [!DNL Data Prep] Mapper har nu möjlighet att **not** kopiera ett attribut från källan till mål-XDM. |

Mer information finns i [[!DNL Data Prep] översikt](../../data-prep/home.md).

## Datavetenskapens arbetsyta {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar. Ett sätt som Data Science Workspace kan åstadkomma detta är genom att använda [!DNL JupyterLab]. [!DNL JupyterLab] är ett webbaserat användargränssnitt för [[!DNL Project Jupyter]](https://jupyter.org/) och är nära integrerat i Adobe Experience Platform. Den ger en interaktiv utvecklingsmiljö där datavetare kan arbeta med [!DNL Jupyter] bärbara datorer, kod och data.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| [!DNL JupyterLab] Mallen Recipe Builder | Anteckningsbok för att hämta in krav på användning och versioner har uppdaterats. [!DNL Python] XML-basbilden för körningsmiljön har uppdaterats för användning [!DNL Python] 3.6.7 och [!DNL Conda] enbart miljön. |

Mer information finns i dokumentet om [skapa ett recept med Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Tjänst {#destinations}

I [Real-time Customer Data Platform](../../rtcdp/overview.md)är destinationer färdiga integrationer med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

| Destination | Beskrivning |
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

Mer information finns i [Översikt över destinationer](../../destinations/home.md).

## Intelligenta tjänster {#intelligent-services}

Intelligenta tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Consumer Experience Events (CEE) dataset | När du skapar en CEE-datauppsättning har du nu stöd för att lägga till identitetsfält i datauppsättningen med Schemaredigeraren. Attribution AI- och kunds-AI använder den primära identiteten för att kombinera händelser. |

Mer information finns i avsnittet om [lägga till identitetsfält i en datauppsättning](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) i handboken Intelligent Services för dataförberedelse.

### Attribution AI

Attribution AI, som en del av Intelligent Services är en flerkanalig algoritmisk attribueringstjänst som beräknar påverkan och inkrementell påverkan av kundinteraktioner i förhållande till angivna resultat.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Länk till datakälla | Länken till den ursprungliga datakällan kan visas och navigeras till från den högra listen i en vald tjänstinstans. |
| Redigera instansnamn | Nu kan du ändra namnet på en befintlig Attribution AI-instans. |
| Kloninstans | Kopierar den valda tjänstinstansinställningen och tillåter ändringar. |
| Ändra parametrar för instanskonfiguration | Du kan nu ändra konfigurationen för en befintlig Attribution AI-instans om den inte har börjat betygsätta än. |
| Enkelt att poängsätta | Du kan nu aktivera ad hoc-modellbedömning i dina Attribution AI. |
| Genomför kolumner | Nu kan du konfigurera ytterligare kolumner som ska läggas till i filerna för utdataskalning för att lägga till ytterligare dimensioner till vyer för BI-verktyg. |
| Instansaktivering och inaktivering | Nu kan du aktivera och inaktivera den schemalagda modellutbildningen och poängsättningen för dina Attribution AI. |
| Tillståndsspårning | Du kan hitta den totala mängden attribueringsinsikter som används av ditt konto i Skapa instansbehållare. |
| Uppdelning efter position | En ny insiktsgraf som ger en analys av kontaktytor genom konvertering av banpositioner. |
| De vanligaste konverteringsbanorna | Ett nytt insiderdiagram finns på fliken Sökvägsanalys. Diagrammet innehåller en lista över de fem populäraste konverteringssökvägarna som visar sekvensen av kontaktytor i marknadsföringskanalen som ledde till de flesta konverteringar. |
| Pekpunktseffektivitet | Innehåller djupgående insikter om de tre viktigaste variablerna som din modell mäter kontaktytans effektivitet med. Variablerna är förhållandet mellan positiva och negativa banor, kontaktpunktseffektivitet och kontaktpunktsvolym. |

Mer information finns i [Översikt över Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Kund-AI

Kundens AI, som en del av de intelligenta tjänsterna, ger marknadsförarna möjlighet att generera kundprognoser på individnivå med förklaringar. Med hjälp av inflytelserika faktorer kan kundens AI tala om för er vad en kund kan tänkas göra och varför. Dessutom kan marknadsförarna dra nytta av kundernas AI-prognoser och insikter för att personalisera kundupplevelser genom att leverera de lämpligaste erbjudandena och budskapen.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Länk till datakälla | Länken till den ursprungliga datakällan kan visas och navigeras till från den högra listen i en vald tjänstinstans. |
| Redigera instansnamn | Du kan ändra namnet på en befintlig Kundens AI-instans. |
| Ändra parametrar för instanskonfiguration | Du kan nu ändra konfigurationen för en befintlig kundens AI-instans om den inte har påbörjat en poängsättning än. |
| Kloninstans | Kopierar den valda tjänstinstansinställningen och tillåter ändringar. |
| Tillståndsspårning | Du hittar det totala antalet profiler som Kund-AI har gjort för ditt konto i Skapa instansbehållare. |
| Förutsägelsemål | Flexibiliteten när det gäller att skapa ett förutsägelsemål har ökat med nya alternativ för att förutsäga om något kommer att hända eller inte. Dessutom finns alternativ för att förutsäga om alla händelser inträffar eller om någon av händelserna inträffar när flera händelser har lagts till. |
| Influensafaktor-drilldown | De viktigaste inflytelserika faktorbuckarna innehåller nu borrningar. Nedbrytning är en djupare nivåsammanfattning av värden för var och en av de viktigaste inflytelserika faktorerna inom en benägenhetspyts. |

Mer information finns i [Översikt över AI för kunder](../../intelligent-services/customer-ai/overview.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdaterat arbetsflöde för sammanslagningsprinciper | Plattformen har uppgraderat konfigurationen av sammanfogningsprincipen till ett nytt stegvis arbetsflöde. Med det här arbetsflödet kan användarna sammanföra datafragment från flera profildatauppsättningar och ange prioritet för hur data sammanfogas över dessa datauppsättningar för att skapa en heltäckande bild av varje individ. Användare kan sammanfoga markerade XDM-datauppsättningar för enskilda profiler genom att välja lämplig sammanfogningsmetod (prioritetsordning för tidsstämpling eller datauppsättning) och lägga till ExperienceEvent-datauppsättningar i profildatauppsättningarna. |
| Unionsschemavy | I användargränssnittet i Experience Platform är det enklare att hitta information om alla scheman och datauppsättningar som bidrar till unionsschemat samt attribut för ytnycklar som identitets- och relationsfält. Dessa uppdateringar förbättrar möjligheten att felsöka och verifiera att profiler är korrekt konfigurerade, identiteterna är korrekt sammanfogade och data har importerats. |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa metoder för att arbeta med [!DNL Profile] data, läs [Översikt över kundprofiler i realtid](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya källor**

| Funktion | Beskrivning |
| ------- | ----------- |
| [!DNL Shopify] | Nu kan du ansluta [!DNL Shopify] till [!DNL Experience Platform] med [!DNL Flow Service] API eller gränssnittet. Se [Översikt över kopplingen](../../sources/connectors/ecommerce/shopify.md) för mer information. |

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera anslutningsinformation | Nu kan du uppdatera namn, beskrivningar och autentiseringsuppgifter för befintliga batchanslutningar med [!DNL Flow Service] API och användargränssnittet. Mer information finns i självstudiekursen om [uppdatera anslutningar med API:t för Flow Service](../../sources/tutorials/api/update.md) och [redigera kontoinformation med användargränssnittet](../../sources/tutorials/ui/monitor.md). |
| Ta bort anslutningar | Batchanslutningar som innehåller fel eller har blivit onödiga kan nu tas bort med [!DNL Flow Service] API och användargränssnittet. Mer information finns i självstudiekursen om [ta bort anslutningar med API:t för Flow Service](../../sources/tutorials/api/delete.md) och [ta bort konton med användargränssnittet](../../sources/tutorials/ui/delete-accounts.md). |
| Hierarkisk mappning | Du kan förhandsgranska en hierarkisk källfil, som JSON eller Parquet, under dataöverföringsprocessen. Se självstudiekursen på [konfigurera ett dataflöde för molnlagringsanslutningar i användargränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) för mer information. |
| API-stöd för mappning i strömningskällor | Nu kan du använda API:er för att utföra mappningsfunktioner med direktuppspelningskällor. |
| API-stöd för anpassade avgränsare för molnlagringskällor | Nu kan du samla in filer som inte är CSV-avgränsade med molnlagringskällor. Du kan använda valfri kolumnavgränsare, t.ex. tabb, komma, pipe, semikolon eller hash, för att samla platta filer i alla format. |
| Stöd för sandlåda i Adobe Audience Manager Connector | Kopplingen Audience Manager är nu sandlådebaserad. Användare kan aktivera kopplingen för att dirigera datauppsättningar från Audience Manager till valfri sandlåda (inklusive icke-produktionssandlådor). Konfigurationen är begränsad till en sandlåda per IMS-organisation. |
| UX-förbättringar | Filbaserad inmatning är nu tillgängligt via källkatalogen. |

Mer information om källor finns i [källöversikt](../../sources/home.md).
