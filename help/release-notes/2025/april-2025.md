---
title: Versionsinformation om Adobe Experience Platform april 2025
description: Versionsinformationen för Adobe Experience Platform från april 2025.
exl-id: a3b1e2e8-d780-4e23-b323-37e1a631f716
source-git-commit: e0740ca9cd6e1d0b92d5504a2869ac03c28d4980
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 99%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 29 april 2025**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [Experience League](#experience-league)
- [Datainsamling](#data-collection)
- [Mål](#destinations)
- [Experience Data Model](#xdm)
- [Identitetstjänst](#identity)
- [Frågetjänst](#query-service)
- [Sandlådor](#sandboxes)
- [Källor](#sources)
- [Use Case Playbooks](#use-case-playbooks)

## Experience League {#experience-league}

Experience League är en omfattande utbildningsplattform som förbättrar dina färdigheter inom Adobe-produkter. Här finns en mängd olika resurser, bland annat kurser, dokumentation, communitysidor, evenemang och tillgång till certifieringar.

| Funktion | Beskrivning |
| --- | --- |
| Personlig startsida | Få åtkomst till och anpassa din personliga startsida på [Experience League](https://experienceleague.adobe.com/sv/home#). Logga in med dina Adobe-inloggningsuppgifter och välj sedan **[!UICONTROL Experience League]** i menyn längst upp om du vill optimera din utbildningsupplevelse: <ul><li>**Bokmärken**: använd funktionen [!UICONTROL Bookmarks] om du vill spara och samla dina favoritresurser på ett ställe. Du kan spara olika typer av innehåll, inklusive spellistor, artiklar och självstudiekurser.</li><li>**Anpassa din utbildning**: förbättra din utbildningsupplevelse genom att uppdatera din Experience League-profil med roller, branscher, produkter och erfarenhetsnivå som passar dina behov bäst.</li><li>**Rekommendationer**: visa utbildningsinnehåll som rekommenderas utifrån din senaste aktivitet.</li><li>**Nyligen visade**: använd avsnittet [!UICONTROL Recently viewed] för att snabbt gå tillbaka till nyligen visat innehåll, till exempel dokumentation och videor.</li><li>**Utbildningsresurser**: använd panelen [!UICONTROL All learning resources] för att komma till självstudiekurser, dokumentation, community, händelser och certifieringar.</li><li>**Nyheter**: I avsnittet [!UICONTROL What's new] finns en ström med det senaste innehållet på Experience League.</li><li>**Se tidigare händelser på begäran**: se tidigare inspelade livesändningar om produkter i fokus, användningsfall och självstudiekurser med avsnittet [!UICONTROL Watch past events on-demand].</li></ul><br> ![Personlig startsida på Experience League.](../2025/assets/april/personalized-home-page.png "Personlig startsida på Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Adform]-tillägg | Tillägget [!DNL Adform] på serversidan gör det möjligt för varumärken att enkelt rikta om målgrupper utanför webbplatsen med hjälp av ECID:er. Det här tillägget på serversidan är inte beroende av cookies från tredje part eller alternativa ID:n för cookies. Eftersom detta görs helt på serversidan behövs dessutom inga ytterligare pixlar eller andra ändringar på klientsidan. Mer information finns i [tilläggsöversikten för Adform](/help/tags/extensions/server/adform/overview.md). |
| [!DNL Amazon] API-tillägg för webbhändelser | API-tillägget [!DNL Amazon]-konverteringar gör att annonsörer kan dela webbplatsinteraktioner direkt med [!DNL Amazon], vilket ger förbättrad tillskrivning, tillförlitlighet för data och kampanjoptimering. Det här tillägget har stöd för vidarebefordran av händelser, vilket gör att du kan skicka konverteringshändelser som inköp, varukorgstillägg med mera, samtidigt som du säkerställer korrekt deduplicering för korrekt rapportering. Mer information finns i [tilläggsöversikten för Amazon](/help/tags/extensions/server/amazon/overview.md). |

{style="table-layout:auto"}

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [Marketo Engage Person Sync](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe uppdaterade målet [!DNL Marketo Engage Person Sync] för att åtgärda ett problem som påverkade kunder när det fanns flera e-postmeddelanden i identitetsmappningen. |
| [(V2) Målgruppsanslutning för Pega CDH Realtime ](/help/destinations/catalog/personalization/pega-v2.md) | Använd målet [!DNL (V2) Pega Customer Decision Hub Realtime Audience] i Adobe Experience Platform för att skicka profilattribut och data om målgruppsmedlemskap till Pega Customer Decision Hub för bästa beslutsfattande åtgärd när du har flera Pega Customer Decision Hub-program konfigurerade i Pega-kontot. |

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| **Veckovisa** och **månadsvisa** schemaläggningsalternativ för fullständiga filexporter | Nu kan du schemalägga fullständiga filexporter för personer och potentiella målgrupper varje vecka eller månad när du aktiverar till filbaserade mål för molnlagring. [Läs mer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) om schemaläggningsalternativ. |

{style="table-layout:auto"}

**Korrigeringar, förbättringar och andra meddelanden** {#destinations-fixes-and-enhancements}

- **Slutdatum för verkställande av datauppsättningsexport har senarelagts till 1 september 2025**\
  Som en del av [versionen från september 2024](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality) har Adobe fastställt slutdatumet 1 maj 2025 för dataflöden avseende datauppsättningsexport som skapats *innan den versionen lanserades*. Adobe förlänger nu den här tidsfristen till **1 september 2025** för att ge kunderna ytterligare tid att uppdatera sina scheman. Mer information om hur du ändrar slutdatumet för ett dataflöde i en datauppsättningsexport finns i avsnittet om schemaläggning i [självstudiekursen för export av datauppsättningar](../../destinations/ui/export-datasets.md#schedule-dataset-export).

- **Förbättrad hantering av misslyckade SFTP-överföringar för LiveRamp-registrering**\
  Adobe har implementerat en korrigering för ett problem som påverkar filexporten tillmålet [LiveRamp-registering](/help/destinations/catalog/advertising/liveramp-onboarding.md) via SFTP. Ibland misslyckades filöverföringar på grund av tillfälliga serverproblem och tillfälliga filer från de här försöken finns kvar på servern. Filerna kan inte tas bort och hindrar efterföljande försök eftersom Adobe inte har behörighet att skriva över dem.\
  Efter korrigeringen genererar Adobe en ny fil med ett suffix `attempt2` om ett efterföljande försök inte kan ta bort den temporära filen, så att efterföljande försök kan slutföras.

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Uppdaterade XDM-komponenter**

| Funktion | Beskrivning |
| --- | --- |
| Strängfält får ett lägsta värde på ett | Nya strängfält får som standard en kortaste längd på ett. Null-värden för fält som inte är obligatoriska accepteras fortfarande. Mer information om bästa praxis finns i guiden [Bästa praxis för datamodellering](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [Systemöversikten över XDM](../../xdm/home.md).

## Identitetstjänst {#identity}

Använd identitetstjänsten för Adobe Experience Platform för att skapa en heltäckande bild av dina kunder och deras beteenden genom att skapa en bro mellan identiteter på olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Begränsad tillgänglighet]{type=Informative} [!DNL Identity Graph Linking Rules] | Länkningsregler för identitetsdiagram kan nu användas av alla kunder i utvecklingssandlådor. <ul><li>**Aktiveringskrav**: funktionen förblir inaktiv tills du konfigurerar och sparar [!DNL Identity Settings]. Utan konfigurationen fortsätter systemet att fungera som vanligt, utan att beteendet förändras.</li><li>**Viktigt**! Under den här fasen med begränsad tillgänglighet kan Edge-segmentering ge oväntade resultat för segmentmedlemskap. Streaming och gruppsegmentering fungerar dock som förväntat.</li><li>**Nästa steg**: kontakta Adobe-kontoteamet för mer information om hur du aktiverar funktionen i produktionssandlådor.</li></ul> |

{style="table-layout:auto"}

Mer information finns i [[!DNL Identity Graph Linking Rules] dokumentationen](../../identity-service/identity-graph-linking-rules/overview.md).

## Frågetjänst {#query-service}

Fråga efter data i Adobe Experience Platforms datasjö med hjälp av standard-SQL med Frågetjänst. Kombinera datauppsättningar sömlöst och generera nya från dina frågeresultat för att driva rapportering, aktivera datavetenskapliga arbetsflöden eller underlätta inmatning i kundprofil i realtid. Du kan till exempel sammanfoga kundtransaktionsdata med beteendedata för att identifiera värdefulla målgrupper för riktade marknadsföringskampanjer.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Skriv över SQL-målgrupp | Uppdatera målgruppsmedlemskapet genom att skriva över befintliga profiler med resultatet för en ny SQL-fråga. På så sätt kan du hantera dynamiska målgrupper effektivare genom att ta bort och uppdatera gamla poster i en enda åtgärd. Mer information finns i guiden för [SQL:s målgruppstillägg](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Hämta och kopiera resultat för frågor | [Hämta frågeresultat direkt från frågeredigeraren](../../query-service/ui/overview.md#download-query-results) i CSV-, XLSX- eller JSON-filer, eller [kopiera resultat till urklipp](../../query-service/ui/overview.md#copy-results) som kommaavgränsade värden (CSV) för snabb användning i kalkylbladsprogram som Excel. Förbättringarna effektiviserar arbetsflöden för offlineanalys, rapportering och datavalidering. |
| Visa frågeresultat i helskärm | [Förhandsgranska frågeresultaten i en dialogruta i helskärmsläge](../../query-service/ui/overview.md#view-results) om du vill göra det lättare att läsa dem, enkelt skanna stora datauppsättningar och välja rader för kopiering. I helskärmsläget finns ett rutnät som du kan ändra storlek på för att göra det lättare att granska breda tabeller och detaljerade utdata. |
| Utökat urval av kolumner i modellförutsägelse | Välj specifika kolumner och tillämpa alias med den utökade syntaxen `model_predict`. Hämta resultat från mellanliggande förutsägelser, t.ex. funktionsvektorer och sannolikhetsresultat. Det utökade urvalet kräver att en funktionsflagga aktiveras. Se [modellens livscykeldokumentation](../../query-service/advanced-statistics/models.md#select-specific-output-fields) för exempel på syntax och information om funktionsflaggor. |
| Spara modellförutsägelseutdata med SKAPA TABELL och INFOGA I | [Spara valda förutsägelseutdata i nya tabeller med SKAPA TABELL MED VALDA eller infoga i befintliga tabeller med INFOGA I VALDA](../../query-service/advanced-statistics/models.md#predict). Om utökat urval av kolumner har aktiverats kan mellanliggande resultat som funktionsvektorer och sannolikheter också bevaras tillsammans med slutliga förutsägelser. Du hittar exempel på användning i [SQL:s syntaxdokumentation](../../query-service/sql/syntax.md#create-table-as-select). |

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../../query-service/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Utökad support för plugin-program för verktyg i sandlådan | Anpassade åtgärder kan nu kopieras som ett beroende objekt när du skapar dubbletter av Journey-objekt i sandlådeverktyg. Du kan dessutom välja befintliga åtgärder att återanvända i målsandlådan. De kan också läggas till i ett paket var för sig. Du hittar fullständig information om vilka Adobe Journey Optimizer-objekt som stöds i guiden om [sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Nya källor**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | Källan [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) är nu tillgänglig. Använd den här källan om du vill överföra data som tillhör dina [!DNL Algolia]-användarprofiler till Experience Platform. Du kan sedan använda dessa data för att förbättra användarengagemang, konverteringsgrader och övergripande kundupplevelser genom att tillhandahålla sökfunktionslösningar av hög kvalitet för webbplatser, e-handelsplattformar och program. Du hittar mer information i guiden om hur du [matar in [!DNL Algolia User Profiles]  data på Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md). |
| [!BADGE Beta]{type=Informative} API-stöd för [!DNL Azure Databricks] | Källan [!DNL Azure Databricks] är nu tillgänglig i API. Använd [!DNL Flow Service]-API för att ansluta ditt [!DNL Databricks]-konto och överföra dina [!DNL Databricks]-data till Experience Platform. Du hittar mer information i dokumentationen på [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| XDM-fält för inmatning av data från mediestreaming i Experience Platform har uppdaterats. | Den nya XDM-fältgruppen `mediaReporting` är nu tillgänglig och kan användas för att mata in data från mediestreaming via Adobe Analytics-källan till Experience Platform. Det här fältet ersätter fältet `media.mediaTimed`.</br> <br>Under en övergångsperiod på tre månader kommer inmatning av data i `media.mediaTimed`-fält att fortsätta. I slutet av juli 2025 kommer dock `media.mediaTimed`-fälten att vara helt inaktuella och inte längre synliga i användargränssnittet för schemaläggning i Experience Platform. Data skickas istället endast med hjälp av `mediaReporting`-fälten.</br><br>Om du har implementerat Analytics-källan för att samla in data från mediestreaming till plattformen före 22 april 2025 måste du migrera dina befintliga konfigurationer för att skicka data med den nya fältgruppen. Migreringen måste vara klar i slutet av juli 2025. Kontakta Adobe-kontoteamet för migreringsstöd. |
| Nya autentiseringstyper för [!DNL MariaDB] och [!DNL PostgreSQL] | Du kan nu använda grundläggande autentisering för att autentisera dina [!DNL MariaDB]- och [!DNL PostgreSQL]-källor på Experience Platform. Mer information finns i följande dokumentation: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Filtreringsstöd på radnivå för [!DNL Amazon Redshift] | Du kan använda filtreringsfunktioner på radnivå för dina [!DNL Amazon Redshift]-data på Experience Platform. Du hittar mer information i guiden om [filtrering av data på radnivå för källor i API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).

## Use Case Playbooks {#use-case-playbooks}

Use Case Playbooks utformades från början som stöd för att komma igång med Real-Time Customer Data Platform (RTCDP) eller Adobe Journey Optimizer. Men de har fortsatt att utvecklas och kan nu användas för att snabbt komma igång med viktiga användningsfall inom marknadsföring med inspiration och färdiga resurser för test och produktion.

Use Case Books har utvecklats från ett identifieringsverktyg till ett samverkansbaserat ramverk. Det kan användas för att skapa, hantera och dela egna spelböcker i olika organisationer.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} Skapa och dela dina egna spelböcker | Med nya Playbook Authoring Framework kan du skapa, hantera och dela egna spelböcker med användningsfall. Du får stöd för att hämta viktiga metadata, redigera resekartor och associera relevanta tekniska resurser. Du kan dela spelböcker mellan olika organisationer för att standardisera marknadsföringsstrategier och skapa enhetlighet. |

{style="table-layout:auto"}

Läs dokumentet [Skapa och dela dina egna spelböcker](/help/use-case-playbooks/playbooks/author.md) om du vill lära dig att skapa och dela dina egna spelböcker.

Ta del av [översikten över Use Case Playbooks](/help/use-case-playbooks/playbooks/overview.md) som ger en översikt över spelböckernas funktionalitet, deras syfte och en heltäckande demonstration, inklusive hur man skapar instanser och importerar genererade tillgångar till andra sandlådemiljöer.