---
title: Versionsinformation om Adobe Experience Platform september 2022
description: Versionsinformationen för Adobe Experience Platform från september 2022.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2723'
ht-degree: 20%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 28 september 2022**

Nya funktioner i Adobe Experience Platform:

- [Attributbaserad åtkomstkontroll](#abac)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Granskningsloggar](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Datainsamling](#data-collection)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Frågetjänst](#query-service)
- [Källor](#sources)

## Attributbaserad åtkomstkontroll {#abac}

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll aktiveras från och med oktober 2022. Om du vill bli tidig användare kan du kontakta din Adobe-representant.

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika Experience Platform-användare i organisationen.

Med attributbaserad åtkomstkontroll kan administratören styra användarnas åtkomst till, känsliga personuppgifter (SPD), personligt identifierbar information (PII) och andra anpassade typer av data i alla Experience Platform arbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

| Funktion | Beskrivning |
| --- | --- |
| Attributbaserad åtkomstkontroll | Med attributbaserad åtkomstkontroll kan du etikettera XDM-schemafält (Experience Data Model) och segment med etiketter som definierar användningsområde för organisation eller data. Samtidigt kan administratörer använda användar- och rolladministrationsgränssnittet för att definiera åtkomstprinciper som omfattar XDM-schemafält och -segment för att bättre hantera åtkomsten som ges till användare eller användargrupper (interna, externa eller externa användare). Mer information finns i [Översikt över den attributbaserade åtkomstkontrollen](../../access-control/abac/overview.md). |
| Behörigheter | Behörigheter är det område i Experience Cloud där administratörer kan definiera användarroller och åtkomstprinciper för att hantera åtkomstbehörigheter för funktioner och objekt i ett produktprogram. Med behörigheter kan du skapa och hantera roller, tilldela önskade resursbehörigheter för dessa roller och skapa profiler för att utnyttja etiketter och definiera vilka användarroller som har åtkomst till specifika Experience Platform-resurser. Med behörigheter kan du också hantera etiketter, sandlådor och användare som är kopplade till en viss roll. Mer information finns i [Användargränssnittsguiden för behörigheter](../../access-control/abac/ui/browse.md). |

Mer information om attributbaserad åtkomstkontroll finns i [översikt över attributbaserad åtkomstkontroll](../../access-control/abac/overview.md). En utförlig guide om det attributbaserade arbetsflödet för åtkomstkontroll finns i [heltäckande attributbaserad åtkomstkontroll](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML-tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa modeller som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskap.

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktpunkter som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktpunkt för marknadsföring över kundresor.

| Funktion | Beskrivning |
| --- | --- |
| Spara utkastinstans | Med den här nya funktionen kan marknadsföringsanalytiker spara en modellkonfiguration som ett utkast och fortsätta redigera den tills den är klar innan utbildning och poängsättning. Scenarier där den här funktionen är användbar kan vara när en användare har flera fält att definiera i arbetsflödet men inte kan slutföra den på grund av tidsbegränsningar. Ett annat scenario är när en eller flera datauppsättningsstatistik bearbetas och inte är tillgängliga än. Läs användarhandboken för [Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) om du vill veta mer. |
| Styrningspolitik | När användare har skickat in för att skapa en instans via konfigurationsarbetsflödet kontrollerar den nya tjänsten för regelefterlevnad om det finns några regelbrott för dataanvändningen och visar informationen i en port. Det ser till att dataåtgärder och marknadsföringsåtgärder är kompatibla med dataanvändningsprinciper som konfigurerats på Adobe Experience Platform. |

Mer information om Attribution AI finns i [AI-översikten för Attribution](../../intelligent-services/attribution-ai/overview.md). Mer information om policyer för datastyrning finns i [principöversikten](../../data-governance/policies/overview.md).

### Kund-AI

Customer AI available in Real-Time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale.

| Funktion | Beskrivning |
| --- | --- |
| Spara utkastinstans | Med den här nya funktionen kan marknadsföringsanalytiker spara en modellkonfiguration som ett utkast och fortsätta redigera den tills den är klar innan utbildning och poängsättning. Scenarier där den här funktionen är användbar kan vara när en användare har flera fält att definiera i arbetsflödet men inte kan slutföra den på grund av tidsbegränsningar. Ett annat scenario är när en eller flera datauppsättningsstatistik bearbetas och inte är tillgängliga än. Läs användarhandboken för [AI för kunder](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) om du vill veta mer. |
| Styrningspolitik | När användare har skickat in för att skapa en instans via konfigurationsarbetsflödet kontrollerar den nya tjänsten för regelefterlevnad om det finns några regelbrott för dataanvändningen och visar informationen i en port. Det ser till att dataåtgärder och marknadsföringsåtgärder är kompatibla med dataanvändningsprinciper som konfigurerats på Adobe Experience Platform. |

Mer information om AI för kunder finns i [Översikt över AI för kunder](../../intelligent-services/customer-ai/overview.md). Mer information om policyer för datastyrning finns i [principöversikten](../../data-governance/policies/overview.md).

## Granskningsloggar {#audit-logs}

Med Experience Platform kan du granska användaraktivitet för olika tjänster och funktioner. Granskningsloggarna innehåller information om vem som gjorde vad och när.

**Uppdaterade funktioner**

| Funktion | Namn | Beskrivning |
| --- | --- | --- |
| Tillagda resurser | <ul><li>Attribution AI-instans</li><li>AI-instans för kund</li><li>Datastream</li></ul> | Granskningsloggresurser registreras automatiskt när aktiviteten utförs. Om funktionen är aktiverad behöver du inte aktivera loggsamling manuellt. |

{style="table-layout:auto"}

Mer information om olika resursspecifika händelsetyper som spåras av granskningsloggar i Experience Platform finns i [översikten över granskningsloggar](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan visa viktiga insikter om organisationens data, som fångas upp under dagliga ögonblicksbilder.

| Funktion | Beskrivning |
| --- | --- |
| Etikett för användning | När den visas i widgetbiblioteket identifierar etiketten som används enkelt att det finns befintliga widgetar på din instrumentpanel. Det gör det enkelt att undvika duplicering, även om du kan lägga till samma widget flera gånger om du vill. |
| Användardefinierade kontrollpaneler | Användardefinierade kontrollpaneler hjälper dig att få bättre insikter och anpassa visualiseringar genom att du kan skapa och hantera anpassade kontrollpaneler. Med användardefinierade kontrollpaneler kan du skapa, lägga till och redigera anpassade widgetar för att visualisera viktiga nyckeltal som är relevanta för organisationen. Läs [funktionsguiden](../../dashboards/standard-dashboards.md) om du vill veta mer. |
| Datamodell för Insikter om kunddataplattform | Funktionen CDP (Customer Data Platform) Insights Data Model visar de datamodeller och SQL som driver insikterna för olika profil-, mål- och segmenteringswidgetar. Du kan anpassa de här SQL-frågemallarna för att skapa CDP-rapporter för dina användningsfall för marknadsförings- och nyckelutförandeindikatorer. Dessa insikter kan sedan användas som anpassade widgetar för dina användardefinierade instrumentpaneler. Läs funktionsguiden [CDP Insights Data Model](../../dashboards/data-models/cdp-insights-data-model-b2c.md) om du vill veta mer. |
| Rapportwidget för publiköverlappning | Den här widgeten är tillgänglig för både [!UICONTROL Profiles]- och [!UICONTROL Segments]-instrumentpaneler. Rapporten innehåller en ordnad lista över målgrupper som rangordnas efter de högsta eller lägsta överlappningsprocentsatserna för det valda segmentet. Från kontrollpanelen [!UICONTROL Profiles] kan du filtrera och visa målgruppsöverlappning genom att sammanfoga principer från alla tillgängliga segment. Med kontrollpanelerna [!UICONTROL Segments] kan du filtrera målgruppsöverlappningen efter ett visst segment.<br>Använd den här analysen för att skapa nya högpresterande segment och undvika att skicka samma målgrupp till olika destinationer. Rapporten kan också hjälpa till att identifiera dolda insikter för att förbättra segmenteringen eller hitta unika profiler att eftersträva. Läs respektive [profiler](../../dashboards/guides/profiles.md#audience-overlap-report) och [segmentwidgetguider](../../dashboards/guides/audiences.md#audience-overlap-report) om du vill veta mer. |

Mer information om [!DNL Dashboards] finns i [[!DNL Dashboards] översikten](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform tillhandahåller en uppsättning tekniker som gör att du kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omvandlas och distribueras till mål inom eller utanför Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Integrering av vänster navigering i Experience Platform UI | Alla funktioner som tidigare var exklusiva för användargränssnittet för datainsamling (inklusive taggar, vidarebefordran av händelser och datastreams) är nu även tillgängliga via den vänstra navigeringen i Experience Platform, under kategorin **[!UICONTROL Data Collection]**. Detta eliminerar behovet av att växla mellan användargränssnitt när du arbetar med datainsamlingsfunktioner i Experience Platform. |
| Användarattribuering i taggar och händelsevidarebefordran | När [!UICONTROL Properties] listas i taggar och händelsevidarebefordran visas nu varje egenskap i listan när den senast uppdaterades och vilken användare som gjorde uppdateringen. |
| [[!DNL Snap Conversions API] tillägg](https://exchange.adobe.com/apps/ec/108550) för händelsevidarebefordran | Du kan nu skicka data till [!DNL Snapchat Conversions API] med ett [vidarebefordringstillägg](../../tags/ui/event-forwarding/overview.md). Mer information om hur du autentiserar dig och använder API:et finns i [[!DNL Snapchat Marketing API] dokumentationen](https://marketingapi.snapchat.com/docs/conversion.html). |
| [Klienttips för användaragent i Web SDK](/help/web-sdk/use-cases/client-hints.md) | Web SDK har nu stöd för [klienttips för användaragent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Klienttips gör att webbplatsägare kan komma åt mycket av den information som finns i strängen [!DNL User-Agent], men på ett mer sekretessbeständigt sätt. |
| [Migrering sida vid sida för SDK på webben](../../web-sdk/home.md#migrating-to-web-sdk) | Du kan nu migrera dina befintliga webbegenskaper från andra Experience Cloud-bibliotek, som [!DNL at.js], till Web SDK, en sida i taget. Detta möjliggör en stegvis hantering av migrering av SDK på webben, utan att du behöver migrera alla sidor samtidigt. |
| [[!DNL Adobe Journey Optimizer] stöd för datastreams](../../datastreams/overview.md#aep) | Adobe Experience Platform-tjänsten för datastreams stöder nu [!DNL Adobe Journey Optimizer]. Med det här alternativet kan du använda webb- och appbaserade inkommande kanaler i [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

Mer information om datainsamling i Experience Platform finns i [datainsamlingsöversikten](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| Destination SDK | Destination SDK ger nu fullt stöd för partners och kunder som skapar gruppvis (eller filbaserat) producerade eller privata destinationer. Mer information finns på följande dokumentationssidor: <ul><li>[Destination SDK - översikt](../../destinations/destination-sdk/overview.md)</li><li>[Konfigurera ett filbaserat mål](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Konfigurera filformateringsalternativ för filbaserade mål](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Testa dina filbaserade mål](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Nya eller uppdaterade mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services är en plattform för att designa flerkanaliga kundupplevelser och en miljö för visuell kampanjsamordning, interaktionshantering i realtid och flerkanalsmarknadsföring. [Kom igång med kampanj](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Observera att den här integreringen fungerar med [Adobe Campaign version 8.4 eller senare](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | Målet [!DNL Salesforce CRM] har uppdaterats för att stödja både kontakt- och lead-uppdateringar samt prestandaförbättringar för snabbare uppdateringar. |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation**

| Dokumentation | Beskrivning |
| ----------- | ----------- |
| API-dokumentation för destinationsflödestjänst | Referenshandboken för [Destinations-API:t](https://developer.adobe.com/experience-platform-apis/references/destinations/) har uppdaterats med vägledning om hur åtgärder ska utföras på filbaserade mål. Åtgärder för direktuppspelningsmål läggs till vid ett senare tillfälle. |

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Gränssnittsstöd för uppräkningar och föreslagna värden | Förutom enum som aktiverar dataverifiering kan du nu [lägga till eller ta bort föreslagna värden](../../xdm/ui/fields/enum.md) för standardsträngfält eller anpassade strängfält så att Experience Platform-användare har en egen lista med värden att välja mellan när segment skapas. |

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Egenskaper för ett specifikt element som interagerades och som orsakade att proposition-händelsen utlöstes. |
| Fältgrupp | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Spåra medieinteraktioner över tid. |
| Fältgrupp | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Information om medieinformation spåras. |
| Fältgrupp | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beskriver ytor för Experience Events i Adobe Journey Optimizer. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Beteende | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Tillagda värden för `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Värden för `eventType` har tagits bort:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Fältgrupp | (Flera) | [Uppdaterade flera fältbeskrivningar](https://github.com/adobe/xdm/pull/1628/files) för alla Journey Orchestration-komponenter. |
| Fältgrupp | (Flera) | [Titlarna för flera Adobe Workfront-komponenter har uppdaterats](https://github.com/adobe/xdm/pull/1634/files) för att vara konsekventa. |
| Fältgrupp | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Namnområdena för flera fält har uppdaterats till `xdm`. |
| Fältgrupp | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Ett nytt fält har lagts till, `isReadSegmentTriggerStartEvent`. |
| Fältgrupp | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Fältet `xdm:uvIndex` har ändrats till en heltalstyp och namnutrymmet `xdm` har lagts till i flera fält där det saknades. |
| Fältgrupp | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` och `xdm:implementationDetails` har tagits bort från fältgruppen. |
| Datatyp | (Flera) | [Uppdaterade flera mediaegenskapsnamn](https://github.com/adobe/xdm/pull/1626/files) för flera datatyper, vilket ger enhetlighet. |
| Datatyp | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Okända namn för fladder har lagts till. |
| Datatyp | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Datatypen kan nu acceptera en lista med metadatanyckelvärdepar som är associerade med den aktuella punkten. |
| Datatyp | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] har bytt namn till [!UICONTROL Proposition Action]. |
| Datatyp | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] har bytt namn till [!UICONTROL Proposition Action]. |
| (Flera) | (Flera) | Experimentella egenskaper har [stabiliserats för alla B2B-komponenter](https://github.com/adobe/xdm/pull/1617/files). |
| (Flera) | (Flera) | Adobe Journey Optimizer-entiteter har [stabiliserats](https://github.com/adobe/xdm/pull/1625/files). |
| (Flera) | (Flera) | Namnutrymmena för vissa fält i flera experimentella komponenter har [uppdaterats för konsekvens](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Identitetstjänst {#identity-service}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för borttagning av datauppsättningar | Identitetstjänsten har nu stöd för borttagning av datauppsättningar vid begäran via [katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), gränssnitt eller datahygien. Mer information finns i guiden [Ta bort datauppsättningar i användargränssnittet](../../catalog/datasets/user-guide.md#delete-a-dataset). |

Läs [Översikt över identitetstjänsten](../../identity-service/home.md) om du vill veta mer om identitetstjänsten.

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard SQL för att söka efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla samman alla datauppsättningar från [!DNL Data Lake] och samla in sökresultaten som en ny datauppsättning för användning i rapportering, arbetsytan för datavetenskap eller för inmatning i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aviseringsprenumerations-API | Med Adobe Experience Platform Query Service kan du prenumerera på aviseringar för både ad hoc-frågor och schemalagda frågor. Varningar kan tas emot via e-post, i Experience Platform-gränssnittet eller båda. Frågevarningar kan för närvarande bara prenumereras på med [Query Service API](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Datauppsättningsexempel | Med hjälp av datamängdsprover från frågetjänsten kan du utföra undersökande frågor på stora data, vilket minskar bearbetningstiden avsevärt och därmed kan ge korrekta frågor. Mer information finns i [exempelguiden för datauppsättningar](../../query-service/key-concepts/dataset-samples.md). |

Mer information om [!DNL Query Service] finns i [[!DNL Query Service] översikten](../../query-service/home.md).

Läs [frågevarningsdokumentationen](../../query-service/api/alert-subscriptions.md) om du vill veta mer.

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Audience Manager segmentpopulation påverkar kundprofilen i realtid | Intag av stora Audience Manager-segmentpopulationer påverkar direkt det totala antalet profiler när du skickar ett Audience Manager-segment till Experience Platform med hjälp av Audience Manager-källan. Det innebär att om du väljer alla segment kan det eventuellt leda till ett profilantal som överskrider licensanvändningsbehörigheten. Mer information finns i [Audience Manager källöversikt](../../sources/connectors/adobe-applications/audience-manager.md). Mer information om din licensanvändning finns i dokumentationen om [med kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md). |
| Stöd för Adobe Campaign Managed Cloud Service | Använd Adobe Campaign Managed Cloud Service-källa för att överföra data från Adobe Campaign v8.4-leverans och spårningsloggar till Experience Platform. Mer information finns i guiden om att [skapa en Adobe Campaign Managed Cloud Service-källanslutning i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/campaign.md). |
| API-stöd för on demand-inmatning för batchkällor | Använd on-demand-inmatning för att skapa ad hoc-flödeskörningar för ett givet dataflöde med API:t [!DNL Flow Service]. Skapade flödeskörningar måste anges som engångsintag. Mer information finns i guiden om att [skapa en flödeskörning för on-demand-import med API](../../sources/tutorials/api/on-demand-ingestion.md). |
| API-stöd för nya försök med misslyckade dataflöden för batchkällor | Använd åtgärden `re-trigger` om du vill försöka återskapa det misslyckade dataflödet via API:t. Mer information finns i guiden [Återförsöken av misslyckade dataflöden med API](../../sources/tutorials/api/retry-flows.md). |
| API-stöd för filtrering av radnivådata för källorna [!DNL Google BigQuery] och [!DNL Snowflake] | Använd logiska operatorer och jämförelseoperatorer för att filtrera radnivådata för källorna [!DNL Google BigQuery] och [!DNL Snowflake]. Mer information finns i guiden [om att filtrera data för en källa med API](../../sources/tutorials/api/filter.md). |

Mer information om källor finns i [översikten över källor](../../sources/home.md).
