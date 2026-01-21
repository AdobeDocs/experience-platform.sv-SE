---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: d401707e263f09ccd8575f02a71d7e74899e02db
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 20%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: januari 2026**

Nya funktioner och uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Mål](#destinations)
- [Kundprofil i realtid](#real-time-customer-profile)
- [Scheman](#schemas)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Agent Orchestrator {#agent-orchestrator}

Med Agent Orchestrator kan ni bygga och driftsätta AI-baserade agenter som kan automatisera arbetsflöden och interagera med kunder över flera kanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Trial motion for Agent Orchestrator | Agent Orchestrator erbjuder nu en testversion som gör att kunderna kan utforska och testa tjänsten innan de genomför ett fullständigt köp. Med detta alternativ kan man prova-på-före-du-köpa utvärdera Agent Orchestrator-funktioner, inklusive kunskaper och orkestreringsfunktioner, i sin egen miljö. Testversionen ger en praktisk erfarenhet av att bygga AI-baserade agenter och förstå hur de kan integreras i befintliga arbetsflöden. |

{style="table-layout:auto"}

Mer information finns i [Agent Orchestrator-dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| Kevel-destinationskontakt är nu tillgänglig | [[!DNL Kevel]](https://www.kevel.com/) innehåller den AI-aktiverade tekniken och expertvägledningen som hjälper innovativa handelsledare att starta, skala och lyckas inom detaljhandelsmedia. Retail Media Cloud för [!DNL Kevel] har funktioner för riktade, hänförliga och anpassningsbara annonseringsformat för annonsering på plats och utanför webbplatsen. |
| Målkopplingen för Index Exchange är nu tillgänglig | [!DNL Index] är en global plattform för annonsleveranser som hjälper mediekonstruktörer att maximera värdet av sitt innehåll på alla skärmar. Med över 20 års branschledarskap knyter [!DNL Index] samman världens största varumärken med förstklassiga upplevelsemakare för att leverera högkvalitativa kundupplevelser. |
| Regionala slutpunkter stöder Braze-anslutningar | Alla [regionspecifika slutpunkter](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) som stöds av [!DNL Braze] är nu tillgängliga för val under målkonfigurationsflödet. Fråga din [!DNL Braze]-representant vilken slutpunktsinstans du ska använda. |
| Veckovis och månadsvis schemaläggningssupport för Liveramp Onboarding | Du kan nu konfigurera exportscheman varje vecka och månad för Liveramp Onboarding-målet. |
| Stöd för AES256-kryptering för Amazon S3-destinationer | Nu kan du konfigurera AES256-kryptering för dina Amazon S3-exporter. |
| Förbättrad aktiveringsupplevelse för The Trade Desk och Microsoft Bing-destinationer | Trade Desk och Microsoft Bing-destinationerna innehåller nu fördefinierade obligatoriska mappningar för en optimerad aktiveringsupplevelse. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Skyddsgränsen för Adobe Target-destinationen har uppdaterats | Det maximala antalet målgrupper som kan mappas till ett enda Adobe Target-mål har ökats från 50 till 250. På så sätt anpassas Adobe Target till standardmålgruppsgränsen för andra destinationer, vilket ger större flexibilitet i arbetsflödena för målgruppsaktivering. Nu kan du aktivera fler målgrupper för Adobe Target-destinationer utan att behöva skapa flera dataflöden. |
| [Redigera mål](/help/destinations/ui/edit-destination.md) och [redigera marknadsföringsåtgärder](/help/destinations/ui/edit-activation.md#edit-marketing-actions) allmän tillgänglighet | Alternativet att redigera mål och marknadsföringsåtgärder är nu tillgängligt för alla användare. |
| Växla visningsnamn för fält i mappningssteget | När du mappar schemafält till ett mål kan du nu växla mellan att visa det fullständiga XDM-fältnamnet och endast visa visningsnamnet. |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Kundprofil i realtid {#real-time-customer-profile}

Med kundprofilen i realtid kan ni få en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tvingande strömningskapacitet | Experience Platform tillämpar nu strömningskapacitet för kundprofil och identitetstjänst i realtid. När kunderna överträffar sin avtalade strömningskapacitet kommer data att ställas i kö och behandlas på ett första-i-första-ut-sätt. Detta garanterar förutsägbara systemprestanda och förhindrar att kapacitetsöverträdelser påverkar dataöverföringskvaliteten. Viktigt: Direktuppspelning kommer inte att vara tillgängligt i datasjön när kapaciteten överskrids, detta gäller inte för kunder med Adobe Journey Optimizer-licenser och data som köas kommer att behandlas sekventiellt när kapaciteten blir tillgänglig. |
| API-åtkomstborttagning för Real-Time CDP Prime | API-åtkomst för upplevelsehändelser är nu föråldrat för alla Real-Time CDP Prime-kunder. Den här ändringen påverkar möjligheten att fråga upplevelsehändelser direkt via API. Real-Time CDP Ultimate-kunder kan begära ett undantag genom en formell undantagsprocess för att aktivera API-åtkomst för upplevelsehändelser om det behövs för deras användningsfall. Den här borttagningen hjälper till att optimera systemprestanda och anpassas till bästa praxis för dataåtkomstmönster. |
| Kör bildskärmsdataflöde | Nu kan du övervaka dataflödets förlopp och beredskap i Profil. |

{style="table-layout:auto"}

Mer information finns i [[!DNL Real-Time Customer Profile] översikten](../profile/home.md).

## Scheman {#schemas}

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data. Scheman består av en basklass och noll eller flera schemafältgrupper.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Modernisering av schemalagret med sökning, filter, taggar och mappar | Sidan för att bläddra i scheman har moderniserats för att ge bättre funktioner för att ordna och identifiera scheman. De nya funktionerna är bland annat avancerade sök- och filtreringsalternativ, stöd för användargenererade taggar och mappar för att ordna scheman och textbundna åtgärder för att effektivisera arbetsflödena. Viktiga förbättringar är: uppdaterade kolumner (Namn, Klass, Datamängder, Identiteter, Relationer, Aktivera för profil, Beteende, Schematyp, Taggar, Skapad den, Senast ändrad), avancerade filter (Visa profiler, Schematyp, Klass, Har tagg, Skapad av, Ändringsdatum, Har primär identitet, Har relation, Primär identitetsnamnrymd), textbundna åtgärder (Redigera, Ta bort, Använd etiketter), Skapa datauppsättning för icke-relationella scheman, Hantera taggar, Flytta till mapp, Lägg till i paket, Kopiera JSON-struktur, Hämta exempelfil) och möjligheten att ordna scheman med hjälp av taggar och mappar. De här förbättringarna ger omfattande insyn i schemaresurser och möjliggör mer effektiv schemahantering på sandlådenivå. |

Mer information finns i [[!DNL Schemas] översikten](../xdm/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Övervakning av strömningssegmentering | Realtidsövervakning för direktuppspelningssegmentering ger transparens vad gäller utvärderingsfrekvens, fördröjning och datakvalitetsstatistik på sandbox-, dataset- och målgruppsnivå. Detta stöder förebyggande varningar och åtgärdbara insikter som hjälper datatekniker att identifiera kapacitetsöverträdelser och problem med inmatning. Övervakningsmätningar inkluderar utvärderingshastighet, fördröjning av P95-intag samt mottagna, utvärderade, misslyckade och hoppade över poster. Funktioner för visa-för-data och visa-för-målgrupp ger omfattande insyn i nya profiler som är kvalificerade och diskvalificerade. |
| TTL-uppdatering för extern målgrupp | Externa målgrupper (t.ex. CSV-överföringar) har nu stöd för en tvingad uppdateringsfunktion för TTL-inställningar (Time-to-Live). Med den här funktionen kan användare uppdatera TTL-förfallotiden manuellt för externa målgrupper, vilket ger större kontroll över hanteringen av målgruppens livscykler. Detta är särskilt användbart för målgrupper som måste stanna kvar efter den inledande TTL-perioden eller som behöver aktiveras på nytt utan att överföra data på nytt. |

Mer information finns i [[!DNL Segmentation Service] översikten](../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| [!DNL Oracle Eloqua] V2-källa | En ny [!DNL Oracle Eloqua]-källkoppling är nu tillgänglig och ersätter den inaktuella kopplingen. Den här uppdaterade anslutningen ger förbättrad funktionalitet och förbättrad tillförlitlighet vid inmatning av data från [!DNL Oracle Eloqua] till Experience Platform. Kunder som använder den befintliga anslutningen bör migrera till den nya implementeringen eftersom befintliga anslutningar inte längre fungerar. Den nya kopplingen stöder alla installations- och konfigurationssteg som behövs för att ansluta till [!DNL Oracle Eloqua] och data för automatiserad import. |
| [!DNL Salesforce Marketing Cloud] V2-källa | En ny [!DNL Salesforce Marketing Cloud]-källkoppling är nu tillgänglig och ersätter den inaktuella kopplingen. Den här uppdaterade anslutningen ger bättre prestanda och ytterligare funktioner för inmatning av data från [!DNL Salesforce Marketing Cloud] till Experience Platform. Kunder som använder den befintliga kopplingen bör gå över till den nya implementeringen. Den nya kopplingen innehåller omfattande konfigurationsinstruktioner för anslutning till [!DNL Salesforce Marketing Cloud] och inmatning av automatiserade marknadsföringsdata. |

Mer information finns i [översikten över källor](../sources/home.md).

