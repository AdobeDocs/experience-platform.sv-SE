---
title: (Beta) Experience Cloud Publiker
description: Lär dig hur du delar segment från Experience Platform till olika Experience Platform-lösningar.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 017c8bbc19845c0f60040ba2995b5dd2b0299a8b
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 0%

---

# (Beta) [!UICONTROL Experience Cloud Audiences] anslutning

Med den här målplatsen kan ni dela segment från Experience Platform till olika Experience Cloud-lösningar, som Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target eller Marketo.

![Experience Cloud-målgruppsmålet, som är markerat i målkatalogen.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* Detta mål ersätter [integrering av äldre segmentdelning](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) från Experience Platform till olika lösningar för Experience Cloud.
>* Detta mål är för närvarande i betaversion. Dokumentationen och funktionerna kan komma att ändras.


## Användningsexempel och fördelar {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!UICONTROL Experience Cloud Audiences] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Aktivera användningsfall för datahanteringsplattform {#dmp-use-cases}

I Audience Manager kan du använda Experience Platform-segment för datahanteringsplattformens användningsfall, till exempel:

* Lägg till [data från tredje part](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) till era segment,
* [Algoritmisk modellering](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Aktivera dina segment till cookie-baserade mål som ännu inte stöds i Experience Platform-målkatalogen.

### Detaljerad kontroll över exporterade segment {#segments-control}

Använd den nya integreringen av segmentdelning via Experience Cloud för att välja vilka segment som ska exporteras till Audience Manager och utanför. På så sätt kan du avgöra vilka segment du vill dela med andra Experience Cloud-lösningar och vilka segment du vill behålla exklusivt i Experience Platform.

Integreringen av den gamla segmentdelningen gjorde att det inte gick att styra vilka segment som skulle exporteras till Audience Manager och vidare.

### Dela segment i Experience Platform med ytterligare lösningar för Experience Cloud {#share-segments-with-other-solutions}

Förutom att dela segment med Audience Manager kan du med målkortet för målgruppen Experience Platform-målgrupper dela segment med andra Experience Cloud som du har provisionerat för, till exempel:

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics 
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## Förutsättningar {#prerequisites}

>[!IMPORTANT]
>
> * Det här målet är tillgängligt för [Adobe Real-time Customer Data Platform Prime och Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) kunder.
> * Du behöver en Audience Manager-licens för att kunna aktivera [Användningsexempel för datahanteringsplattform](#dmp-use-cases) som nämns ovan.
> * Du *behöver inte* en Audience Manager-licens för att dela Experience Platform-segment med Adobe Advertising Cloud, Adobe Target, Marketo och andra Experience Cloud-lösningar som nämns i [avsnitt ovan](#share-segments-with-other-solutions).


### För kunder som använder den gamla segmentdelningslösningen

Om ni redan delar segment från Experience Platform till Audience Manager och andra Experience Cloud-lösningar via [integrering av äldre segmentdelning](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)måste du kontakta antingen kundtjänst eller ditt Adobe-kontoteam för att inaktivera integreringen. Kundtjänst- och Adobe-kontoteam måste registrera en Jira-biljett (se mallbiljett AAM-52354) för att inaktivera integreringen.

Den tid det tar att lösa avprovisioneringsbiljetten för betakunder är sex arbetsdagar eller mindre. När den befintliga integreringen har inaktiverats kan du fortsätta till [skapa en anslutning](#connect) via självbetjäningskortet.

>[!IMPORTANT]
>
>Segmentexporten från Experience Platform till dina andra lösningar stoppas i tiden mellan Jiras biljettlösning och den tidpunkt då en ny anslutning upprättas via målkortet. Du kan minimera den här driftstoppen genom att skapa anslutningen via målkortet så snart Jira-biljetten stängs.

## Kända begränsningar och hänvisningar {#known-limitations}

Observera följande kända begränsningar och viktiga hänvisningar i betaversionen av Publikationskortet i Experience Cloud:

* [Dataflödesövervakning](/help/dataflows/ui/monitor-destinations.md) stöds inte.
* När du ansluter till målet kan du se ett alternativ för att [aktivera dataflödesaviseringar](#enable-alerts). Visas i användargränssnittet, men **alternativet aktivera aviseringar stöds inte** i betaversionen.
* **Backfills stöds inte**. Den första exporten till Audience Manager eller andra lösningar från Experience Cloud omfattar inte en historisk population av segmenten.
* I betaversionen kan du skapa **en enda målanslutning till målgruppen Experience Cloud**, i alla sandlådor som tillhör din Experience Platform-organisation.

### Latens vid aktivering av målgrupper {#audience-activation-latency}

Det finns fyra timmars fördröjning mellan den tidpunkt då målgrupperna först aktiveras i Experience Platform och den tidpunkt då de är klara att användas i Audience Manager och andra Experience Cloud-lösningar för vissa användningsfall.

Det kan ta upp till 24 timmar för målgrupper att vara fullt tillgängliga i Audience Manager för alla användningsfall och upp till 48 timmar för målgrupper från Experience Cloud att visas i Audience Manager-rapporter.

Metadata, till exempel segmentnamn, är tillgängliga i Audience Manager inom några minuter efter att du har konfigurerat exporten till målgruppen Experience Cloud.

## Identiteter som stöds {#supported-identities}

De profiler som exporteras till [!UICONTROL Experience Cloud Audiences] målet mappas till de identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| ECID | Experience Cloud ID | Ett namnutrymme som representerar ECID. Detta namnutrymme kan även refereras till av följande alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Se följande dokument på [ECID](/help/identity-service/ecid.md) för mer information. |
| GAID | Google Advertising ID | Profiler som inhämtas till Experience Platform med en primär identitet för Google Advertising ID (GAID) kan exporteras till det här målet. |
| IDFA | Apple ID för annonsörer | Profiler som inhämtas till Experience Platform med den primära identiteten Apple ID for Advertisers (IDFA) kan exporteras till den här destinationen. |
| email_lc_sha256 | E-postadresser som hash-kodats med SHA256-algoritmen | Profiler som inhämtas till Experience Platform med en primär identitet för hash-e-postadresser kan exporteras till det här målet. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) som är märkta med identiteterna som listas i avsnittet ovan. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

>[!IMPORTANT]
> 
>I betaversionen kan du skapa en enda målanslutning till målplatsen Experience Cloud, i alla sandlådor som tillhör din Experience Platform-organisation.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet väljer du **[!UICONTROL Set up]** i målkortsvyn i katalogen och välj **[!UICONTROL Connect to destination]**.

![Vy över målalternativet Anslut till för målplatsen Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Konfigurera en ny målskärm med de obligatoriska och valfria inställningarna för att ansluta till målplatsen Experience Cloud.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.


## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet. Observera att nej [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) krävs och nej [planeringssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) är tillgängligt för det här målet.

## Validera dataexport {#exported-data}

Om du vill validera dataexporten kan du kontrollera att era segment har lyckats med exporten till den önskade Experience Cloud-lösningen.

### Validera data i Audience Manager

Dina Experience Platform-segment visas i Audience Manager som [signaler](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [traits](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)och [segment](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). Du kan kontrollera i Audience Manager om data har visats enligt anvisningarna i dokumentationslänkarna ovan.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](/help/data-governance/home.md).

Datastyrning i Experience Platform genomförs av båda [etiketter för dataanvändning](/help/data-governance/labels/reference.md) och marknadsföringsåtgärder.
Dataanvändningsetiketter överförs till program, men marknadsföringsåtgärder kommer inte att göra det. Det innebär att när de landar i Audience Manager kan segment från Experience Platform exporteras till alla tillgängliga destinationer. I Audience Manager kan du använda [dataexportkontroller](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) om du vill blockera segment från att exporteras till vissa mål.

### Behörighetshantering i Audience Manager

Segment och egenskaper i Audience Manager omfattas av [Rollbaserade åtkomstkontroller](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=en) (RBAC).

Segment som exporteras från Experience Platform tilldelas en specifik datakälla i Audience Manager som kallas **[!UICONTROL Experience Platform Segments]**.

Om du bara vill ge vissa användare åtkomst till segmenten kan du använda åtkomstkontroller för de segment som tillhör datakällan. Du måste ange nya behörigheter för åtkomstkontroll i Audience Manager för de här segmenten och egenskaperna som skapas från Experience Platform-segmenten.
