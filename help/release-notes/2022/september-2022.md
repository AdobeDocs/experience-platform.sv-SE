---
title: Adobe Experience Platform Release Notes september 2022
description: Versionsinformation för september 2022 för Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 4bdbb987905b6010f4b4f75bee060828d0e07368
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 2%

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
- [Mål ](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Frågetjänst](#query-service)
- [Källor](#sources)

## Attributbaserad åtkomstkontroll {#abac}

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll aktiveras från och med oktober 2022. Om du vill bli en tidig användare, vänligen kontakta din Adobe-representant.

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Tack vare attributbaserad åtkomstkontroll kan administratören styra användarnas åtkomst till, känsliga personuppgifter (SPD), personligt identifierbar information (PII) och andra anpassade typer av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

| Funktion | Beskrivning |
| --- | --- |
| Attributbaserad åtkomstkontroll | Med attributbaserad åtkomstkontroll kan du etikettera XDM-schemafält (Experience Data Model) och segment med etiketter som definierar användningsområde för organisation eller data. Samtidigt kan administratörer använda användar- och rolladministrationsgränssnittet för att definiera åtkomstprinciper som omfattar XDM-schemafält och -segment för att bättre hantera åtkomsten som ges till användare eller användargrupper (interna, externa eller externa användare). Mer information finns i [attributbaserad åtkomstkontroll - översikt](../../access-control/abac/overview.md). |
| Behörigheter | Behörigheter är det område i Experience Cloud där administratörer kan definiera användarroller och åtkomstprinciper för att hantera åtkomstbehörigheter för funktioner och objekt i ett produktprogram. Med behörigheter kan du skapa och hantera roller, tilldela önskade resursbehörigheter för de här rollerna och skapa profiler för att utnyttja etiketter och definiera vilka användarroller som har åtkomst till specifika plattformsresurser. Med behörigheter kan du också hantera etiketter, sandlådor och användare som är kopplade till en viss roll. Mer information finns i [Användargränssnittshandbok för behörigheter](../../access-control/abac/ui/browse.md). |

Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll - översikt](../../access-control/abac/overview.md). En omfattande guide om det attributbaserade arbetsflödet för åtkomstkontroll finns i [attribueringsbaserad åtkomstkontroll från början till slut](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML-tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa modeller som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis.

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktpunkter som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktpunkt för marknadsföring över kundresor.

| Funktion | Beskrivning |
| --- | --- |
| Spara utkastinstans | Med den här nya funktionen kan marknadsföringsanalytiker spara en modellkonfiguration som ett utkast och fortsätta redigera den tills den är klar innan utbildning och poängsättning. Scenarier där den här funktionen är användbar kan vara när en användare har flera fält att definiera i arbetsflödet men inte kan slutföra den på grund av tidsbegränsningar. Ett annat scenario är när en eller flera datauppsättningsstatistik bearbetas och inte är tillgängliga än. Läs [Användarhandbok för Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) om du vill veta mer. |
| Styrningspolitik | När användare har skickat in för att skapa en instans via konfigurationsarbetsflödet kontrollerar den nya tjänsten för regelefterlevnad om det finns några regelbrott för dataanvändningen och visar informationen i en port. Det ser till att dataåtgärder och marknadsföringsåtgärder är kompatibla med dataanvändningsprinciper som konfigurerats på Adobe Experience Platform. |

Mer information om Attribution AI finns i [Översikt över Attribution AI](../../intelligent-services/attribution-ai/overview.md). Mer information om policyer för datastyrning finns i [profiler, översikt](../../data-governance/policies/overview.md).

### Kund-AI

Customer AI available in Real-time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale.

| Funktion | Beskrivning |
| --- | --- |
| Spara utkastinstans | Med den här nya funktionen kan marknadsföringsanalytiker spara en modellkonfiguration som ett utkast och fortsätta redigera den tills den är klar innan utbildning och poängsättning. Scenarier där den här funktionen är användbar kan vara när en användare har flera fält att definiera i arbetsflödet men inte kan slutföra den på grund av tidsbegränsningar. Ett annat scenario är när en eller flera datauppsättningsstatistik bearbetas och inte är tillgängliga än. Läs [Användarhandbok för AI](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) om du vill veta mer. |
| Styrningspolitik | När användare har skickat in för att skapa en instans via konfigurationsarbetsflödet kontrollerar den nya tjänsten för regelefterlevnad om det finns några regelbrott för dataanvändningen och visar informationen i en port. Det ser till att dataåtgärder och marknadsföringsåtgärder är kompatibla med dataanvändningsprinciper som konfigurerats på Adobe Experience Platform. |

Mer information om AI för kunder finns i [Översikt över AI för kunder](../../intelligent-services/customer-ai/overview.md). Mer information om policyer för datastyrning finns i [profiler, översikt](../../data-governance/policies/overview.md).

## Granskningsloggar {#audit-logs}

Med Experience Platform kan du granska användaraktivitet för olika tjänster och funktioner. Granskningsloggarna innehåller information om vem som gjorde vad och när.

**Uppdaterade funktioner**

| Funktion | Namn | Beskrivning |
| --- | --- | --- |
| Tillagda resurser | <ul><li>Attribution AI instans</li><li>AI-instans för kund</li><li>Datastream</li></ul> | Granskningsloggresurser registreras automatiskt när aktiviteten utförs. Om funktionen är aktiverad behöver du inte aktivera loggsamling manuellt. |

{style="table-layout:auto"}

Mer information om de olika resursspecifika händelsetyperna som spåras av granskningsloggar i Platform finns i [granskningsloggar - översikt](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform tillhandahåller flera instrumentpaneler där du kan se viktiga insikter om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

| Funktion | Beskrivning |
| --- | --- |
| Etikett för användning | När den visas i widgetbiblioteket identifierar etiketten som används enkelt att det finns befintliga widgetar på din instrumentpanel. Det gör det enkelt att undvika duplicering, även om du kan lägga till samma widget flera gånger om du vill. |
| Användardefinierade kontrollpaneler | Användardefinierade kontrollpaneler hjälper dig att få bättre insikter och anpassa visualiseringar genom att du kan skapa och hantera anpassade kontrollpaneler. Med användardefinierade kontrollpaneler kan du skapa, lägga till och redigera anpassade widgetar för att visualisera viktiga nyckeltal som är relevanta för organisationen. Läs [funktionsguide](../../dashboards/user-defined-dashboards.md) om du vill veta mer. |
| Datamodell för Insikter om kunddataplattform | Funktionen CDP (Customer Data Platform) Insights Data Model visar de datamodeller och SQL som driver insikterna för olika profil-, mål- och segmenteringswidgetar. Du kan anpassa de här SQL-frågemallarna för att skapa CDP-rapporter för dina användningsfall för marknadsförings- och nyckelutförandeindikatorer. Dessa insikter kan sedan användas som anpassade widgetar för dina användardefinierade instrumentpaneler. Läs [Funktionsguide för CDP Insights-datamodell](../../dashboards/cdp-insights-data-model.md) om du vill veta mer. |
| Rapportwidget för publiköverlappning | Den här widgeten är tillgänglig för båda [!UICONTROL Profiles] och [!UICONTROL Segments] instrumentpaneler. Rapporten innehåller en ordnad lista över målgrupper som rangordnas efter de högsta eller lägsta överlappningsprocentsatserna för det valda segmentet. Från [!UICONTROL Profiles] på kontrollpanelen kan du filtrera och visa målgruppsöverlappning genom att sammanfoga principer från alla tillgängliga segment. The [!UICONTROL Segments] Med kontrollpaneler kan du filtrera målgruppsöverlappningen efter ett visst segment.<br>Använd den här analysen för att skapa nya högpresterande segment och undvika att skicka samma målgrupp till olika destinationer. Rapporten kan också hjälpa till att identifiera dolda insikter för att förbättra segmenteringen eller hitta unika profiler att eftersträva. Läs respektive [profiler](../../dashboards/guides/profiles.md#audience-overlap-report) och [segment](../../dashboards/guides/audiences.md#audience-overlap-report) widgetguider för mer information. |

Mer information om [!DNL Dashboards], se [[!DNL Dashboards] översikt](../../dashboards/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Integrering med vänster navigering i plattformsgränssnittet | Alla funktioner som tidigare var exklusiva för användargränssnittet för datainsamling (inklusive taggar, vidarebefordran av händelser och datastreams) är nu även tillgängliga via den vänstra navigeringen i Experience Platform, under kategorin **[!UICONTROL Data Collection]**. Detta eliminerar behovet av att växla mellan användargränssnitt när du arbetar med datainsamlingsfunktioner i Platform. |
| Användarattribuering i taggar och händelsevidarebefordran | När listning är tillgänglig [!UICONTROL Properties] in-taggar och vidarebefordran av händelser, visar nu alla angivna egenskaper när de senast uppdaterades och vilken användare som gjorde uppdateringen. |
| [[!DNL Snap Conversions API] extension](https://exchange.adobe.com/apps/ec/108550) för vidarebefordran av händelser | Nu kan du skicka data till [!DNL Snapchat Conversions API] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Mer information om hur du autentiserar och använder API:t finns i [[!DNL Snapchat Marketing API] dokumentation](https://marketingapi.snapchat.com/docs/conversion.html). |
| [[!DNL User-Agent Client Hints] i Web SDK](../../edge/fundamentals/user-agent-client-hints.md) | Web SDK har nu stöd för [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Klienttips gör att webbplatsägare kan komma åt mycket av den information som finns i [!DNL User-Agent] på ett mer sekretessbelagt sätt. |
| [Migrering av sida vid sida för Web SDK](../../edge/home.md#migrating-to-web-sdk) | Nu kan du migrera dina befintliga webbegenskaper från andra Experience Cloud-bibliotek, till exempel [!DNL at.js], till Web SDK, en sida i taget. Detta möjliggör en stegvis hantering av Web SDK-migrering, utan att du behöver migrera alla sidor samtidigt. |
| [[!DNL Adobe Journey Optimizer] stöd för datastreams](../../edge/datastreams/overview.md#aep) | Adobe Experience Platform-tjänsten för datastreams har nu stöd för [!DNL Adobe Journey Optimizer]. Med det här alternativet kan du använda webb- och appbaserade inkommande kanaler i [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

Mer information om datainsamling i Platform finns i [datainsamling - översikt](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| Destination SDK | Destination SDK ger nu fullt stöd för partners och kunder som skapar batchvis (eller filbaserat) producerade eller privata destinationer. Mer information finns på följande dokumentationssidor: <ul><li>[Översikt över Destination SDK](../../destinations/destination-sdk/overview.md)</li><li>[Konfigurera ett filbaserat mål](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Konfigurera filformateringsalternativ för filbaserade mål](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Testa dina filbaserade mål](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Nya eller uppdaterade destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services är en plattform för att designa flerkanaliga kundupplevelser och en miljö för visuell kampanjsamordning, interaktionshantering i realtid och flerkanalsmarknadsföring. [Kom igång med Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Observera att den här integreringen fungerar med [Adobe Campaign version 8.4 eller senare](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | The [!DNL Salesforce CRM] målet har uppdaterats för att stödja både kontakt- och lead-uppdateringar samt prestandaförbättringar för snabbare uppdateringar. |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation**

| Dokumentation | Beskrivning |
| ----------- | ----------- |
| API-dokumentation för destinationsflödestjänst | The [Referenshandbok för destinations-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) uppdaterades med vägledning om hur åtgärder ska utföras på filbaserade mål. Åtgärder för direktuppspelningsmål läggs till vid ett senare tillfälle. |

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Gränssnittsstöd för uppräkningar och föreslagna värden | Förutom uppräkningar som aktiverar dataverifiering kan du nu [lägga till eller ta bort föreslagna värden](../../xdm/ui/fields/enum.md) för standardsträngfält eller anpassade strängfält så att plattformsanvändare har en egen lista med värden att välja mellan när segment skapas. |

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
| Beteende | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Tillagda värden för `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Borttagna värden för `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Fältgrupp | (Flera) | [Uppdaterade flera fältbeskrivningar](https://github.com/adobe/xdm/pull/1628/files) över Journey Orchestration-komponenter. |
| Fältgrupp | (Flera) | [Titlarna för flera Adobe Workfront-komponenter har uppdaterats](https://github.com/adobe/xdm/pull/1634/files) för enhetlighet. |
| Fältgrupp | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Namnutrymmena för flera fält har uppdaterats till `xdm`. |
| Fältgrupp | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Ett nytt fält har lagts till, `isReadSegmentTriggerStartEvent`. |
| Fältgrupp | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Ändrad `xdm:uvIndex` fält till en heltalstyp och lägger till `xdm` namnutrymme till flera fält som saknades. |
| Fältgrupp | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` och `xdm:implementationDetails` har tagits bort från fältgruppen. |
| Datatyp | (Flera) | [Uppdaterat flera mediaegenskapsnamn](https://github.com/adobe/xdm/pull/1626/files) i flera datatyper för att vara konsekventa. |
| Datatyp | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Okända namn för fladder har lagts till. |
| Datatyp | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Datatypen kan nu acceptera en lista med metadatanyckelvärdepar som är associerade med den aktuella punkten. |
| Datatyp | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] har bytt namn till [!UICONTROL Proposition Action]. |
| Datatyp | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] har bytt namn till [!UICONTROL Proposition Action]. |
| (Flera) | (Flera) | Experimentella egenskaper har [stabiliserad för alla B2B-komponenter](https://github.com/adobe/xdm/pull/1617/files). |
| (Flera) | (Flera) | Adobe Journey Optimizer enheter har [stabiliserad](https://github.com/adobe/xdm/pull/1625/files). |
| (Flera) | (Flera) | Namnutrymmen för vissa fält i flera experimentella komponenter har [uppdaterat för enhetlighet](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Identitetstjänst {#identity-service}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för borttagning av datauppsättningar | Identitetstjänsten har nu stöd för borttagning av datauppsättningar vid begäran via [Katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), användargränssnittet eller datahygien. Läs guiden på [ta bort datauppsättningar i användargränssnittet](../../catalog/datasets/user-guide.md#delete-a-dataset) för mer information. |

Mer information om identitetstjänsten finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, datavetenskapen eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aviseringsprenumerations-API | Med Adobe Experience Platform Query Service kan du prenumerera på aviseringar för både ad hoc-frågor och schemalagda frågor. Varningar kan tas emot via e-post, i användargränssnittet för plattformen eller båda. Frågevarningar kan för närvarande bara prenumereras på med [API för frågetjänst](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Datauppsättningsexempel | Med hjälp av datamängdsprover från frågetjänsten kan du utföra undersökande frågor på stora data, vilket minskar bearbetningstiden avsevärt och därmed kan ge korrekta frågor. Se [exempelguide för datauppsättning](../../query-service/essential-concepts/dataset-samples.md) om du vill veta mer. |

Mer information om [!DNL Query Service], se [[!DNL Query Service] översikt](../../query-service/home.md).

Se [frågeaviseringsdokumentation](../../query-service/api/alert-subscriptions.md) om du vill veta mer.

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Audience Manager segmentpopulationens påverkan på kundprofilen i realtid | Intag av stora Audience Manager-segmentpopulationer har en direkt inverkan på det totala antalet profiler när du för första gången skickar ett Audience Manager-segment till plattformen via Audience Manager. Det innebär att om du väljer alla segment kan det eventuellt leda till ett profilantal som överskrider licensanvändningsbehörigheten. Mer information finns i [Översikt över Audience Manager-källa](../../sources/connectors/adobe-applications/audience-manager.md). Mer information om licensanvändningen finns i dokumentationen om [med kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md). |
| Stöd för Adobe Campaign Managed Cloud Service | Använd Adobe Campaign Managed Cloud Service-källan för att skicka data från Adobe Campaign v8.4-leverans och spårningsloggar till Experience Platform. Läs guiden på [skapa en källanslutning till en hanterad Cloud Service från Adobe Campaign i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/campaign.md) för mer information. |
| API-stöd för on demand-inmatning för batchkällor | Använd on-demand-inmatning för att skapa ad hoc-flöden för ett givet dataflöde med [!DNL Flow Service] API. Skapade flödeskörningar måste anges som engångsintag. Mer information finns i guiden [skapa en flödeskörning för on-demand-inmatning med API](../../sources/tutorials/api/on-demand-ingestion.md) för mer information. |
| API-stöd för nya försök med misslyckade dataflödeskörningar för batchkällor | Använd `re-trigger` för att försöka återanvända det misslyckade dataflödet via API:t. Läs guiden på [försöka köra misslyckade dataflöden igen med API](../../sources/tutorials/api/retry-flows.md) för mer information. |
| API-stöd för filtrering av radnivådata för [!DNL Google BigQuery] och [!DNL Snowflake] källor | Använd logiska operatorer och jämförelseoperatorer för att filtrera radnivådata för [!DNL Google BigQuery] och [!DNL Snowflake] källor. Läs guiden på [filtrera data för en källa med API](../../sources/tutorials/api/filter.md) för mer information. |

Läs mer om källor i [källöversikt](../../sources/home.md).
