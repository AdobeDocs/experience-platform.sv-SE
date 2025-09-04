---
title: Versionsinformation om Adobe Experience Platform för augusti 2025
description: Versionsinformation för augusti 2025 för Adobe Experience Platform.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 91%

---

# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 19 augusti 2025**


Nya funktioner och uppdateringar i Adobe Experience Platform:

- [Aviseringar](#alerts)
- [Katalogtjänst](#catalog-service)
- [Mål](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Aviseringar om strömning av genomströmningskapacitet | Med tre nya aviseringar kan användare prenumerera på och konfigurera aviseringar för att proaktivt hantera och övervaka prestanda för strömningskapacitet. Nya aviseringsmeddelanden innefattar när strömningsflödet har nått 80 %, 90 % eller överstiger kapacitetsgränserna. Mer information finns i guiden [Regler för kapacitetsaviseringar](../../observability/alerts/rules.md#capacity). |

Mer information om aviseringar finns i avsnittet [[!DNL Observability Insights] översikt](../../observability/home.md).

## Katalogtjänst {#catalog-service}

Catalog Service är det system som registrerar var data finns och hur de härstammar från Adobe Experience Platform. Alla data som tas in i Experience Platform lagras i datasjön som filer och kataloger medan katalogen innehåller metadata och beskrivningar av dessa filer och kataloger för sök- och övervakningsändamål.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Datalagring för kundprofil i realtid | Du kan **endast** uppdatera datalagringsperioden för kundprofilen i realtid en gång var 30:e dag. |

Mer information om Katalogtjänsten finns i [översikten över Katalogtjänsten](../../catalog/home.md).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

>[!IMPORTANT]
>
>**Schematillägg för datauppsättningsexport**
>
>Om dataflöden för dataexport har skapats före november 2024 kommer dessa dataflöden att sluta fungera den **1 september 2025**. Om du behöver dataflödena för att kunna fortsätta exportera data efter 1 september 2025 måste du utöka deras scheman för varje mål som du exporterar datauppsättningar till genom att följa stegen i [den här guiden](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>**Uppdatering av IP-tillåtelselista krävs för API-baserade mål**
>
>På grund av uppgraderingar av exportmotorn för strömningsmål måste organisationer som använder [IP-tillåtelselista](../../destinations/catalog/streaming/ip-address-allow-list.md) för API-baserade mål lägga till följande IP-adresser i sina tillåtelselistor **före 15 september 2025**:
>
>**Nödvändiga IP-adresser:**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**Den här ändringen gäller följande måltyper:**
>
>- [Strömningsmål för målgruppsexport](../../destinations/destination-types.md#streaming-destinations) ([Pega CDH Realtime Audience](/help/destinations/catalog/personalization/pega-v2.md), API-baserade integreringar med [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) och [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Offentliga eller privata mål som skapats via [Destination SDK](../../destinations/destination-sdk/getting-started.md)
>
>**Åtgärd krävs:** Om du har arbetat med Adobe för att tillåtelselista IP-adresser till API-baserade strömningsmål måste du lägga till IP-adresserna ovan i tillåtelselistan för att säkerställa att inga avbrott inträffar i dataflödena till API-baserade mål.

**Nya destinationer**

| Mål | Beskrivning |
| --- | --- |
| Mål [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | Använd målet [!DNL Acxiom Real ID Audience Connection] för att förbättra målgrupperna med tekniken [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) och aktivera målgrupper på flera plattformar, till exempel [!DNL Altice], [!DNL Ampersand], [!DNL Comcast]. |

**Uppdaterade mål**

| Mål | Beskrivning |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) intern uppgradering | Från och med 11 augusti 2025 har du under en kort tidsperiod kanske sett två **[!DNL Microsoft Bing]**-kort sida vid sida i destinationskatalogen. Det här beror på en intern uppgradering av måltjänsten. Den befintliga målanslutningen **[!DNL Microsoft Bing]** har bytt namn till **[!UICONTROL (Deprecated) Microsoft Bing]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL Microsoft Bing]**. <br> Uppgraderingen har slutförts och det inaktuella kortet har tagits bort från destinationskatalogen. Använd **[!UICONTROL Microsoft Bing]**-anslutningen i katalogen för nya aktiveringsdataflöden. Om du har aktiva dataflöden till **[!UICONTROL (Deprecated) Microsoft Bing]**-destinationen uppdateras de automatiskt. Du behöver därför inte göra något. <br><br> Om du skapar dataflöden via [Flow Service API:et](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden:<ul><li>Flödesspecifikation-id: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Anslutningsspecifikation-id: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Efter den här uppgraderingen kan det hända att **antalet aktiverade profiler** i dina dataflöden minskar till [!DNL Microsoft Bing]. Denna minskning orsakas av introduktionen av **ECID-mappningskravet** för alla aktiveringar till den här målplattformen. |
| Information om förfallotid för autentisering för [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md)- och [LinkedIn Matched Audiences](../../destinations/catalog/social/linkedin-b2b.md)-destinationer | Information om förfallotid för autentisering för [!DNL LinkedIn]-destinationer visas nu direkt i Experience Platform-gränssnittet, så du kan se när din autentisering kommer att upphöra och förnya den innan den orsakar eventuella avbrott i dataflödena. Du kan övervaka förfallotiden för dina tokens från kolumnen **[!UICONTROL Account expiration date]** på flikarna **[[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts)** eller **[[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrade funktioner för sökning, filtrering och taggning för mål | Förbättra arbetsflödet för målhantering med förbättrade sök-, filtrerings- och taggningsfunktioner på flikarna [Bläddra](../../destinations/ui/destinations-workspace.md#browse) och [Konton](../../destinations/ui/destinations-workspace.md#accounts). <br> Nu kan du söka efter specifika dataflöden och konton med namn, filtrera efter olika kriterier däribland destinationsplattform eller status och datum samt skapa anpassade taggar för att ordna dina destinationer. Kolumnsortering är också tillgänglig för viktiga fält, bland annat körningstid för senaste dataflöde, vilket gör det enklare att identifiera och hantera destinationsanslutningarna. <br> ![Animerad demonstration av sökning efter ett destinationsdataflöde på fliken Bläddra](../../destinations/assets/ui/workspace/search.gif) |

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Modellbaserade scheman | Förenkla datamodelleringen med modellbaserade scheman. Nu kan du lättare skapa scheman tack vare många exempel och guider. Den här funktionen är för närvarande tillgänglig för innehavare av Campaign Orchestration-licens och kommer att utvidgas till att omfatta Data Distiller-kunder på GA, vilket gör datamodelleringen mer tillgänglig och effektiv. |

Mer information finns i [XDM-översikten](../../xdm/home.md).

<!--
## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## Sandlådor {#sandboxes}

Adobe Experience Platform är utvecklad för att berika program för digitala upplevelser på global nivå. Företagen kör ofta flera program för digitala upplevelser parallellt och måste ta hänsyn till utveckling, testning och driftsättning av dessa program samtidigt som de måste se till att de uppfyller gällande krav.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Avduplicering av beroendeobjekt vid import av arbetsflöde | Verktyg för sandlådor återanvänder nu alltid befintliga objekt om objekt med samma namn identifieras, för att undvika objektförökning. Den här ändringen gäller följande objekt: <ul><li>Schema</li><li>Fältgrupper</li><li>Målgrupp</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Mer information finns i [guiden om objekt som stöds för sandlådeverktyg](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Stöd för delning av organisationspaket i hela sandlådan | Sandlådeverktygen har nu stöd för typen **Hela sandlådan** vid delning av organisationspaket. Nu kan du dela både hela sandlådepaket och paket med flera objekt över flera organisationer. Mer information finns i [guiden om objekt som stöds för sandlådeverktyg](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Mer information om sandlådor finns i [översikten över sandlådor](../../sandboxes/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Målgruppsuppskattningar | Målgruppsuppskattningar visas nu som ett **intervall**, som baseras på samplingsdatans konfidensintervall. Mer information om uppskattningar finns i [guiden Skapa segment](/help/segmentation/ui/segment-builder.md#audience-properties). |

Mer information finns i [[!DNL Segmentation Service] översikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för källan [!DNL Oracle NetSuite] | [!DNL Oracle NetSuite]-källan är nu allmänt tillgänglig. Du kan nu ansluta ditt [!DNL Oracle NetSuite]-konto till Experience Platform för att importera aktiviteter och entitetsdata för en enhetlig analys och aktivering. Mer information finns i [[!DNL Oracle NetSuite] översikten](../../sources/connectors/marketing-automation/oracle-netsuite.md). |
| Allmän tillgänglighet för källan [!DNL PathFactory] | [!DNL PathFactory]-källan är nu allmänt tillgänglig. Du kan ansluta ditt [!DNL PathFactory]-konto till Experience Platform för att hämta besökare, sessioner och sidvisningsdata för en enhetlig analys och aktivering. Mer information finns i [[!DNL PathFactory] översikten](../../sources/connectors/marketing-automation/pathfactory.md). |
| Allmän tillgänglighet för källan [!DNL Stripe] | [!DNL Stripe]-källan är nu allmänt tillgänglig. Du kan ansluta ditt [!DNL Stripe]-konto till Experience Platform för att importera betalnings- och transaktionsdata för enhetlig analys och aktivering. Mer information finns i [[!DNL Stripe] översikten](../../sources/connectors/payments/stripe.md). |
| Förbättrad autentisering för [!DNL Azure Blob Storage] | Nu kan du använda tjänsteprincipbaserad autentisering för att ansluta din [!DNL Azure Blob Storage]-källa till Experience Platform. Använd tjänsteprincipbaserad autentisering för förbättrad säkerhet, enklare rotation av autentiseringsuppgifter och en mer detaljerad åtkomstkontroll för kontot. Mer information finns i [[!DNL Azure Blob Storage] översikten](../../sources/connectors/cloud-storage/blob.md). |

Mer information finns i [översikten över källor](../../sources/home.md).

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

| Enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination  | The enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination is an upgraded version of the existing [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector. This new connector brings profile sync capabilities in addition to the existing audience sync capabilities from the legacy connector, providing a tighter integration with [!DNL Marketo Engage]. <br> The [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector will be deprecated in **March 2026**. To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** destination, review the following key points and required actions: <ul><li>All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.</li><li> **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../destinations/ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.</li></ul>|
-->
