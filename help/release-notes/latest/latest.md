---
title: Versionsinformation om Adobe Experience Platform april 2025
description: Versionsinformationen för Adobe Experience Platform från april 2025.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 92b9d4a0529fabb8094e13f4dc6b4bb6d8649b16
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 28%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Läs följande dokumentation om du vill veta mer om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 29 april 2025**

Uppdateringar av befintliga funktioner och dokumentation i Adobe Experience Platform:

- [Experience League](#experience-league)
- [Datainsamling](#data-collection)
- [Mål](#destinations)
- [Experience Data Model](#xdm)
- [Identitetstjänst](#identity)
- [Frågetjänst](#query-service)
- [Kundprofil i realtid](#profile)
- [Sandlådor](#sandboxes)
- [Källor](#sources)
- [Use Case Playbooks](#use-case-playbooks)

## Experience League {#experience-league}

Experience League är en omfattande utbildningsplattform som hjälper dig att höja din kompetens med Adobe produkter. Här finns en mängd olika resurser, bland annat kurser, dokumentation, communitysidor, evenemang och tillgång till certifieringar.

| Funktion | Beskrivning |
| --- | --- |
| Personlig hemsida | Gå till och anpassa din personliga hemsida på [Experience League](https://experienceleague.adobe.com/en/home#). Logga in med dina Adobe-inloggningsuppgifter och välj sedan **[!UICONTROL Experience League]** på den översta menyn för att optimera din inlärningsupplevelse: <ul><li>**Bokmärken**: Använd funktionen [!UICONTROL Bookmarks] för att spara och samla in dina favoritresurser på ett ställe. Du kan spara olika typer av innehåll, inklusive spellistor, artiklar och självstudiekurser.</li><li>**Anpassa din inlärning**: Förbättra din inlärningsupplevelse genom att uppdatera din Experience League-profil med de roller, branscher, produkter och den upplevelsenivå som bäst passar dina behov.</li><li>**Rekommendationer**: Visa utbildningsinnehåll som rekommenderas baserat på din senaste aktivitet.</li><li>**Nyligen visade**: Använd avsnittet [!UICONTROL Recently viewed] för att snabbt gå tillbaka till nyligen visat innehåll, till exempel dokumentation och videoklipp.</li><li>**Utbildningsresurser**: Använd panelen [!UICONTROL All learning resources] för att navigera till självstudiekurser, dokumentation, forum, händelser och certifieringar.</li><li>**Nyheter**: I avsnittet [!UICONTROL What's new] finns en ström med det senaste innehållet på Experience League.</li><li>**Titta på tidigare event on-demand**: Se tidigare inspelade liveströmmar på produktspotlights, användningsfall och självstudiekurser med avsnittet [!UICONTROL Watch past events on-demand].</li></ul><br> ![Personaliserad hemsida på Experience League.](../2025/assets/april/personalized-home-page.png "Personlig hemsida på Experience League."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Adform]-tillägg | Tillägget [!DNL Adform] på serversidan gör det möjligt för varumärken att enkelt rikta om målgrupper utanför webbplatsen med hjälp av ECID. Det här tillägget på serversidan är inte beroende av cookies från tredje part eller alternativa ID:n för cookies. Eftersom detta görs helt på serversidan behövs dessutom inga ytterligare pixlar eller andra ändringar på klientsidan. Mer information finns i [Översikt över tillägget Anpassa](/help/tags/extensions/server/adform/overview.md). |
| API-tillägg för [!DNL Amazon]-webbhändelser | API-tillägget [!DNL Amazon] Conversions gör att annonsörer kan dela webbplatsinteraktioner direkt med [!DNL Amazon], vilket ger förbättrad attribuering, tillförlitlighet för data och kampanjoptimering. Det här tillägget har stöd för vidarebefordran av händelser, vilket gör att du kan skicka konverteringshändelser som inköp, varukorgstillägg med mera, samtidigt som du säkerställer korrekt borttagning av dubbletter för korrekt rapportering. Mer information finns i [Översikt över Amazon-tillägget](/help/tags/extensions/server/amazon/overview.md). |

{style="table-layout:auto"}

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer** {#new-updated-destinations}

| Mål | Beskrivning |
| --- | --- |
| [Marketo Engage personsynkronisering](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe uppdaterade målet [!DNL Marketo Engage Person Sync] för att åtgärda ett problem som påverkade kunder när det fanns flera e-postmeddelanden i identitetskartan. |
| [(V2) Målgruppsanslutning för Pega CDH Realtime ](/help/destinations/catalog/personalization/pega-v2.md) | Använd målet [!DNL (V2) Pega Customer Decision Hub Realtime Audience] i Adobe Experience Platform för att skicka profilattribut och data om målgruppsmedlemskap till Pega Customer Decision Hub för nästa bästa åtgärd-beslut, när du har flera Pega Customer Decision Hub-program konfigurerade i Pega-kontot. |

**Ny eller uppdaterad funktionalitet** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| --- | --- |
| Schemaläggningsalternativ för **Veckovis** och **Månadsvis** för fullständig filexport | Du kan nu schemalägga fullständig filexport för personer och potentiella målgrupper varje vecka eller månad när du aktiverar till filbaserade mål för molnlagring. [Läs mer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) om schemaläggningsalternativ. |

{style="table-layout:auto"}

**Korrigeringar, förbättringar och andra meddelanden** {#destinations-fixes-and-enhancements}

- **Tvingande slutdatum för datauppsättningsexport fördröjt till 1 september 2025**\
  Som en del av [september 2024-utgåvan](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality) har Adobe angett standardslutdatumet 1 maj 2025 för datauppsättningsexportdataflöden som skapats *före den utgåvan*. Adobe förlänger nu den här tidsgränsen till **1 september 2025** för att ge kunderna ytterligare tid att uppdatera sina scheman. Mer information om hur du redigerar slutdatumet för ett datauppsättningsexportflöde finns i avsnittet om schemaläggning i självstudiekursen [Exportera datauppsättningar](../../destinations/ui/export-datasets.md#schedule-dataset-export).

- **Förbättrad hantering av misslyckade SFTP-överföringar för LiveRamp-introduktion**\
  Adobe har implementerat en korrigering för ett problem som påverkar filexporten till [LiveRamp Onboarding](/help/destinations/catalog/advertising/liveramp-onboarding.md)-målet via SFTP. Ibland misslyckades filöverföringar på grund av tillfälliga serverproblem, och tillfälliga filer från misslyckade försök finns kvar på servern. Dessa filer som inte kan tas bort blockerade efterföljande försök eftersom Adobe inte har behörighet att skriva över dem.\
  Om ett försök att ta bort den temporära filen inte kan tas bort med korrigeringen genereras en ny fil med det tillagda suffixet `attempt2` i Adobe, så att du kan vara säker på att återförsöket slutförs korrekt.

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Uppdaterade XDM-komponenter**

| Funktion | Beskrivning |
| --- | --- |
| Strängfält får minst ett värde | Nya strängfält får som standard en minsta längd på ett. Null-värden för fält som inte är obligatoriska accepteras fortfarande. Mer information om bästa praxis finns i guiden [Bästa praxis för datamodellering](../../xdm/schema/best-practices.md#data-integrity-tips) |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [Systemöversikten över XDM](../../xdm/home.md).

## Identitetstjänst {#identity}

Använd identitetstjänsten för Adobe Experience Platform för att skapa en heltäckande bild av dina kunder och deras beteenden genom att skapa en bro mellan identiteter på olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Begränsad tillgänglighet]{type=Informative} [!DNL Identity Graph Linking Rules] | Länkningsregler för identitetsdiagram har nu begränsad tillgänglighet och kan nås av alla kunder i utvecklingssandlådor. <ul><li>**Aktiveringskrav**: Funktionen förblir inaktiv tills du konfigurerar och sparar [!DNL Identity Settings]. Utan den här konfigurationen kommer systemet att fortsätta fungera som vanligt, utan att beteendet förändras.</li><li>**Viktigt!** Under den här fasen med begränsad tillgänglighet kan Edge-segmentering ge oväntade resultat. Direktuppspelning och gruppsegmentering fungerar dock som förväntat.</li><li>**Nästa steg**: Kontakta Adobe-kontoteamet om du vill ha mer information om hur du aktiverar den här funktionen i produktionssandlådor.</li></ul> |

{style="table-layout:auto"}

Mer information finns i [[!DNL Identity Graph Linking Rules] dokumentationen](../../identity-service/identity-graph-linking-rules/overview.md).

## Frågetjänst {#query-service}

Fråga efter data i Adobe Experience Platforms datasjö med hjälp av standard-SQL med Frågetjänst. Kombinera datauppsättningar sömlöst och generera nya från dina frågeresultat för att driva rapportering, aktivera datavetenskapliga arbetsflöden eller underlätta inmatning i kundprofil i realtid. Du kan till exempel sammanfoga kundtransaktionsdata med beteendedata för att identifiera värdefulla målgrupper för riktade marknadsföringskampanjer.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Skriv över SQL-målgrupp | Uppdatera målgruppsmedlemskapet genom att skriva över befintliga profiler med resultatet av en ny SQL-fråga. På så sätt kan ni hantera dynamiska målgrupper effektivare genom att ta bort gamla poster och infoga uppdaterade i en enda åtgärd. Mer information finns i [guiden för SQL-målgruppstillägg](../../query-service/data-distiller-audiences/overview.md#replace-audience). |
| Hämta och kopiera frågeresultat | [Hämta frågeresultat direkt från frågeredigeraren](../../query-service/ui/overview.md#download-query-results) som CSV-, XLSX- eller JSON-filer, eller [kopiera resultat till Urklipp](../../query-service/ui/overview.md#copy-results) som kommaavgränsade värden (CSV) för snabb användning i kalkylbladsprogram som Excel. Dessa förbättringar effektiviserar arbetsflödena för offlineanalys, rapportering och datavalidering. |
| Visa frågeresultat i helskärm | [Förhandsgranska frågan resulterar i en dialogruta i helskärmsläge](../../query-service/ui/overview.md#view-results) för att förbättra läsbarheten, enkelt skanna stora datamängder och välja rader för kopiering. I helskärmsläget finns en stödrasterlayout som du kan ändra storlek på, vilket gör att du kan granska breda tabeller och detaljerade utdata mer effektivt. |
| Förbättrad kolumnmarkering i modellförutsägelse | Välj specifika kolumner och tillämpa alias med den utökade syntaxen `model_predict`. Hämta resultat från mellanliggande förutsägelser, t.ex. funktionsvektorer och sannolikhetsresultat. Det utökade urvalet kräver aktivering av en funktionsflagga. Se [Modellens livscykeldokumentation](../../query-service/advanced-statistics/models.md#select-specific-output-fields) för syntaxexempel och information om funktionsflaggor. |
| Spara modellförutsägelseutdata med CREATE TABLE och INSERT INTO | [Spara valda förutsägelseutdata i nya tabeller med CREATE TABLE AS SELECT eller infoga i befintliga tabeller med INSERT INTO SELECT](../../query-service/advanced-statistics/models.md#predict). Om utökad kolumnmarkering är aktiverat kan mellanliggande resultat som funktionsvektorer och sannolikheter också bevaras tillsammans med slutliga prognoser. Exempel på användning finns i [SQL-syntaxdokumentationen](../../query-service/sql/syntax.md#create-table-as-select). |

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../../query-service/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med profilen kan du konsolidera kunddata till en enhetlig vy som ger en handlingsbar, tidsstämplad redogörelse för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Pseudonymt utgångsdatum för profildata | Hantera dina pseudonyma profildata när de förfaller på profilkontrollpanelen. Om du vill veta mer om den här funktionen och pseudonyma profiler läser du [utgångsguiden för pseudonyma profildata](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

Mer information om kundprofil i realtid finns i [profilöversikt](../../profile/home.md).

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav. För att tillgodose det här behovet tillhandahåller Experience Platform sandlådor som partitionerar en enda Experience Platform-instans i separata virtuella miljöer för att utveckla och förbättra program för digitala upplevelser.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för utökning av plugin-program för sandlådeverktyg | Anpassade åtgärder kan nu kopieras som ett beroende objekt när du duplicerar reseobjekt i sandlådeverktyg. Dessutom kan du välja befintliga åtgärder som ska återanvändas i målsandlådan. De kan också läggas till i ett paket oberoende av varandra. Fullständig information om vilka Adobe Journey Optimizer-objekt som stöds finns i handboken om [sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects). |

{style="table-layout:auto"}

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

Använd källor i Experience Platform för inmatning av data från ett Adobe-program eller en datakälla från tredje part.

**Nya källor**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md)-källan är nu tillgänglig. Använd den här källan för att ta med dina [!DNL Algolia]-användarprofiler till Experience Platform. Ni kan sedan använda dessa data för att förbättra användarengagemanget, konverteringsgraden och den övergripande kundupplevelsen genom att tillhandahålla högpresterande söklösningar för webbplatser, e-handelsplattformar och applikationer. Mer information finns i guiden om hur du [importerar [!DNL Algolia User Profiles] data till Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md). |
| [!BADGE Stöd för Beta]{type=Informative} API för [!DNL Azure Databricks] | [!DNL Azure Databricks]-källan är nu tillgänglig i API:t. Använd API:t [!DNL Flow Service] för att ansluta ditt [!DNL Databricks]-konto och överföra dina [!DNL Databricks]-data till Experience Platform. Mer information finns i dokumentationen om [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md). |

{style="table-layout:auto"}

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Uppdaterade XDM-fält för inmatning av strömmande mediedata i Experience Platform. | Den nya XDM-fältgruppen, `mediaReporting`, är nu tillgänglig för inhämtning av direktuppspelningsmediedata via Adobe Analytics-källan till Experience Platform. Det här fältet ersätter fältet `media.mediaTimed`.</br> <br>Under en övergångsperiod på tre månader kommer inmatning av data i `media.mediaTimed` fält att fortsätta. I slutet av juli 2025 kommer dock `media.mediaTimed`-fälten att vara helt inaktuella och inte längre synliga i användargränssnittet för Experience Platform Schema, och data kommer endast att skickas med hjälp av fälten `mediaReporting`.</br><br>Om du har implementerat Analytics-källan för att samla in Streaming Media-data till plattformen före 22 april 2025 måste du migrera dina befintliga konfigurationer för att skicka data med den nya fältgruppen. Denna migrering måste vara slutförd i slutet av juli 2025. Kontakta Adobe Account Team för migreringssupport. |
| Nya autentiseringstyper för [!DNL MariaDB] och [!DNL PostgreSQL] | Du kan nu använda grundläggande autentisering för att autentisera dina [!DNL MariaDB]- och [!DNL PostgreSQL]-källor på Experience Platform. Mer information finns i följande dokumentation: <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| Filtreringsstöd på radnivå för [!DNL Amazon Redshift] | Du kan använda filtreringsfunktioner på radnivå för dina [!DNL Amazon Redshift]-data på Experience Platform. Mer information finns i handboken om [filtrering av radnivådata för källor i API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

Mer information finns i [översikten över källor](../../sources/home.md).

## Use Case Playbooks {#use-case-playbooks}

Använd fallspelsböcker var ursprungligen utformade för att övervinna utmaningar när man kom igång med Real-Time Customer Data Platform eller Adobe Journey Optimizer. De fortsätter att utvecklas och gör det nu möjligt för er att snabbt komma igång med viktiga användningsfall för marknadsföring och tillhandahålla inspiration och färdiga resurser för att testa och börja producera.

Använd fallspelsböcker har gått över från ett identifieringsverktyg till ett samverkansbaserat ramverk. De hjälper er nu att skapa, hantera och dela egna spelböcker i olika organisationer.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Beta]{type=Informative} Skapa och dela dina egna spelböcker | Med nya Playbook Authoring Framework kan du skapa, hantera och dela egna fallspelböcker. Detta inkluderar stöd för att hämta viktiga metadata, redigera färdkartor och associera relevanta tekniska resurser. Ni kan dela Playbooks mellan olika organisationer för att standardisera marknadsföringsstrategier och upprätthålla enhetlighet. |

{style="table-layout:auto"}

Läs dokumentet [Författare och dela dina egna spelböcker](/help/use-case-playbooks/playbooks/author.md) om du vill lära dig hur du kan skapa och dela dina egna spelböcker.

Mer information finns i översikten [Använd fallspelningsböcker](/help/use-case-playbooks/playbooks/overview.md) som ger en översikt över spelbokens funktion, syfte och en heltäckande demonstration, inklusive hur du skapar instanser och importerar genererade resurser till andra sandlådemiljöer.
