---
title: Versionsinformation om Adobe Experience Platform från augusti 2022
description: Versionsinformation för augusti 2022 för Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1965'
ht-degree: 21%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 24 augusti 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML-tjänster ger marknadsföringsanalytiker och yrkesverksamma möjlighet att utnyttja artificiell intelligens och maskininlärning i kundupplevelsefall. På så sätt kan marknadsföringsanalytiker skapa modeller som är specifika för ett företags behov med hjälp av konfigurationer på företagsnivå utan behov av datavetenskap.

### Attribution AI

Attribution AI används för att attribuera krediter till kontaktpunkter som leder till konverteringshändelser. Detta kan användas av marknadsförare för att kvantifiera marknadsföringseffekten av varje enskild kontaktpunkt för marknadsföring över kundresor.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för sekretess | <ul><li> Attribution AI har nu stöd för att definiera användarroller och åtkomstprinciper för att hantera [behörigheter](../../../help/access-control/abac/ui/permissions.md) för funktioner och objekt i ett produktprogram. </li><li>Granskningsloggresurser registreras automatiskt när aktiviteten utförs.</li><li> Genom [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på vissa attribut, som kan läggas till i ett objekt, t.ex. etiketter. Administratörer kan också definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.</li><li>Attribution AI utnyttjar Experience Platform datamängder. För att ge stöd åt förfrågningar om konsumenträttigheter som ett varumärke kan ta emot, bör varumärken använda Experience Platform Privacy Service för att skicka in förfrågningar om åtkomst och radering från konsumenter för att ta bort deras data i datasjön, identitetstjänst och kundprofil i realtid.  </li><li>Alla datauppsättningar som används för in-/utdata av modeller följer Experience Platform riktlinjer. Experience Platform datakryptering gäller för data i vila och under överföring. Mer information om [datakryptering](../../../help/landing/governance-privacy-security/encryption.md) finns i dokumentationen.</li></ul> |

{style="table-layout:auto"}

**Obs!**: Attribution AI kommer inte att vara tillgängligt för befintliga kunder inom hälso- och sjukvårdsskölden förrän du får mer information.

Mer information om Attribution AI finns i översikten för [Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Kund-AI

Customer AI available in Real-Time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för sekretess | <ul><li> Kund-AI har nu stöd för att definiera användarroller och åtkomstprinciper för att hantera [behörigheter](../../../help/access-control/abac/ui/permissions.md) för funktioner och objekt i ett produktprogram. </li><li>Granskningsloggresurser registreras automatiskt när aktiviteten utförs.</li><li> Genom [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på vissa attribut. Dessa attribut kan läggas till i ett objekt, till exempel etiketter. Administratörer kan också definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.</li><li>Kund-AI använder Experience Platform datamängder. För att ge stöd åt förfrågningar om konsumenträttigheter som ett varumärke kan ta emot, bör varumärken använda Experience Platform Privacy Service för att skicka in förfrågningar om åtkomst och radering från konsumenter för att ta bort deras data i datasjön, identitetstjänst och kundprofil i realtid. </li><li>Alla datauppsättningar som används för in-/utdata av modeller följer Experience Platform riktlinjer. Experience Platform datakryptering gäller för data i vila och under överföring. Mer information om [datakryptering](../../../help/landing/governance-privacy-security/encryption.md) finns i dokumentationen.</li></ul> |

{style="table-layout:auto"}

**Obs!** Kundens AI kommer inte att vara tillgängligt för befintliga kunder inom hälso- och sjukvårdsskölden förrän ytterligare information skickas.

Mer information om kundens AI finns i översikten över [kundens AI](../../intelligent-services/customer-ai/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform tillhandahåller flera [!DNL dashboards] som du kan använda för att visa viktiga insikter om organisationens data, som de har fångats in under dagliga ögonblicksbilder.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Widget för schemalagda aktiveringar | Widgeten [!UICONTROL Scheduled activations] innehåller en tabellvy över de senast aktiverade målplatserna. För varje segment innehåller det namn, målplattform samt start- och slutdatum för aktiveringen. Med den här widgeten kan du snabbt identifiera var och när målgruppen aktiveras och göra duplicerade eller onödiga aktiveringar mer transparenta. Den samlade informationen visar också var aktiveringar har utelämnats. |

Mer information om [!DNL Dashboards] finns i [[!DNL Dashboards] översikten](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för inmatning av poster med varningar | Dataprep lokaliserar nu varningar (icke-kritiska fel) till fälten och tillåter att resten av raden importeras. Alla mappningsomformningsfel rapporteras nu som varningar och rader som är delvis inkapslade betraktas som lyckade, med en varning.  Övervakning stöds även för poster med varningar och diagnostikinformation. Det går för närvarande bara att få del av poster med varningar att strömma data. Mer information finns i dokumentationen om [hur poster hämtas med varningar](../../sources/tutorials/ui/monitor-streaming.md). |

{style="table-layout:auto"}

Mer information om [!DNL Data Prep] finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| (Beta) Attributbaserat personaliseringsstöd för personaliseringsmål | I betaversionen av attributbaserad personalisering visas två nya kort i [målkatalogen](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: Den här kopplingen är för närvarande i betaversion och endast tillgänglig för ett visst antal kunder. Utöver de funktioner som finns på Adobe Target V1-kortet lägger Target V2-anslutningen till ett [mappningssteg](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) i aktiveringsarbetsflödet, vilket gör att du kan mappa profilattribut till Adobe Target, vilket möjliggör attributbaserad anpassning på samma sida och nästa sida.</li><li>**[!UICONTROL Custom Personalization With Attributes]**: Den här kopplingen är för närvarande i betaversion och endast tillgänglig för ett visst antal kunder. Utöver de funktioner som tillhandahålls av **[!UICONTROL Custom Personalization]** lägger **[!UICONTROL Custom Personalization With Attributes]**-kopplingen till ett valfritt [mappningssteg](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes) i aktiveringsarbetsflödet, vilket gör att du kan mappa profilattribut till ditt anpassade anpassningsmål, vilket möjliggör attributbaserad anpassning på samma sida och nästa sida.</li></ul> <br> profilattribut kan innehålla känsliga data. För att skydda dessa data kräver **[!UICONTROL Custom Personalization With Attributes]**-målet att du använder [ Edge Network Server-API ](../../server-api/overview.md) för datainsamling. Dessutom måste alla Server-API-anrop göras i en [autentiserad kontext](../../server-api/authentication.md). |

{style="table-layout:auto"}

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) är en Experience Platform för försäljningskörning med de flesta interaktionsdata för B2B-köpare i världen och betydande investeringar i egna AI-tekniker för att omvandla säljdata till intelligens. [!DNL Outreach] hjälper organisationer att automatisera säljengagemanget och agera på intäktsanalys för att förbättra deras effektivitet, förutsägbarhet och tillväxt. |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en specifikation med öppen källkod som tillhandahåller gemensamma strukturer och definitioner (scheman) för data som förs in i Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Klass | [[!UICONTROL AJO Entity Class]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-class.schema.json) | En postbaserad klass för att skapa uppslagsscheman för Adobe Journey Optimizer. |
| Fältgrupp | [[!UICONTROL Workfront Work Objects]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | En omslutningsfältgrupp som refererar till alla objektspecifika fältgrupper på den lägre nivån för Adobe Workfront. |

{style="table-layout:auto"}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Två nya egenskaper har lagts till: `origTimeStamp` och `experienceID`. |
| Fältgrupp | [[!UICONTROL Segment Membership Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Förutom [!UICONTROL XDM Individual Profile] kan den här fältgruppen nu även användas i scheman baserat på klassen XDM Business Account. |
| Fältgrupp | (Flera) | Flera fältgrupper som rör Marketo B2B-aktiviteter har uppdaterats till stabil status. Mer information finns i följande [pull-begäran](https://github.com/adobe/xdm/pull/1593/files). |
| Fältgrupp | (Flera) | Flera väderrelaterade fältgrupper har uppdaterats för att åtgärda fel som uppstod för `uvIndex` och `sunsetTime`. Mer information finns i följande [pull-begäran](https://github.com/adobe/xdm/pull/1602/files). |
| Datatyp | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | En ny egenskap `productImageUrl` har lagts till. |
| Datatyp | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | En ny egenskap `framesPerSecond` har lagts till. |
| Datatyp | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` har bytt namn till `appVersion`. `meta:enum` och `description` fält har också uppdaterats. |
| Datatyper och fältgrupper | (Flera) | Flera mediedatatyper och fältgrupper har nya fält och uppdaterade beskrivningar. Mer information finns i följande [pull-begäran](https://github.com/adobe/xdm/pull/1582/files). |
| (Alla) | (Flera) | Alla schemaobjekt som innehåller ett `enum`-fält innehåller nu även motsvarande `meta:enum`-fält som anger visningsvärden för varje begränsning. Mer information finns i följande [pull-begäran](https://github.com/adobe/xdm/pull/1601/files). |

{style="table-layout:auto"}

Mer information om XDM i Experience Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med profilen kan du konsolidera kunddata till en enhetlig vy som ger en handlingsbar, tidsstämplad redogörelse för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Hög gräns för sammanslagningsprinciper | Experience Platform tillämpar nu en hård gräns på **fem** sammanslagningsprinciper per per sandlåda. Om din sandlåda har fler än fem sammanfogningsprinciper kan du **inte** skapa nya sammanfogningsprinciper tills sandlådan har färre än fem sammanfogningsprinciper. |
| Rensning av kanter för överblivna profiler | För alla organisationer tar nu profiltjänsten bort vänsterkantsattribut i användaraktivitetsområdet dagligen för att ge en mer korrekt återgivning av dina profiler i systemet. Den här rensningen sker efter att alla profilfragment för en viss profil har tagits bort och påverkar profiler som sammanfogas från datauppsättningar där `com_adobe_aep_profile_region_dataset` har markerats som `true`. Detta kan visa en minskning av&quot;adresserbar målgrupp&quot;-måttet på kontrollpanelen för licensanvändning och kan visa en minskning i &quot;profilräknaren&quot; i profilkontrollpanelen, eftersom dessa mått inkluderade attributfragment med vänsterkant före den här versionen. |

{style="table-layout:auto"}

Om du vill veta mer om kundprofilen i realtid, inklusive självstudiekurser och bästa praxis för arbete med profildata, börjar du med att läsa [Översikt över kundprofilen i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Segmenten kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för 4 000 segment | Alla organisationer med Experience Platform har nu stöd för upp till 4 000 segmentdefinitioner. Mer information om hur den här ändringen påverkar API:erna för segmentjobb finns i [slutpunktshandboken för segmentjobb](../../segmentation/api/segment-jobs.md) |

Mer information om [!DNL Segmentation Service] finns i [segmenteringsöversikten](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för självbetjäningskällor (Batch SDK) | Utveckla, testa och integrera REST API-baserade datakällor för att importera batchdata till Experience Platform med hjälp av lättkonfigurerade källspecifikationer. Med Sources SDK kan man <ul><li>Konfigurera en ny källa till Experience Platform-katalogen.</li><li>Definiera specifikationer för källan, inklusive information om vilka autentiseringstyper som stöds, schemaläggning och hur resursdata hämtas.</li><li>Skapa användarinriktad dokumentation för den nya källan.</li></ul> Mer information finns i dokumentationen om [självbetjäningskällor (Batch SDK)](../../sources/sources-sdk/overview.md). |
| Allmän tillgänglighet för källan [!DNL Google BigQuery] | Använd [!DNL Google BigQuery]-källan för att importera data från ditt [!DNL Google BigQuery]-datalager till Experience Platform. Mer information finns i dokumentationen för [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] källa (Beta) | Använd källan [!DNL Teradata Vantage] för att importera data från hybridmiljöer med flera moln till Experience Platform. Mer information finns i dokumentationen för [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Stöd för olika regioner för Adobe Analytics | Du kan nu importera rapportsviter från valfri region (USA, Storbritannien eller Singapore). Rapportsviter måste mappas till samma organisation som den Experience Platform Sandbox-instans i vilken källanslutningen skapas. Mer information finns i guiden om att [skapa en Adobe Analytics-källanslutning i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Mer information om källor finns i [Källöversikt](../../sources/home.md).
