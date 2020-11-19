---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 11 november 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: b5fa40deb480f264b02a8be56aff2c50e4149cb2
workflow-type: tm+mt
source-wordcount: '2103'
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

Mer information finns i [Data Lake Migration Guide](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] använder [Adobe Admin Console](https://adminconsole.adobe.com) produktprofiler för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd plattformsfunktioner, inklusive datamodellering, profilhantering och sandlådeadministration.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Behörigheter | På fliken [!DNL Admin Console]i en [!DNL Platform] produktprofil kan du anpassa vilka [!DNL Platform] funktioner som är tillgängliga för användarna som är kopplade till profilen. Tillgängliga behörighetskategorier är: **[!UICONTROL Data Modeling]**, **[!UICONTROL Data Management]**, **[!UICONTROL Profile Management]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Data Monitoring]**, **[!UICONTROL Sandbox Administration]**, **[!UICONTROL Destinations]**, **[!UICONTROL Data Ingestion]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Query Service]** och **[!UICONTROL Data Governance]**. |
| Åtkomst till sandlådor | Fliken **[!UICONTROL Permissions]** i en [!DNL Platform] produktprofil kan ge användare åtkomst till specifika sandlådor. Mer information finns i avsnittet om [sandlådor](#sandboxes) nedan. |

Mer information finns i översikten över [åtkomstkontrollen](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] är en programtjänst som är integrerad med [!DNL Experience Platform]. Ni kan utnyttja detta för [!DNL Platform] att leverera det bästa erbjudandet och upplevelsen till era kunder via alla kontaktytor vid rätt tidpunkt.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Centraliserat erbjudandebibliotek | Gränssnittet där du skapar och hanterar de olika elementen som utgör erbjudandena och definierar deras regler och begränsningar. |
| Beslutsmotor för erbjudande | Avtalsmotorn utnyttjar [!DNL Platform] data och [!DNL Real-time Customer Profiles], tillsammans med erbjudandebiblioteket, för att välja rätt tidpunkt, kunder och kanaler som erbjudandena ska levereras till. |

Mer information finns i [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) dokumentationen.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] är byggt för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller sandlådor [!DNL Experience Platform] som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Produktionssandlåda | [!DNL Experience Platform] innehåller en enda produktionssandlåda som inte kan tas bort eller återställas. Det totala antalet tillgängliga sandlådor, produktion och icke-produktion, bestäms av den licensierade licensen. |
| Sandlådor utan produktion | Du kan skapa flera icke-produktionssandlådor för en enda [!DNL Platform] instans, så att du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. |
| Sandlådeväxlare | I [!DNL Experience Platform] användargränssnittet gör sandlådeväxlaren i skärmens övre vänstra hörn att du kan växla mellan tillgängliga sandlådor via en nedrullningsbar meny. Sandlådeväxlaren innehåller också en sökfunktion som gör att du kan filtrera igenom tillgängliga sandlådor. |
| `x-sandbox-name` header | Alla anrop till [!DNL Experience Platform] API:er måste nu inkludera det nya `x-sandbox-name` `name` huvudet, vars värde refererar till attributet för den sandlåda som åtgärden ska utföras i. |

Mer information finns i Översikt över [sandlådor](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Interaktiva åtgärder | [!DNL Data Prep] Mapper har nu stöd för iterativa åtgärder i en hierarki. |
| Mappningsfunktion | [!DNL Data Prep] Mapper kan nu **inte** kopiera ett attribut från källan till mål-XDM. |

Mer information finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## Datavetenskapens arbetsyta {#dsw}

Data Science Workspace använder maskininlärning och artificiell intelligens för att skapa insikter utifrån era data. Data Science Workspace är integrerat i Adobe Experience Platform och hjälper er att göra prognoser med hjälp av ert innehåll och era dataresurser över alla Adobe-lösningar. Ett sätt som Data Science Workspace kan uppnå detta är genom användning av [!DNL JupyterLab]. [!DNL JupyterLab] är ett webbaserat användargränssnitt för [[!DNL Project Jupyter]](https://jupyter.org/) och är nära integrerat med Adobe Experience Platform. Den utgör en interaktiv utvecklingsmiljö där datavetare kan arbeta med [!DNL Jupyter] bärbara datorer, kod och data.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| [!DNL JupyterLab] Mallen Recipe Builder | Anteckningsbok för att hämta in krav på användning och versioner har uppdaterats. [!DNL Python] XML-basbilden för körningsmiljön har uppdaterats så att den endast använder [!DNL Python] 3.6.7 och en [!DNL Conda] miljö. |

Mer information finns i dokumentet om att [skapa ett recept med Jupyter-anteckningsböcker](../../data-science-workspace/jupyterlab/create-a-recipe.md).

## [!DNL Destinations] Tjänst {#destinations}

I kunddataplattformen [i](../../rtcdp/overview.md)realtid är mål färdiga integreringar med målplattformar som aktiverar data till dessa partners på ett smidigt sätt.

**Nya destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| Microsoft Bing | Microsoft Bing-målet hjälper er att genomföra återannonsering och målgruppsanpassade digitala kampanjer i Microsoft Display Advertising. |
| The Trade Desk | Trade Desk är en självbetjäningsplattform för annonsköpare som kan genomföra återannonsering och målgruppsanpassade digitala kampanjer för olika annonser, videoklipp och mobila inventeringskällor. |

<!-- | Braze | Braze is a comprehensive customer engagement platform that power relevant and memorable experiences between customers and the brands they love. |  -->

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| UX-uppdateringar för målinformation | Arbetsflödet för mål-CDP i realtid innefattar nu intern övervakning så att du kan se vilka gruppaktiveringar som lyckades. Med den här funktionen kan användare lösa problem direkt i arbetsflödet för batchdestinationer via aviseringar och en kontrollpanel för övervakning för att spåra fel i bearbetningsprocessen. |
| Obligatoriska fält | Användarna kan markera fält som obligatoriska och se till att endast fält som innehåller det obligatoriska fältet exporteras. |

<!-- | File scheduling | For both email based and cloud storage destinations, users can create a one-time export or create daily snapshots. |
| File encryption | For file based destinations, users can now add encryption to their exported files. | -->

Mer information finns i Översikt över [destinationer](../../rtcdp/destinations/destinations-overview.md).

## Intelligenta tjänster {#intelligent-services}

Intelligenta tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa prediktioner som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Consumer Experience Events (CEE) dataset | När du skapar en CEE-datauppsättning har du nu stöd för att lägga till identitetsfält i datauppsättningen med Schemaredigeraren. Attribution AI- och kunds-AI använder den primära identiteten för att kombinera händelser. |

Mer information finns i avsnittet om [att lägga till identitetsfält i en datauppsättning](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) i guiden för dataförberedelse för Intelligent Services.

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

Mer information finns i [Attribution AI - översikt](../../intelligent-services/attribution-ai/overview.md).

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
| Förutsägelsemål | Flexibiliteten när det gäller att skapa ett förutsägelsemål har ökat med nya alternativ för att förutsäga om något kommer att hända eller inte. Dessutom finns alternativ för att förutsäga om alla händelser inträffar eller om någon av händelserna inträffar när flera händelser används. |
| Influensafaktor-drilldown | De viktigaste inflytelserika faktorbuckarna innehåller nu borrningar. Nedbrytning är en djupare nivåsammanfattning av värden för var och en av de viktigaste inflytelserika faktorerna inom en benägenhetspyts. |

Mer information finns i [Kundens AI-översikt](../../intelligent-services/customer-ai/overview.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdaterat arbetsflöde för sammanslagningsprinciper | Plattformen har uppgraderat konfigurationen av sammanfogningsprincipen till ett nytt stegvis arbetsflöde. Med det här arbetsflödet kan användarna sammanföra datafragment från flera profildatauppsättningar och ange prioritet för hur data sammanfogas över dessa datauppsättningar för att skapa en heltäckande bild av varje individ. Användare kan sammanfoga markerade XDM-datauppsättningar för enskilda profiler genom att välja lämplig sammanfogningsmetod (prioritetsordning för tidsstämpling eller datauppsättning) och lägga till ExperienceEvent-datauppsättningar i profildatauppsättningarna. |
| Unionsschemavy | I användargränssnittet i Experience Platform är det enklare att hitta information om alla scheman och datauppsättningar som bidrar till unionsschemat samt attribut för ytnycklar som identitets- och relationsfält. Dessa uppdateringar förbättrar möjligheten att felsöka och verifiera att profiler är korrekt konfigurerade, identiteterna är korrekt sammanfogade och data har importerats. |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa metoder för att arbeta med [!DNL Profile] data, finns i [Kundprofilöversikt](../../profile/home.md)i realtid.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya källor**
| Funktion | Beskrivning |
| — | — |
| [!DNL Shopify] | Du kan nu ansluta [!DNL Shopify] till [!DNL Experience Platform] med [!DNL Flow Service] API:t eller gränssnittet. Mer information finns i översikten [för](../../sources/connectors/ecommerce/shopify.md) Förminska koppling. |

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera anslutningsinformation | Nu kan du uppdatera namn, beskrivningar och autentiseringsuppgifter för befintliga batchanslutningar med hjälp av API:t och gränssnittet [!DNL Flow Service] . Mer information finns i självstudiekursen om hur du [uppdaterar anslutningar med API:t](../../sources/tutorials/api/update.md) för Flow Service och [redigerar kontoinformation med hjälp av gränssnittet](../../sources/tutorials/ui/monitor.md). |
| Ta bort anslutningar | Batchanslutningar som innehåller fel eller har blivit onödiga kan nu tas bort med API:t och gränssnittet [!DNL Flow Service] . Mer information finns i självstudiekursen om hur du [tar bort anslutningar med API:t](../../sources/tutorials/api/delete.md) för Flow Service och [tar bort konton med gränssnittet](../../sources/tutorials/ui/delete-accounts.md). |
| Hierarkisk mappning | Du kan förhandsgranska en hierarkisk källfil, som JSON eller Parquet, under dataöverföringsprocessen. Mer information finns i självstudiekursen om hur du [konfigurerar ett dataflöde för molnlagringskontakter i användargränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) . |
| API-stöd för mappning i strömningskällor | Nu kan du använda API:er för att utföra mappningsfunktioner med direktuppspelningskällor. |
| API-stöd för anpassade avgränsare för molnlagringskällor | Nu kan du samla in filer som inte är CSV-avgränsade med molnlagringskällor. Du kan använda valfri kolumnavgränsare, t.ex. tabb, komma, pipe, semikolon eller hash, för att samla platta filer i alla format. |
| Stöd för sandlåda i Adobe Audience Manager Connector | Kopplingen Audience Manager är nu sandlådebaserad. Användare kan aktivera kopplingen för att dirigera datauppsättningar från Audience Manager till valfri sandlåda (inklusive icke-produktionssandlådor). Konfigurationen är begränsad till en sandlåda per IMS-organisation. |
| UX-förbättringar | Filbaserad inmatning är nu tillgängligt via källkatalogen. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).