---
title: Adobe Experience Platform Release Notes september 2022
description: Versionsinformation för september 2022 för Adobe Experience Platform.
source-git-commit: 3d7a04c0ec6cf6a9bed90c9c22db2e8b56bfa01f
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 28 september 2022**

Nya funktioner i Adobe Experience Platform:

- [Datahygien](#data-hygiene)
- [[!UICONTROL Privacy Console]](#privacy-console)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Granskningsloggar](#audit-logs)
- [Datainsamling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Källor](#sources)

## Datahygien {#data-hygiene}

Adobe Experience Platform har en robust uppsättning verktyg för hantering av stora, komplicerade dataåtgärder för att samordna kundupplevelser. När data hämtas in till systemet över tid blir det allt viktigare att hantera dina datalager så att data används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationsprofiler anser det nödvändigt.

Med Adobe Experience Platform datahygifunktioner kan du rensa dina data genom att schemalägga automatiska datauppsättningsutgångsdatum och programmässigt ta bort konsumentdata per identitet.

>[!NOTE]
>
>Funktioner för borttagning av konsumentinformation är endast tillgängliga för organisationer som har köpt Adobe Healthcare Shield eller Privacy Shield.

Läs följande dokumentation för att komma igång med datahygien:

- [Datahygien - översikt](../../hygiene/home.md): Lär dig grunderna om plattformens datahygien.
- [[!UICONTROL Data Hygiene] Användargränssnittsguide](../../hygiene/ui/overview.md): Lär dig schemalägga förfallodatum för datauppsättningar och förfrågningar om konsumentborttagning i användargränssnittet för plattformen.
- [API-guide för datahygien](../../hygiene/api/overview.md): Alla datahygienaktiviteter som du kan utföra i användargränssnittet kan också programmässigt

## [!UICONTROL Privacy Console] {#privacy-console}

The [!UICONTROL Privacy Console] i användargränssnittet för Experience Platform ger en översikt över viktiga insikter från sekretessrelaterade funktioner som [förfrågningar från registrerade från Privacy Servicen], [arbetsorder för datahygien]och [granskningsloggar]. Konsolen innehåller också flera handledningar för användning i produkten som hjälp att hantera vanliga sekretessarbetsflöden.

Se [Översikt över Integritetskonsolen](../../landing/governance-privacy-security/privacy-console.md) för mer information om funktionen.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML-tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa modeller som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskaplig expertis.

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktytor som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktyta för marknadsföring över kundresor.

| Funktion | Beskrivning |
| --- | --- |
| Spara utkastinstans | Med den här nya funktionen kan marknadsföringsanalytiker spara modellkonfigurationen som ett utkast under konfigurationer och fortsätta redigera utkastet tills det är klart innan utbildning och poängsättning. Scenarier där den här funktionen är användbar omfattar, men är inte begränsade till, när användare har flera fält att definiera i konfigurationsarbetsflödet som de inte kan slutföra på en gång eller när en eller flera datauppsättningsstatistik (som kolumnfullständighet) tar tid att bearbeta innan de blir tillgängliga. Läs [Användarhandbok för Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) om du vill veta mer. |
| Styrningspolitik | När användare har skickat in för att skapa en instans via konfigurationsarbetsflödet kontrollerar den nya tjänsten för regelefterlevnad om det finns några regelbrott för dataanvändningen och visar informationen i en port. Det ser till att dataåtgärder och marknadsföringsåtgärder är kompatibla med dataanvändningsprinciper som konfigurerats på Adobe Experience Platform. |

Mer information om Attribution AI finns i [Översikt över Attribution AI](../../intelligent-services/attribution-ai/overview.md). Mer information om policyer för datastyrning finns i [profiler, översikt](../../data-governance/policies/overview.md).

### Kund-AI

Customer AI available in Real-time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale.

| Funktion | Beskrivning |
| --- | --- |
| Spara utkastinstans | Med den här nya funktionen kan marknadsföringsanalytiker spara modellkonfigurationen som ett utkast under konfigurationer och fortsätta redigera utkastet tills det är klart innan utbildning och poängsättning. Scenarier där den här funktionen är användbar omfattar, men är inte begränsade till, när användare har flera fält att definiera i konfigurationsarbetsflödet som de inte kan slutföra på en gång eller när en eller flera datauppsättningsstatistik (som kolumnfullständighet) tar tid att bearbeta innan de blir tillgängliga. Läs [Användarhandbok för AI](../../intelligent-services/customer-ai/user-guide/configure.md) om du vill veta mer. |
| Styrningspolitik | När användare har skickat in för att skapa en instans via konfigurationsarbetsflödet kontrollerar den nya tjänsten för regelefterlevnad om det finns några regelbrott för dataanvändningen och visar informationen i en port. Det ser till att dataåtgärder och marknadsföringsåtgärder är kompatibla med dataanvändningsprinciper som konfigurerats på Adobe Experience Platform. |

Mer information om AI för kunder finns i [Översikt över AI för kunder](../../intelligent-services/customer-ai/overview.md). Mer information om policyer för datastyrning finns i [profiler, översikt](../../data-governance/policies/overview.md).

## Granskningsloggar {#audit-logs}

Med Experience Platform kan du granska användaraktivitet för olika tjänster och funktioner. Granskningsloggarna innehåller information om vem som gjorde vad och när.

**Uppdaterade funktioner**

| Funktion | Namn | Beskrivning |
| --- | --- | --- |
| Tillagda resurser | <ul><li>Attribution AI instans</li><li>AI-instans för kund</li><li>Datastream</li></ul> | Granskningsloggresurser registreras automatiskt när aktiviteten utförs. Om funktionen är aktiverad behöver du inte aktivera loggsamling manuellt. |

{style=&quot;table-layout:auto&quot;}

Mer information om de olika resursspecifika händelsetyperna som spåras av granskningsloggar i Platform finns i [granskningsloggar - översikt](../../landing/governance-privacy-security/audit-logs/overview.md).

## Datainsamling

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Integrering med vänster navigering i plattformsgränssnittet | Alla funktioner som tidigare var exklusiva för användargränssnittet för datainsamling (inklusive taggar, vidarebefordran av händelser och datastreams) är nu även tillgängliga via den vänstra navigeringen i Experience Platform, under kategorin **[!UICONTROL Data Collection]**. Detta eliminerar behovet av att växla mellan användargränssnitt när du arbetar med datainsamlingsfunktioner i Platform. |

{style=&quot;table-layout:auto&quot;}

Mer information om datainsamling i Platform finns i [datainsamling - översikt](../../collection/home.md).

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

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Identitetstjänst {#identity-service}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för borttagning av datauppsättningar | Identitetstjänsten har nu stöd för borttagning av datauppsättningar vid begäran via [Katalogtjänstens API](https://developer.adobe.com/experience-platform-apis/references/catalog/), användargränssnittet eller datahygien. Läs guiden på [ta bort datauppsättningar i användargränssnittet](../../catalog/datasets/user-guide.md#delete-a-dataset) för mer information. |

Mer information om identitetstjänsten finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Audience Manager segmentpopulationens påverkan på kundprofilen i realtid | Intag av stora Audience Manager-segmentpopulationer har en direkt inverkan på det totala antalet profiler när du för första gången skickar ett Audience Manager-segment till plattformen via Audience Manager. Det innebär att om du väljer alla segment kan det eventuellt leda till ett profilantal som överskrider licensanvändningsbehörigheten. Mer information finns i [Översikt över Audience Manager-källa](../../sources/connectors/adobe-applications/audience-manager.md). Mer information om licensanvändningen finns i dokumentationen om [med kontrollpanelen för licensanvändning](../../dashboards/guides/license-usage.md). |

Läs mer om källor i [källöversikt](../../sources/home.md).