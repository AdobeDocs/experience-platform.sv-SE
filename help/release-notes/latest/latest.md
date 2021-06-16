---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform för 26 maj 2021.
doc-type: release notes
last-update: May 26, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 487d6dbef21459a7ce78cdc70215ad46e06ba892
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 1%

---


# Versionsinformation för Adobe Experience Platform

**Lanseringsdatum: 26 maj 2021**

Nya funktioner i Adobe Experience Platform:

- [Kontrollpaneler](#dashboards)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [Kundprofil i realtid](#profile)
- [Sandlådor](#sandboxes)
- [Källor](#sources)

## Kontrollpaneler {#dashboards}

Adobe Experience Platform har flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har tagits med vid dagliga ögonblicksbilder.

| Funktion | Beskrivning |
| --- | --- |
| Profilinsikter | Profilpanelen ger en daglig översikt över kundprofilstatistik i realtid för varje organisationssammanslagningsprincip i Experience Platform. Dessa profilinsikter är tillgängliga för alla användare med möjlighet att komma åt och visa profildata inom plattformen. |
| Målgruppsinsikter | Segmentkontrollpanelen ger målgruppsrelaterade insikter till alla användare som har tillgång till att visa segment inom plattformen. Kontrollpanelen ger en daglig översikt över målgruppsmått för målgrupper som skapats med segmentgränssnittet i Segment Builder eller importerats från Adobe Audience Manager. |
| Aktiveringsinsikter | Kontrollpanelen för destinationer är tillgänglig för alla användare med möjlighet att komma åt och visa destinationer. Kontrollpanelen ger en daglig översikt över aktiveringsmåtten för aktiveringar på alla destinationer. |
| Användarspecifika insikter | Kontrollpanelernas utseende och känsla kan anpassas av varje användare, inklusive möjligheten att ändra layouten på kontrollpanelen genom att lägga till, ta bort, ändra storlek på och ordna om widgetar. |
| Skapa och hantera widgetar | Alla standardwidgetar och anpassade widgetar är tillgängliga för marknadsförare i ett centralt arkiv för att skapa och dela insikter:<br/><ul><li>Standardfliken innehåller widgetar som tillhandahålls av Adobe som är tillgängliga i instrumentpanelskontexten. </li><li>Den anpassade fliken innehåller anpassade widgetar som har skapats av organisationen, inklusive ett alternativ för att dölja widgetar.</li><li>Arbetsflödet för att skapa widgetar i profiler och målgruppsinsikter möjliggör redigering, markering, förhandsgranskning och publicering av anpassade widgetar.</li></ul> |
| Anpassade insikter | Behörigheter gör det möjligt för datatekniker och marknadsföringsspecialister att anpassa profilattribut som är tillgängliga för att skapa widgetar. |

Mer information om kontrollpaneler, inklusive hur du beviljar åtkomstbehörigheter och skapar anpassade widgetar, får du genom att läsa översikten [kontrollpaneler](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

| Funktion | Beskrivning |
| ------- | ----------- |
| Varningar för milda fel | Felmeddelandena för datapanelen är nu mer lättanvända genom att tillhandahålla varningar i stället för fel tillsammans med delvis omformade rader. |
| Nya funktioner | Tillagda funktioner för att hämta nycklar, lägga till element i en befintlig array, lägga till element från flera arrayer i en befintlig array, använda objekt för att skapa arrayer och använda JSON-objektets namn som en stränglitteral. |

Mer information finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättrad övervakning (beta) | Förbättrade funktioner för övervakning av destinationer, inklusive information för både batch- och direktuppspelningsdestinationer |
| [Snabbare stegvis filexport (beta)](../../destinations/ui/activate-destinations.md#export-incremental-files) | Lagt till möjlighet att exportera inkrementella filer till destinationer var 3, 6, 8 eller 12:e timme. <br> <br>Den här funktionen är för närvarande i betaversion och är endast tillgänglig för ett visst antal kunder. Kunder som inte är beta kan exportera inkrementella filer en gång om dagen. |
| [Stöd för dedupliceringsnyckel (beta)](../../destinations/ui/activate-destinations.md#deduplication-keys) | Lagt till möjligheten att ange ID-namnutrymmen eller profilattribut som dedupliceringsnycklar. Avdupliceringsnycklar eliminerar möjligheten att ha flera poster med samma profil i en exportfil. <br> <br>Den här funktionen är för närvarande i betaversion och är endast tillgänglig för ett visst antal kunder. |

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) är en öppen källkodsspecifikation som är utformad för att förbättra kraften i digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

| Funktion | Beskrivning |
| --- | --- |
| Fältgrupper för schema | Termen&quot;mixin&quot; har uppdaterats till&quot;fältgrupp&quot;. Den här förändringen återspeglas i hela Adobe Experience Platform användargränssnitt. API:t för schemaregister har dessutom en ny [fältgruppsslutpunkt](../../xdm/api/field-groups.md), medan slutpunkten för mixins har tagits bort som en äldre slutpunkt. Mer information finns i [XDM-dokumentationen](../../xdm/home.md). |

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] gör att ni kan sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Överlappningsrapport för datauppsättning | Den överlappande rapporten för datauppsättningen ger synlighet i profilarkivets sammansättning genom att de datauppsättningar som bidrar mest till den adresserbara målgruppen exponeras. Förutom att ge insikter i profildata hjälper den här rapporten användarna att vidta åtgärder för att optimera användningen av licenser, som att sätta en gräns för vissa data. Om du vill veta mer kan du följa självstudiekursen om att [generera överlappningsrapporten](../../profile/tutorials/dataset-overlap-report.md). |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa praxis för att arbeta med [!DNL Profile]-data, får du om du börjar med att läsa översikten över kundprofilen i realtid](../../profile/home.md).[

## [!DNL Sandboxes] {#sandboxes}

Adobe Experience Platform är utvecklat för att berika applikationer för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav. För att tillgodose detta behov tillhandahåller Experience Platform sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

| Funktion | Beskrivning |
| ------- | ----------- |
| Flera produktionssandlådor | Nu kan du skapa och hantera flera produktionssandlådor i din IMS-organisation och dedikera specifika produktionssandlådor till olika affärsområden, varumärken, projekt eller regioner. Självstudiekurserna för att skapa en produktionssandlåda [i gränssnittet](../../sandboxes/ui/user-guide.md) eller [med API](../../sandboxes/api/overview.md) innehåller mer information. |

### Kända begränsningar

- Alla Experience Cloud-organisationer har en färdig standardproduktionssandlåda. Den här sandlådan fungerar som standardmål för varje begäran som skickas till plattformen från ett annat Adobe-program eller ett icke-Adobe-program som inte är (än) sandlådekompatibelt. Standardproduktionssandlådan kan inte återställas om identitetsdiagrammet som finns i den också används av Adobe Analytics för funktionen [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html), eller om identitetsdiagrammet som finns i den också används av Adobe Audience Manager för funktionen [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).
- Produktionssandlådor som används för dubbelriktad segmentdelning med Adobe Audience Manager eller Audience Core Service kan varken återställas eller tas bort.
- Alla användarskapade produktions- och utvecklingssandlådor kan tas bort, förutom standardproduktionssandlådan.

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| ------- | ----------- |
| Användargränssnittsstöd för komprimerad filinmatning | Du kan nu förhandsgranska och importera komprimerade JSON-filer eller avgränsade filer med hjälp av molnlagringskällor i användargränssnittet. Mer information finns i självstudiekursen om hur du konfigurerar ett dataflöde för en molnlagringskällanslutning i gränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md).[ |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Azure Synapse Analytics]](../../sources/connectors/databases/synapse-analytics.md)</li><li>[[!DNL Greenplum]](../../sources/connectors/databases/greenplum.md)</li><li>[[!DNL HubSpot]](../../sources/connectors/marketing-automation/hubspot.md)</li><li>[[!DNL ServiceNow]](../../sources/connectors/customer-success/servicenow.md)</li></ul> |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).
