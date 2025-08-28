---
title: Versionsinformation om Adobe Experience Platform för augusti 2025
description: Versionsinformation för augusti 2025 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 45a50800f74a6a072e4246b11d338b0c134856e0
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 81%

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
- [Kundprofil i realtid](#profile)
- [Sandlådor](#sandboxes)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Aviseringar {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika Experience Platform-aktiviteter. Du kan prenumerera på olika aviseringsregler på fliken [!UICONTROL Alerts] i Experience Platform-användargränssnittet och du kan välja att ta emot aviseringssmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
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
| Förbättrat [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)-mål | Det utökade [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)-målet är en uppgraderad version av den befintliga [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)-kopplingen. Den här nya kopplingen erbjuder profilsynkroniseringsfunktioner utöver de befintliga målgruppssynkroniseringsfunktionerna från den äldre anslutningen, vilket ger en tätare integrering med [!DNL Marketo Engage]. <br> Kopplingen [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) kommer att bli inaktuell i **mars 2026**. Granska följande nyckelpunkter och nödvändiga åtgärder för att säkerställa en smidig övergång till det nya **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)**-målet: <ul><li>Alla användare av det befintliga **[!UICONTROL (Legacy) (V2) Marketo Engage]** måste migrera till det nya **[!UICONTROL Marketo Engage]**-målet före mars 2026.</li><li> **Befintliga dataflöden migreras inte automatiskt.** Du måste [konfigurera en ny anslutning](../../destinations/ui/connect-destination.md) till det nya **[!UICONTROL Marketo Engage]**-målet och aktivera målgrupperna där.</li></ul> |

**Uppdaterade mål**

| Mål | Beskrivning |
| --- | --- |
| [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) intern uppgradering | Från och med den 11 augusti 2025 har du kanske sett två **[!DNL Microsoft Bing]**-kort sida vid sida i målkatalogen under en kort tidsperiod. Det här beror på en intern uppgradering av måltjänsten. Den befintliga målanslutningen **[!DNL Microsoft Bing]** har bytt namn till **[!UICONTROL (Deprecated) Microsoft Bing]** och du har nu tillgång till ett nytt kort med namnet **[!UICONTROL Microsoft Bing]**. <br> Uppgraderingen har slutförts och det borttagna kortet har tagits bort från målkatalogen. Använd anslutningen **[!UICONTROL Microsoft Bing]** i katalogen för nya aktiveringsdataflöden. Om du har haft aktiva dataflöden till målet **[!UICONTROL (Deprecated) Microsoft Bing]** uppdateras de automatiskt, så ingen åtgärd krävs från dig. <br><br> Om du skapar dataflöden via [Flow Service API:et](https://developer.adobe.com/experience-platform-apis/references/destinations/) måste du uppdatera [!DNL flow spec ID] och [!DNL connection spec ID] till följande värden:<ul><li>Flödesspecifikation-id: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>Anslutningsspecifikation-id: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Efter den här uppgraderingen kan det hända att **antalet aktiverade profiler** i dina dataflöden minskar till [!DNL Microsoft Bing]. Denna minskning orsakas av introduktionen av **ECID-mappningskravet** för alla aktiveringar till den här målplattformen. |
| Information om förfallodatum för autentisering för [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) och [LinkedIn Matched Audiences](../../destinations/catalog/social/linkedin-b2b.md) | Information om förfallodatum för autentisering för [!DNL LinkedIn]-mål visas nu direkt i Experience Platform-gränssnittet, så du kan se när din autentisering kommer att upphöra och förnya den innan den orsakar eventuella avbrott i dataflödena. Du kan övervaka dina tokens förfallodatum från kolumnen **[!UICONTROL Account expiration date]** på flikarna **[[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts)** eller **[[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse)**. |

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrade funktioner för sökning, filtrering och taggning för mål | Förbättra arbetsflödet för målhantering med förbättrade sök-, filtrerings- och taggningsfunktioner på flikarna [Bläddra](../../destinations/ui/destinations-workspace.md#browse) och [Konton](../../destinations/ui/destinations-workspace.md#accounts). <br> Du kan nu söka efter specifika dataflöden och konton efter namn, filtrera efter olika villkor, inklusive målplattform, status och datum, och skapa anpassade taggar för att ordna dina mål. Kolumnsortering är också tillgängligt för nyckelfält som körningstid för senaste dataflöde, vilket gör det enklare att identifiera och hantera målanslutningarna. <br> ![Animerad demonstration av sökning efter ett måldataflöde på fliken Bläddra](../../destinations/assets/ui/workspace/search.gif) |


## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan all data om kundupplevelsen införlivas i en gemensam representation för att leverera insikter på ett snabbare och mer integrerat sätt. Du kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut för personalisering.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Modellbaserade scheman | Förenkla datamodelleringen med modellbaserade scheman. Nu kan du lättare skapa scheman tack vare många exempel och guider. Den här funktionen är för närvarande tillgänglig för innehavare av Campaign Orchestration-licens och kommer att utvidgas till att omfatta Data Distiller-kunder på GA, vilket gör datamodelleringen mer tillgänglig och effektiv. |

Mer information finns i [XDM-översikten](../../xdm/home.md).

## Kundprofil i realtid {#profile}

Kundprofilen i realtid ger en enhetlig, användbar bild av varje kund genom att konsolidera data från alla kanaler till en enda profil.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrade sökfunktioner i Entities API | Entities API har nu stöd för följande: <ul><li>Person (profil)</li><li>Experience-händelser</li><li>Konto</li><li>Möjligheter</li></ul> Den här uppdateringen förenklar API-användningen och hjälper till att säkerställa optimal prestanda och tillförlitlighet. Om du tidigare har använt sökningar efter andra enhetstyper, inklusive sammanfogningstabeller och anpassade multienhetstyper, kan du passa på att granska din API-användning och dra nytta av den förbättrade upplevelsen. Mer information finns i [arkitekturuppgraderingsguiden för Real-Time CDP B2B Edition](../../rtcdp/b2b-architecture-upgrade.md). |

Mer information om kundprofil i realtid finns i [profilöversikten](../../profile/home.md).

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
| Målgruppsuppskattningar | Målgruppsuppskattningar genereras nu automatiskt i Segment Builder. Värdet uppdateras varje gång du ändrar målgruppen och återspeglar alltid de senaste målgruppsreglerna. Beräkningen visas nu som ett **intervall** som baseras på konfidensintervall för samplingsdata. |

Mer information finns i [[!DNL Segmentation Service] översikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrad autentisering för [!DNL Azure Blob Storage] | Nu kan du använda tjänsteprincipbaserad autentisering för att ansluta din [!DNL Azure Blob Storage]-källa till Experience Platform. Använd tjänsteprincipbaserad autentisering för förbättrad säkerhet, enklare rotation av autentiseringsuppgifter och en mer detaljerad åtkomstkontroll för kontot. Mer information finns i [[!DNL Azure Blob Storage] översikten](../../sources/connectors/cloud-storage/blob.md). |

Mer information finns i [översikten över källor](../../sources/home.md).

<!---

| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

-->

