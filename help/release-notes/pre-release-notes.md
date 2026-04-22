---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 8f898e618fbc2b414a3c899511ac410465f280d8
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 17%

---

# Information om förhandsversionen av Adobe Experience Platform

>[!IMPORTANT]
>
>Det här dokumentet är avsett som en **förhandsgranskning** av versionsinformationen för den aktuella månaden. Utgivningsobjekt kan ändras och kan läggas till eller tas bort i den slutliga versionen.

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Lanseringsdatum: April 2026**

Nya funktioner och uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Frågetjänst](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Microsoft Ads - kundmatchning](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Matcha kunder efter e-postadress och återengagera dem i [!DNL Microsoft Advertising Network], inklusive sök- och målgruppsannonser. Länka ditt [!DNL Microsoft Advertising]-konto till Real-Time CDP för att automatisera skapandet och hanteringen av kundmatchningslistor direkt från Experience Platform. Kontakta din kontoansvarige på Adobe för att få åtkomst. |
| [!BADGE Beta]{type=Informative} [Redigera anpassad publik](../destinations/catalog/advertising/reddit-custom-audience.md) | Skicka målgrupper från Experience Platform till [!DNL Reddit Ads]. Anslut ditt [!DNL Reddit]-konto, mappa identiteter och aktivera målgrupper för att nå personer som aktivt utforskar sina intressen på [!DNL Reddit]. |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2] är det aktuella målet för alla nya [!DNL Amazon Ads]-anslutningar. Om du har en befintlig [(äldre) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md)-anslutning fortsätter den att fungera utan nödvändiga ändringar. [!DNL Amazon Ads v2] ansluter till [!DNL Ads Data Manager], som har stöd för utökade identitetstyper, adressrelaterade fält och datadelning mellan [!DNL Amazon Ads]-produkter, vilket förbättrar målgruppsanpassningen och målgruppsmatchningen jämfört med [(äldre) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Rokt] | Använd [!DNL Rokt] för att koppla Experience Platform-målgrupper till AI-driven realtidsbeslutsfattande, vilket förbättrar kampanjresultatet genom mer exakt målinriktning, undertryckning och personalisering. |
| Externt målgruppsstöd för [villkor](../destinations/catalog/advertising/criteo.md) | Aktivera målgrupper från början till segmenteringstjänsten till [!DNL Criteo], inklusive anpassade uppladdningsmålgrupper (importerade från CSV), lookalike-målgrupper, federerade målgrupper och målgrupper som skapats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer]. Mer information finns i avsnittet [målgrupper som stöds](../destinations/catalog/advertising/criteo.md#supported-audiences). |
| [Acxiom Audience Connection](../destinations/catalog/advertising/acxiom-audience-connection.md) | Målet [!DNL Acxiom Audience Connection] är nu allmänt tillgängligt. Använd den för att förbättra målgrupper med [!DNL Acxiom's Real ID]-teknik och aktivera dem för ytterligare plattformar, inklusive [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL LG Ads], [!DNL Spectrum] och [!DNL Viant]. |
| [Målgruppsanslutning för verkligt ID för Acxiom](../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Målet [!DNL Acxiom Real ID Audience Connection] är nu allmänt tillgängligt. Använd det för att aktivera målgrupper med [!DNL Acxiom's Real ID] som matchningsnyckel för samma uppsättning plattformar som stöds, inklusive [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL LG Ads], [!DNL Spectrum] och [!DNL Viant]. |

{style="table-layout:auto"}

**Korrigeringar och förbättringar**

| Korrigera | Beskrivning |
| --- | --- |
| Stöd för anpassad Personalization-övervakning | Kontrollpanelen för mål har nu stöd för [!DNL Custom Personalization] mål. Begränsningsnoten som uteslöt [!DNL Custom Personalization] från övervakning har tagits bort. |
| Profilantal i aktiveringsgranskning | Aktiveringssteget visar nu antalet profiler för målgrupper som redan är aktiverade. Profilantal visas även för direktuppspelningsmål, inte bara gruppmål. |
| [!DNL Pinterest] synlighet för tokenförfallodatum | Målet [!DNL Pinterest] får nu plats med den förfallotid för token som returneras direkt från [!DNL Pinterest], så att du kan se när en ny autentisering krävs. |
| Exportfilen har nu inaktiverats för ogiltiga scheman | Åtgärden **[!UICONTROL Export file now]** är nu inaktiverad när målgruppsschemat är ogiltigt eller inaktuellt. Ett verktygstips förklarar varför åtgärden inte är tillgänglig. |
| Korrigera kolumnsynlighet i aktiveringsarbetsflöde | Ett problem har korrigerats där ändringar av synliga kolumner i en tabell felaktigt påverkade andra tabeller i aktiveringsarbetsflödet. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Synlighet för användning av fältgruppschema | Visa vilka scheman som använder en fältgrupp från detaljsidan och utforska dem i en sorterbar dialogruta med schemadata. Detta hjälper er att snabbt bedöma beroenden och påverkan utan att navigera bort. |

{style="table-layout:auto"}

Mer information finns i [XDM-systemöversikt](../xdm/home.md).

## Frågetjänst {#query-service}

Använd frågetjänsten för att fråga efter data i Adobe Experience Platform [!DNL Data Lake] med standard-SQL. Anslut till datauppsättningar från [!DNL Data Lake] och samla in frågeresultat som en ny datauppsättning som kan användas för rapportering, Data Science Workspace eller förtäring i kundprofilen i realtid.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Data Distiller Accelerators | Kör och schemalägg Adobe-hanterade, parametriserade SQL-mallar i gränssnittet för frågetjänsten för att utföra vanliga analyser utan att skriva SQL. På så sätt kan ni standardisera analysarbetsflöden och återanvända betrodd frågelogik i hela organisationen. |

{style="table-layout:auto"}

Mer information finns i [Översikt över frågetjänsten](../query-service/home.md).

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP] tillhandahåller enhetliga, användbara kundprofiler genom att importera, bearbeta och aktivera data i flera kanaler i realtid. Med Real-Time CDP kan man koppla samman befintliga datakällor, bygga och aktivera multimediala målgrupper och säkerställa integritetskompatibilitet över destinationer, allt inifrån Experience Platform. Detta gör det möjligt för marknadsförare, analytiker och IT-team att leverera personaliserade och vältajmade upplevelser till sina kunder genom sömlösa, kanalövergripande marknadsföringskampanjer.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Real-Time CDP MCP (Beta) | Använd Real-Time CDP MCP för att plocka in Real-Time CDP i AI-agenter och MCP-kompatibla klienter så att du kan interagera med Real-Time CDP-verktyg direkt via din inbyggda LLM-upplevelse. Genom att ansluta en MCP-kompatibel klient (som Claude, ChatGPT, Claude Code, Codex, Cursor eller VS Code) till `https://rtcdp-mcp.adobe.io/mcp` kan du använda naturligt språk för att inspektera målgrupper, målkonfiguration och körningshistorik för aktivering, utan att behöva skriva Experience Platform REST API-anrop eller navigera i flera gränssnittsarbetsflöden. När du har slutfört en webbläsarbaserad inloggning från Adobe får du skrivskyddad åtkomst till verktyg som: <ul><li>Sök bland befintliga målgrupper</li><li>Förhandsgranska publikmedlemskap</li><li>Måltyper för lista</li><li>Lista konfigurerade konton</li><li>Lista konfigurerade mål</li><li>Lista Source-anslutningar</li><li>Visa målanslutningar</li><li>Inspektera aktiveringskörningar</li></ul>. Varje begäran kräver parametrarna `imsOrgId` och `sandboxName` för att säkerställa att åtgärderna omfattar din organisation och sandlåda. Observera att skrivåtgärder inte stöds i den här Beta-versionen. |

{style="table-layout:auto"}

Mer information finns i [Real-Time CDP-översikten](../rtcdp/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa applikationer samtidigt som man ser till att de uppfyller gällande krav.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Express Copy | Använd Express Copy för att kopiera objekt till en målsandlåda i en enda åtgärd från [gränssnittet för sandlådeverktyg](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Beroende objekt identifieras automatiskt och skapas i målsandlådan eller återanvänds när de redan finns. |

{style="table-layout:auto"}

Mer information finns i [översikten över sandlådor](../sandboxes/home.md).

## Segmenteringstjänst {#segmentation-service}

Använd segmenteringstjänsten för att skapa målgrupper utifrån era kunddata och hantera hela deras livscykel i Experience Platform.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Övervakning av strömningssegmentering | Övervaka direktuppspelningssegmentering med synlighet i realtid i utvärderingsfrekvens, fördröjning av förtäring och mätvärden för datakvalitet på sandbox-, dataset- och segmentnivå. Visa mätvärden, inklusive utvärderingshastighet, svarstid för P95-förtäring, mottagna poster, utvärderade poster, misslyckade poster och överhoppade poster. Se även de nya profiler som är kvalificerade och diskvalificerade per segment. Använd dessa insikter för att identifiera kapacitetsöverträdelser och problem med förtäring innan de påverkar era data. |

{style="table-layout:auto"}

Mer information finns i [Publiköversikt](../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| Automatisk dataflödesinaktivering | Dataflöden för källinläsning som misslyckas kontinuerligt i 30 dagar inaktiveras automatiskt, vilket gör att ohälsosamma dataflöden upptäcks och att upprepade misslyckade körningar minskar. |
| [!DNL Delta Sharing] | Du kan använda källan [!DNL Delta Sharing] för att hämta Delta-tabeller till Experience Platform via ett säkert, öppet datadelningsprotokoll. När du har konfigurerat en [!DNL Delta Sharing]-anslutning och valt de resurser och tabeller som du vill importera, hämtar Platform automatiskt dessa data till datauppsättningarna så att du kan använda dem för analys, segmentering och aktivering. |
| [!DNL Meta Ads] (Beta) | Du kan använda [!DNL Meta Ads]-källkopplingen (Beta) på arbetsytan Källor för att autentisera till [!DNL Meta], välja dina annonskonton och schemalägga inmatning av [!DNL Meta Ads] kampanj- och prestandadata i Experience Platform-datauppsättningar. |
| [!DNL Talon.One] | Nu kan du ansluta Experience Platform till [!DNL Talon.One] med de nya batchkällorna [!DNL Talon.One] och direktuppspelningskällorna. Använd de nya källorna för att importera data om lojalitetsprofiler samt transaktioner- och lojalitetshändelser till Experience Platform. |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../sources/home.md).
