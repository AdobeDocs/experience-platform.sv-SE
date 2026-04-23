---
title: Experience Cloud-målgrupper
description: Lär dig hur du delar målgrupper från Real-Time Customer Data Platform till olika Experience Cloud-appar.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 0%

---


# [!UICONTROL Experience Cloud Audiences]-anslutning

>[!AVAILABILITY]
>
> Det här målet är tillgängligt för [Adobe Real-Time Customer Data Platform Prime- och Ultimate](https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform.html)-kunder.

Använd det här målet för att aktivera målgrupper från [!DNL Real-Time CDP] till Audience Manager och [!DNL Adobe Analytics].

Du behöver en Audience Manager-licens för att kunna skicka målgrupper till [!DNL Adobe Analytics]. Mer information finns i översikten för [Audience Analytics](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=sv-SE).

Om du vill skicka målgrupper till andra Adobe-lösningar använder du direktanslutningarna från [!DNL Real-Time CDP] till [Adobe Target](../personalization/adobe-target-connection.md), [Adobe Advertising](../advertising/adobe-advertising-dsp-connection.md), [Adobe Campaign](../email-marketing/adobe-campaign.md) och [Marketo Engage](../adobe/marketo-engage.md).

>[!IMPORTANT]
>
>Det här målet ersätter den [gamla målgruppsdelningsintegreringen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=sv-SE#aep-segments-in-aam) från [!DNL Real-Time Customer Data Platform] till olika Experience Cloud-lösningar.
> 
>Om du redan delar målgrupper från [!DNL Real-Time CDP] till Audience Manager och andra Experience Cloud-lösningar via den [gamla målgruppsdelningsintegreringen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=sv-SE#aep-segments-in-aam) måste du kontakta kundtjänst för att inaktivera den gamla integreringen innan du kan använda den här målplatsen.

![Målet för Experience Cloud-målgrupper, markerat i målkatalogen.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## Användningsexempel och fördelar {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!UICONTROL Experience Cloud Audiences] finns det exempel på användningsområden som [!DNL Real-Time CDP]-kunder kan lösa genom att använda det här målet.

### Aktivera användningsfall för datahanteringsplattform {#dmp-use-cases}

I Audience Manager kan du använda [!DNL Real-Time CDP] målgrupper för datahanteringsplattformens användningsfall, till exempel:

* Lägger till [data från tredje part](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=sv-SE#third-party-data) till dina segment;
* [Algoritmisk modellering](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=sv-SE);
* Aktivera dina målgrupper för cookie-baserade mål som ännu inte stöds i [!DNL Real-Time CDP]-målkatalogen.

### Detaljerad kontroll över exporterade målgrupper {#segments-control}

Om du vill välja vilka målgrupper som ska exporteras till Audience Manager och andra målgrupper använder du den nya självbetjäningsintegreringen för målgruppsdelning via Experience Cloud målgruppsmål.  Använd detta för att avgöra vilka målgrupper du vill dela med andra Experience Cloud-lösningar och vilka målgrupper du vill behålla exklusivt i [!DNL Real-Time CDP].

Tack vare den gamla integreringen av målgruppsdelning gick det inte att styra vilka målgrupper som ska exporteras till Audience Manager och vidare.

### Dela [!DNL Real-Time CDP] målgrupper med [!DNL Adobe Analytics] {#share-audiences-with-analytics}

Publiker som du skickar till målplatsen för Experience Cloud-målgrupper visas inte automatiskt i [!DNL Adobe Analytics].

Innan du kan skicka målgrupper till [!DNL Adobe Analytics] måste du [implementera Experience Cloud Identity Service för Analytics och Audience Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=sv-SE).

>[!IMPORTANT]
>
>Du måste ha en Audience Manager-licens för att kunna skicka målgrupper från [!DNL Real-Time CDP] till [!DNL Adobe Analytics] via målgruppen för Experience Cloud-målgrupper.

### Dela [!DNL Real-Time CDP] målgrupper med andra Experience Cloud-lösningar {#share-segments-with-other-solutions}

Du kan använda målkortet [!DNL Real-Time CDP] för målgrupper om du vill dela målgrupper med andra Experience Cloud-lösningar.

Adobe rekommenderar dock att du använder följande dedikerade målkort om du vill dela målgrupper med dessa lösningar:

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Adobe Advertising DSP](../advertising/adobe-advertising-dsp-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## Förutsättningar {#prerequisites}

>[!IMPORTANT]
>
> * Du behöver en Audience Manager-licens för att kunna aktivera de [datahanteringsplattformens användningsfall](#dmp-use-cases) som nämns ovan.
> * Du *do* behöver en Audience Manager-licens för att dela [!DNL Real-Time CDP] målgrupper med [!DNL Adobe Analytics].
> * Du *behöver inte* någon Audience Manager-licens för att dela [!DNL Real-Time CDP] målgrupper med [!DNL Adobe Advertising], [!DNL Adobe Target], Marketo och andra Experience Cloud-lösningar som nämns i [avsnittet ovan](#share-segments-with-other-solutions).

### För kunder som använder den gamla målgruppslösningen {#legacy-audience-sharing}

Om du redan delar målgrupper från [!DNL Real-Time CDP] till Audience Manager och andra Experience Cloud-lösningar via den [gamla målgruppsdelningsintegreringen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=sv-SE#aep-segments-in-aam) måste du kontakta kundtjänst för att inaktivera den gamla integreringen.

Den tid det tar att lösa avprovisioneringsbiljetten är högst sex arbetsdagar. När den befintliga integreringen har inaktiverats kan du fortsätta med att [skapa en anslutning](#connect) via självbetjäningskortet.

>[!IMPORTANT]
>
>Publiken exporterar från [!DNL Real-Time CDP] till dina andra lösningar stoppas i tiden mellan matchningen av biljetten och den tidpunkt då en ny anslutning upprättas via målkortet. Du kan minimera den här driftstoppen genom att skapa anslutningen via målkortet när biljetten har stängts.

## Kända begränsningar och hänvisningar {#known-limitations}

Observera följande kända begränsningar och viktiga bildtexter när du använder Experience Cloud Audiences-kortet:

* För närvarande kan du konfigurera målplatsen för Experience Cloud-målgrupper på en enda sandlåda per organisation. Om du försöker konfigurera en andra målanslutning i en annan sandlåda uppstår ett fel.
* När du ansluter till målet kan du se ett alternativ för att [aktivera dataflödesaviseringar](../../ui/alerts.md). Även om alternativet **aktivera aviseringar visas i användargränssnittet stöds det inte för närvarande**.
* **Stöd för efterfyllnad av målgrupper**: Den första exporten till Audience Manager eller andra Experience Cloud-lösningar innehåller en historik över målgrupperna. Användare av den [äldre målgruppsdelningsintegreringen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=sv-SE#aep-segments-in-aam) som konfigurerar det här målet bör förvänta sig en återfyllningsdifferens på ungefär sex timmar.
* Publiker som kommer från [Målgruppskomposition](../../../segmentation/ui/audience-composition.md) stöds inte direkt. Om du vill aktivera sammansatta målgrupper för det här målet måste du skapa en målgruppsdefinition med [Segment Builder](../../../segmentation/ui/segment-builder.md) baserat på den sammansatta målgruppen och aktivera den nya målgruppen.

### Fördröjning vid aktivering av målgrupper {#audience-activation-latency}

Det finns en fyra timmars fördröjning mellan den tidpunkt då målgrupperna först aktiveras i [!DNL Real-Time CDP] och den tidpunkt då de är klara att användas i Audience Manager och andra Experience Cloud-lösningar.

Det kan ta upp till 24 timmar innan målgrupperna är fullt tillgängliga i Audience Manager för alla användningsfall. Det kan ta upp till 48 timmar för målgrupper från Experience Cloud-målgrupper att visas i Audience Manager-rapporter.

Metadata, till exempel målgruppsnamn, är tillgängliga i Audience Manager inom några minuter efter att du har konfigurerat exporten till Experience Cloud målgrupper.

## Identiteter som stöds {#supported-identities}

Profilerna som exporteras till målet [!UICONTROL Experience Cloud Audiences] mappas till de identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| ECID | EXPERIENCE CLOUD ID | Ett namnutrymme som representerar ECID. Detta namnområde kan också refereras till av följande alias: Adobe Marketing Cloud ID, [!DNL Adobe Experience Cloud] ID, [!DNL Adobe Experience Platform] ID. Mer information finns i följande dokument på [ECID](/help/identity-service/features/ecid.md). |
| GAID | GOOGLE ADVERTISING ID | Profiler som inhämtas till [!DNL Real-Time CDP] med en primär identitet för Google Advertising ID (GAID) kan exporteras till det här målet. |
| IDFA | Apple ID för annonsörer | Profiler som inhämtas till [!DNL Real-Time CDP] med en primär identitet för Apple ID för annonsörer (IDFA) kan exporteras till det här målet. |
| email_lc_sha256 | E-postadresser som hashas med SHA256-algoritmen | Profiler som inhämtas till [!DNL Real-Time CDP] med en primär identitet för hash-e-postadressen kan exporteras till det här målet. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupp du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Nej | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som har genererats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer], </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en publik som är märkta med identiteterna som listas i avsnittet ovan. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. När en profil uppdateras i [!DNL Real-Time CDP] baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedåt till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet väljer du **[!UICONTROL Set up]** i målkortsvyn i katalogen och väljer **[!UICONTROL Connect to destination]**.

![Vy över målalternativet Anslut till för Experience Cloud-målgrupper.](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Konfigurera en ny målskärm som visar de obligatoriska och valfria inställningarna för att ansluta till Experience Cloud-målgrupper.](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet. Inget [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) krävs och inget [schemaläggningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) är tillgängligt för det här målet.

## Validera dataexport {#exported-data}

För att validera dataexporten kan ni kontrollera att era målgrupper lyckats med exporten till er Experience Cloud-lösning.

### Validera data i Audience Manager {#validate-audience-manager}

Dina [!DNL Real-Time CDP]-målgrupper visas i Audience Manager som [signaler](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=sv-SE#aep-segments-as-aam-signals), [traits](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=sv-SE#aep-segments-as-aam-traits) och [segments](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=sv-SE#aep-segments-as-aam-segments). Du kan verifiera i Audience Manager om informationen har visats så som beskrivs i dokumentationslänkarna ovan.

Segmentnamn börjar fyllas i i Audience Manager 15 minuter efter att målgrupperna har skickats från [!DNL Real-Time CDP].

Segmentpopulationen börjar flöda in i Audience Manager inom 6 timmar från att ha skickats från [!DNL Real-Time CDP] och uppdateras var 24:e timme i Audience Manager.

Hela populationen visas i Audience Manager efter 72 timmar och populationerna fortsätter att flöda till Audience Manager om inte målgruppen tas bort från destinationen i [!DNL Real-Time CDP].

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Real-Time CDP]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

Datastyrning i [!DNL Real-Time CDP] används både av [dataanvändningsetiketter](/help/data-governance/labels/reference.md) och marknadsföringsåtgärder.
Dataanvändningsetiketter överförs till program men marknadsföringsåtgärder gör det inte. Det innebär att när de har landat i Audience Manager kan målgrupper från [!DNL Real-Time CDP] exporteras till alla tillgängliga destinationer. I Audience Manager kan du använda [dataexportkontroller](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=sv-SE) för att blockera målgrupper från att exporteras till vissa mål.

Publiker som har markerats med marknadsföringsåtgärden [!DNL HIPAA] skickas inte från [!DNL Real-Time CDP] till Audience Manager.

### Behörighetshantering i Audience Manager {#audience-manager-permissions}

Publiker och egenskaper i Audience Manager omfattas av [rollbaserade åtkomstkontroller](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=sv-SE) (RBAC).

Publiker som exporteras från [!DNL Real-Time CDP] tilldelas en specifik datakälla i Audience Manager som heter **[!UICONTROL Experience Platform Segments]**.

Om du bara vill ge vissa användare åtkomst till målgrupperna använder du [rollbaserade åtkomstkontroller](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=sv-SE) för att konfigurera användaråtkomst till målgrupper och egenskaper som skapats från [!DNL Real-Time CDP] målgrupper.
