---
title: Experience Platform Pre-Release Notes
description: En förhandsgranskning av den senaste versionsinformationen för Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: a26ad18b1e44b3198db9e8a36ad3749ed8a0afa2
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 37%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: augusti 2025**

Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Aviseringar](#alerts)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Aviseringar om strömning av genomströmningskapacitet | Med tre nya larm kan användare abonnera på och konfigurera aviseringar för att proaktivt hantera och övervaka prestanda för strömningskapacitet. Nya varningsmeddelanden kan vara när strömningsflödet har nått 80 %, 90 % eller överstiger kapacitetsgränserna. Mer information finns i guiden [kapacitetsvarningsregler](../observability/alerts/rules.md#capacity). |

Mer information om aviseringar finns i avsnittet [[!DNL Observability Insights] översikt](../observability/home.md).

## Mål {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya destinationer**

| Mål | Beskrivning |
| --- | --- |
| [!DNL Acxiom Real ID Audience] mål | Använd målet [!DNL Acxiom Real ID Audience Connection] för att förbättra målgrupper med tekniken [!DNL Acxiom's] [Real ID™](https://www.acxiom.com/real-id/real-id/) och aktivera målgrupper på flera plattformar, till exempel [!DNL Altice], [!DNL Ampersand], [!DNL Comcast]. |


**Uppdaterade mål**

| Mål | Beskrivning |
| --- | --- |
| Information om förfallodatum för autentisering för [!DNL LinkedIn] mål | Du behöver aldrig bekymra dig om utgångna autentiseringsuppgifter igen. Information om förfallodatum för kontot visas nu direkt i Experience Platform-gränssnittet, så du kan se när din [!DNL LinkedIn]-autentisering kommer att upphöra och förnya den innan den orsakar eventuella avbrott i dataflödena. |
| Krypteringsstöd för [!DNL Data Landing Zone] mål | Skydda exporterade data med kryptering. Nu kan du bifoga RSA-formaterade offentliga nycklar för att kryptera dina exporterade filer, vilket ger dig samma säkerhetsnivå som andra molnlagringsplatser tillhandahåller för din känsliga information. |
| [[!DNL Microsoft Bing]](../destinations/catalog/advertising/bing.md) intern uppgradering | Från och med 11 augusti 2025 kan du se två **[!DNL Microsoft Bing]**-kort sida vid sida i målkatalogen. Det här beror på en intern uppgradering av måltjänsten. Den befintliga målanslutningen **[!DNL Microsoft Bing]** har bytt namn till **[!UICONTROL (Deprecated) Microsoft Bing]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL Microsoft Bing]**. Använd den nya anslutningen **[!UICONTROL Microsoft Bing]** i katalogen för nya aktiveringsdataflöden. Om du har aktiva dataflöden till målet **[!UICONTROL (Deprecated) Microsoft Bing]** uppdateras de automatiskt. Du behöver därför inte göra något. <br><br> Om du skapar dataflöden via [Flow Service API:et](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden:<ul><li>Flödesspecifikation-id: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Anslutningsspecifikation-id: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Efter den här uppgraderingen kan det hända att antalet aktiverade profiler **i dina dataflöden minskar till**. [!DNL Microsoft Bing] Den här släppningen orsakas av introduktionen av **ECID-mappningskravet** för alla aktiveringar till den här målplattformen. |
| Ytterligare identifierare för [!DNL Amazon Ads] mål | Amazon Ads-målet har nu stöd för nya identiteter (`firstName`, `lastName`, `street`, `city`, `state`, `zip`, `country`). Dessa fält är avsedda att förbättra målgruppsmatchningen och skickas som oformaterad text med SHA256-hash som tillval. |
| Konsolidering av [!DNL Marketo] målkort | Förenkla målinställningen för [!DNL Marketo] med vårt enhetliga målkort. Vi har konsoliderat [!DNL Marketo] V2- och V3-kort till ett enda smidigt alternativ, vilket gör det enklare att välja rätt mål och komma igång snabbt. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Utöka datauppsättningsexportscheman för dataflöden som skapats före november 2024 | Om dataflödena för dataexport har skapats före november 2024 kommer dessa dataflöden att sluta fungera den 1 september 2025. Om du behöver dataflödena för att kunna fortsätta exportera data efter 1 september 2025 måste du utöka deras scheman för varje mål som du exporterar datauppsättningar till genom att följa stegen i [den här handboken](../destinations/ui/dataset-expiration-update.md). |
| Förbättrade funktioner för sökning, filtrering och taggning för destinationer | Förbättra arbetsflödet för målhantering med förbättrade funktioner för sökning, filtrering och taggning på flikarna Bläddra och Konton. Nu kan du söka efter specifika dataflöden och konton efter namn, filtrera efter olika villkor, inklusive målplattform, status och datum, och skapa anpassade taggar för att ordna dina mål. Kolumnsortering är också tillgängligt för nyckelfält som körningstid för senaste dataflöde, vilket gör det enklare att identifiera och hantera målanslutningarna. |

Mer information finns i [översikten över destinationer](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Modellbaserade scheman | Förenkla datamodelleringen med modellbaserade scheman. Nu kan du skapa scheman enklare med omfattande instruktionsexempel och vägledning. Den här funktionen är för närvarande tillgänglig för innehavare av Campaign Orchestration-licenser och kommer att utvidgas till att omfatta Data Distiller-kunder på GA, vilket gör datamodelleringen mer tillgänglig och effektiv. |

Mer information finns i [XDM-översikten](../xdm/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Målgruppsuppskattningar | Målgruppsuppskattningar genereras nu automatiskt i Segment Builder. Värdet uppdateras varje gång du ändrar målgruppen och speglar alltid de senaste målgruppsreglerna. |

Mer information finns i [[!DNL Segmentation Service] översikten](../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| [!BADGE Stöd för Azure Private Link i Beta]{type=Informative} i användargränssnittet | Skydda dina data med privata nätverksanslutningar. Nu kan du skapa privata slutpunkter och konfigurera dataflöden som kringgår det allmänna Internet, vilket ger dig förbättrad säkerhet och nätverksisolering för dina känsliga data. |
| [!DNL Marketo] dokumentationsuppdateringar | Få fullständig synlighet i hur dina [!DNL Marketo]-data omvandlas när de kommer in i Experience Platform. Alla fältmappningar innehåller nu detaljerade förklaringar av dataomvandlingar, så att du kan förstå exakt hur `PersonID` blir `leadID` och `eventType` blir `activityType`. |
| Stöd för huvudautentisering av tjänst för [!DNL Azure Blob Storage] | Du kan nu ansluta ditt [!DNL Azure Blob Storage]-konto till Experience Platform med autentisering av tjänstens huvudnamn. |

Mer information finns i [översikten över källor](../sources/home.md).

<!--

## Query Service {#query-service}

Adobe Experience Platform Query Service provides a robust SQL interface for data analysis and exploration across the platform.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Data Distiller Session Management | Take control of your data analysis sessions with enhanced session management. You can now monitor and manage your sessions more effectively across development and production environments, giving you better visibility into your query performance and resource usage. |

For more information, read the [Query Service overview](../query-service/home.md).

## B2B CDP {#b2b-cdp}

Real-Time CDP B2B Edition provides comprehensive B2B customer data management capabilities, enabling organizations to build unified customer profiles, create sophisticated B2B audiences, and activate data across various marketing channels.

**New or updated features**

| Feature | Description |
| ------- | ----------- |
| Lookup Support for B2B Classes Only | Streamline your B2B data access with focused lookup support. You can now look up Person (Profile), Experience Events, Account, and Opportunity entities directly through the Entities API. This simplified approach helps you access the most important B2B data more efficiently while reducing complexity. |
| B2B Namespace and Schema Updates | Experience a cleaner, more streamlined B2B data model. We've simplified the B2B namespace and schema structure by removing complex relationship mappings and non-primary identity support for certain B2B classes. This makes your B2B data easier to work with and understand. |

For more information, read the [Real-Time CDP B2B Edition overview](../rtcdp/b2b-overview.md).

-->
