---
title: Versionsinformation om Adobe Experience Platform, augusti 2022
description: Versionsinformation från augusti 2022 för Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: 3069bdb3592ac1cd3fd7fe4f7f9234d5be56547d
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 3%

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
| Stöd för sekretess | <ul><li> Attribution AI har nu stöd för att definiera användarroller och åtkomstprinciper för att hantera [behörigheter](../../../help/access-control/abac/ui/permissions.md) för funktioner och objekt i ett produktprogram. </li><li>Granskningsloggresurser registreras automatiskt när aktiviteten utförs.</li><li> Genom [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på vissa attribut, som kan läggas till i ett objekt, t.ex. etiketter. Administratörer kan också definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.</li><li>Attribution AI utnyttjar plattformsdatauppsättningar. För att ge stöd åt konsumenträttigheter som ett varumärke kan ta emot bör varumärken använda Platform Privacy Service för att skicka in förfrågningar från konsumenter om åtkomst och radering för att ta bort sina data över datasjön, identitetstjänst och kundprofil i realtid.  </li><li>Alla datauppsättningar som används för in-/utdata av modeller följer riktlinjerna för plattformen. Plattformsdatakryptering gäller för data i vila och under överföring. Mer information om [datakryptering](../../../help/landing/governance-privacy-security/encryption.md) finns i dokumentationen.</li></ul> |

{style="table-layout:auto"}

**Obs!**: Attribution AI kommer inte att vara tillgänglig för befintliga kunder inom hälso- och sjukvårdsskölden förrän du får mer information.

Mer information om Attribution AI finns i översikten för [Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Kund-AI

Customer AI available in Real-time Customer Data Platform, is used to generate custom bensipensity scores such as churn and conversion for individual profiles at scale.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för sekretess | <ul><li> Kund-AI har nu stöd för att definiera användarroller och åtkomstprinciper för att hantera [behörigheter](../../../help/access-control/abac/ui/permissions.md) för funktioner och objekt i ett produktprogram. </li><li>Granskningsloggresurser registreras automatiskt när aktiviteten utförs.</li><li> Genom [attributbaserad åtkomstkontroll](../../access-control/abac/overview.md) kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på vissa attribut. Dessa attribut kan läggas till i ett objekt, till exempel etiketter. Administratörer kan också definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.</li><li>Kund-AI utnyttjar plattformsdatauppsättningar. För att ge stöd åt konsumenträttigheter som ett varumärke kan ta emot bör varumärken använda Platform Privacy Service för att skicka in förfrågningar från konsumenter om åtkomst och radering för att ta bort sina data över datasjön, identitetstjänst och kundprofil i realtid. </li><li>Alla datauppsättningar som används för in-/utdata av modeller följer riktlinjerna för plattformen. Plattformsdatakryptering gäller för data i vila och under överföring. Mer information om [datakryptering](../../../help/landing/governance-privacy-security/encryption.md) finns i dokumentationen.</li></ul> |

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

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| (Beta) Attributbaserat personaliseringsstöd för personaliseringsmål | I betaversionen av attributbaserad personalisering visas två nya kort i [målkatalogen](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: Den här kopplingen är för närvarande i betaversion och endast tillgänglig för ett visst antal kunder. Utöver de funktioner som finns på Adobe Target V1-kortet lägger Target V2-anslutningen till ett [mappningssteg](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) i aktiveringsarbetsflödet, vilket gör att du kan mappa profilattribut till Adobe Target, vilket möjliggör attributbaserad anpassning på samma sida och nästa sida.</li><li>**[!UICONTROL Custom Personalization With Attributes]**: Den här kopplingen är för närvarande i betaversion och endast tillgänglig för ett visst antal kunder. Utöver de funktioner som tillhandahålls av **[!UICONTROL Custom Personalization]** lägger **[!UICONTROL Custom Personalization With Attributes]**-kopplingen till ett valfritt [mappningssteg](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes) i aktiveringsarbetsflödet, vilket gör att du kan mappa profilattribut till ditt anpassade anpassningsmål, vilket möjliggör attributbaserad anpassning på samma sida och nästa sida.</li></ul> <br> profilattribut kan innehålla känsliga data. För att skydda dessa data kräver **[!UICONTROL Custom Personalization With Attributes]**-målet att du använder [Edge Network Server-API](../../server-api/overview.md) för datainsamling. Dessutom måste alla Server-API-anrop göras i en [autentiserad kontext](../../server-api/authentication.md). |

{style="table-layout:auto"}

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) är en plattform för Försäljningskörning med de flesta interaktionsdata för B2B-köpare i världen och betydande investeringar i egna AI-tekniker för att omvandla säljdata till intelligens. [!DNL Outreach] hjälper organisationer att automatisera säljengagemanget och agera på intäktsanalys för att förbättra deras effektivitet, förutsägbarhet och tillväxt. |

{style="table-layout:auto"}

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

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

Mer information om XDM i Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Hög gräns för sammanslagningsprinciper | Plattformen tillämpar nu en hård gräns på **fem** sammanslagningsprinciper per per sandlåda. Om din sandlåda har fler än fem sammanfogningsprinciper kan du **inte** skapa nya sammanfogningsprinciper tills sandlådan har färre än fem sammanfogningsprinciper. |
| Rensning av kanter för överblivna profiler | För alla organisationer tar nu profiltjänsten bort vänsterkantsattribut i användaraktivitetsområdet dagligen för att ge en mer korrekt återgivning av dina profiler i systemet. Den här rensningen sker efter att alla profilfragment för en viss profil har tagits bort och påverkar profiler som sammanfogas från datauppsättningar där `com_adobe_aep_profile_region_dataset` har markerats som `true`. Detta kan visa en minskning av&quot;adresserbar målgrupp&quot;-måttet på kontrollpanelen för licensanvändning och kan visa en minskning i &quot;profilräknaren&quot; i profilkontrollpanelen, eftersom dessa mått inkluderade attributfragment med vänsterkant före den här versionen. |

{style="table-layout:auto"}

Om du vill veta mer om kundprofilen i realtid, inklusive självstudiekurser och bästa praxis för arbete med profildata, börjar du med att läsa [Översikt över kundprofilen i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

[!DNL Segmentation Service] definierar en viss delmängd av profiler genom att beskriva kriterierna som särskiljer en marknadsföringsbar grupp av personer inom din kundbas. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Stöd för 4 000 segment | Alla organisationer med Platform har nu stöd för upp till 4 000 segmentdefinitioner. Mer information om hur den här ändringen påverkar API:erna för segmentjobb finns i [slutpunktshandboken för segmentjobb](../../segmentation/api/segment-jobs.md) |

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för självbetjäningskällor (batch-SDK) | Utveckla, testa och integrera REST API-baserade datakällor för att importera batchdata till Experience Platform med hjälp av lättkonfigurerade källspecifikationer. Med Sources SDK kan du: <ul><li>Konfigurera en ny källa till Experience Platform-katalogen.</li><li>Definiera specifikationer för källan, inklusive information om vilka autentiseringstyper som stöds, schemaläggning och hur resursdata hämtas.</li><li>Skapa användarinriktad dokumentation för den nya källan.</li></ul> Mer information finns i dokumentationen om [självbetjäningskällor (batch-SDK)](../../sources/sources-sdk/overview.md). |
| Allmän tillgänglighet för källan [!DNL Google BigQuery] | Använd [!DNL Google BigQuery]-källan för att importera data från ditt [!DNL Google BigQuery]-datalager till Experience Platform. Mer information finns i dokumentationen för [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] källa (Beta) | Använd [!DNL Teradata Vantage]-källan för att importera data från hybridmiljöer med flera moln till Experience Platform. Mer information finns i dokumentationen för [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Stöd för olika regioner för Adobe Analytics | Du kan nu importera rapportsviter från valfri region (USA, Storbritannien eller Singapore). Rapportsviterna måste mappas till samma organisation som den Experience Platform Sandbox-instans i vilken källanslutningen skapas. Mer information finns i guiden om att [skapa en Adobe Analytics-källanslutning i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Mer information om källor finns i [Källöversikt](../../sources/home.md).
