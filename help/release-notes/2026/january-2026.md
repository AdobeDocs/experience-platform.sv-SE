---
title: Versionsinformation om Adobe Experience Platform januari 2026
description: Versionsinformationen för Adobe Experience Platform i januari 2026.
source-git-commit: 49074f3ea2650254863a58a488c626f683ba7f06
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 22%

---


# Versionsinformation för Adobe Experience Platform

>[!TIP]
>
>Ta del av följande dokumentation för versionsinformation om andra Adobe Experience Platform-program:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/sv/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/releases/latest)
>- [Federerad målgruppssammansättning](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/sv/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 27 januari 2026**

Nya funktioner och uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Mål](#destinations)
- [Kundprofil i realtid](#real-time-customer-profile)
- [Scheman](#schemas)
- [Segmenteringstjänst](#segmentation-service)
- [Källor](#sources)

## Agent Orchestrator {#agent-orchestrator}

Med Agent Orchestrator kan ni bygga och driftsätta AI-baserade agenter som kan automatisera arbetsflöden och interagera med kunder över flera kanaler.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Adobe Experience Platform Agents användningsbundna testversion | **Utvalda kunder har nu kostnadsfri utvärderingsåtkomst till Adobe Experience Platform Agents**. Du kan använda testversionen för att utforska och interagera med agenter via AI Assistant-gränssnittet från Adobe Experience Platform Agent Orchestrator. Testversionen ger en praktisk upplevelse av AI-agenter som arbetar i kundens befintliga Experience Cloud-produkter och -miljöer, och låter team utvärdera värdet innan de genomför ett fullständigt köp. Adobe Experience Platform Agents vägleds av användarinmatningar och övervakning och respekterar befintliga åtkomstkontroller på produktnivå, vilket säkerställer att användarna bara kan utföra åtgärder eller visa data som de är auktoriserade för inom de underliggande Experience Cloud-programmen. Läs [Experience Platform Agents användningsbundna utvärderingsversion](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial) om du vill ha mer information om hur du kommer igång. |

{style="table-layout:auto"}

Mer information finns i [Agent Orchestrator-dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Mål {#destinations}

[!DNL Destinations] är förbyggda integrationer med målplattformar som möjliggör sömlös aktivering av data från Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya eller uppdaterade destinationer**

| Mål | Beskrivning |
| --- | --- |
| [Kevel-målanslutning](/help/destinations/catalog/advertising/kevel.md) är nu tillgänglig | Strömningsmålet [!DNL Kevel] för Adobe Experience Platform gör det möjligt för kunder att aktivera Adobe-målgrupper direkt i [!DNL Kevel]s API:er för UserDB och segmenthantering för att ge stöd för målanpassning i realtid vid annonsbeslut. [[!DNL Kevel]](https://www.kevel.com/) innehåller den AI-aktiverade tekniken och expertvägledningen som hjälper innovativa handelsledare att starta, skala och lyckas inom detaljhandelsmedia. Retail Media Cloud för [!DNL Kevel] har funktioner för riktade, hänförliga och anpassningsbara annonseringsformat för annonsering på plats och utanför webbplatsen. |
| [Målkopplingen för Exchange](/help/destinations/catalog/advertising/index-exchange.md) är nu tillgänglig | Använd den här målkopplingen om du vill exportera målgruppssegment från Adobe Experience Platform direkt till [!DNL Index Exchange]s programmatiska annonsplattform. [!DNL Index] är en global plattform för annonsleveranser som hjälper mediekonstruktörer att maximera värdet av sitt innehåll på alla skärmar. Med över 20 års branschledarskap knyter [!DNL Index] samman världens största varumärken med förstklassiga upplevelsemakare för att leverera högkvalitativa kundupplevelser. |
| Regionala slutpunkter stöder Braze-anslutningar | Alla [regionspecifika slutpunkter](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) som stöds av [!DNL Braze] är nu tillgängliga för val under målkonfigurationsflödet. Fråga din [!DNL Braze]-representant vilken slutpunktsinstans du ska använda. |
| Stöd för schemaläggning varje vecka och månad för [Liveramp Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Du kan nu konfigurera exportscheman varje vecka och månad för Liveramp Onboarding-målet. <br> Den här versionen lanseras gradvis och kommer att vara slutförd den 30 januari. |
| Förbättrad aktiveringsupplevelse för [Trade Desk](../../destinations/catalog/advertising/tradedesk.md)- och [Microsoft Bing](../../destinations/catalog/advertising/bing.md)-mål | Trade Desk och Microsoft Bing-destinationerna innehåller nu fördefinierade obligatoriska mappningar för en optimerad aktiveringsupplevelse.  <br> Den här versionen lanseras gradvis och kommer att vara slutförd den 30 januari. ![Bild som visar fördefinierade mappningar för Trade Desk](assets/january/mandatory-mappings-ttd.png) {width="150" align="center" zoomable="yes"} <br> ![Bild som visar fördefinierade mappningar för Microsoft Bing ](assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| Telefonnummeraktivering stöds för [Trade Desk - CRM](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing)-anslutningen | Trade Desk - CRM-destinationen stöder nu aktivering av telefonnummer utöver e-postadresser. Du kan aktivera både ohashade telefonnummer i E.164-format och hashade telefonnummer (SHA256_E.164-format) till ditt Trade Desk-konto för målgruppsanpassning och inaktivering baserat på CRM-data. Telefonnummer måste normaliseras till E.164-format innan aktivering. |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) - måluppdateringar | Snowflake Batch-målet innehåller nu funktioner för regionval under målkonfigurationen. Nu kan du välja den specifika Snowflake-region där instansen är etablerad, vilket ger optimal dataöverföring och efterlevnad av regionala krav. Dessutom har standardbegränsningen för sammanfogningsprinciper tagits bort, vilket gör att du kan exportera målgrupper som är mappade till valfri sammanfogningsprincip. <br> Batchmålet [!DNL Snowflake] är för närvarande endast tillgängligt för Real-Time CDP-kunder som etablerats i Experience Platform VA7-regionen. |


<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <ul><li>**[!UICONTROL Default]**: Data will be encrypted at rest with the default encryption algorithm set on your bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest with the AES256 algorithm when it lands in S3. **This option takes precedence over any default encryption algorithm configured on your S3 bucket**.</li></ul> This release is being rolled out gradually and will be complete by January 30th.| -->

**Ny eller uppdaterad funktionalitet**

| Funktion | Beskrivning |
| --- | --- |
| Skyddsgränsen för [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)-mål har uppdaterats | Det maximala antalet målgrupper som kan mappas till ett enda Adobe Target-mål har ökats från 50 till 250. På så sätt anpassas Adobe Target till standardmålgruppsgränsen för andra destinationer, vilket ger större flexibilitet i arbetsflödena för målgruppsaktivering. Nu kan du aktivera fler målgrupper för Adobe Target-destinationer utan att behöva skapa flera dataflöden. |
| [Redigera mål](/help/destinations/ui/edit-destination.md) och [redigera marknadsföringsåtgärder](/help/destinations/ui/edit-activation.md#edit-marketing-actions) allmän tillgänglighet | Alternativet att redigera mål och marknadsföringsåtgärder är nu tillgängligt för alla användare. |
| Växla visningsnamn för fält i mappningen [step](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) | När du mappar schemafält till ett mål kan du nu växla mellan att visa det fullständiga XDM-fältnamnet och endast visa visningsnamnet. <br> ![Skärminspelning med växlingsknappen för visningsnamn.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Mer information finns i [översikten över destinationer](../../destinations/home.md).

## Kundprofil i realtid {#real-time-customer-profile}

Med kundprofilen i realtid kan ni få en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [Strömningskapacitet](/help/landing/license-usage-and-guardrails/capacity.md) - tvång | Experience Platform tillämpar nu strömningskapacitet för kundprofil och identitetstjänst i realtid. När kunderna överträffar sin avtalade strömningskapacitet kommer data att ställas i kö och behandlas på ett första-i-första-ut-sätt. Detta garanterar förutsägbara systemprestanda och förhindrar att kapacitetsöverträdelser påverkar dataöverföringskvaliteten. Viktigt: <ul><li>Direktuppspelande serveringar är inte tillgängliga i datasjön när kapaciteten överskrids</li><li>Detta gäller inte kunder med Adobe Journey Optimizer-licenser</li><li>Data som står i kö bearbetas sekventiellt när kapaciteten blir tillgänglig.</li></ul> Mer information finns i [kapacitetsöversikt](/help/landing/license-usage-and-guardrails/capacity.md). |
| Borttagning av enhetssökning | Användning av entitetssöknings-API för upplevelsehändelser är nu föråldrat för alla Real-Time CDP Prime-kunder. Med den här borttagningen kan Real-Time CDP integreras med licensieringsfunktionerna. Real-Time CDP Ultimate-kunder som avser att använda den här funktionen kan kontakta Adobe kundtjänst för att återaktivera den här funktionen.  Mer information finns i [enhets-API-handboken](/help/profile/api/entities.md). |
| Övervaka jobbstatus för inmatning av profil | Nu kan du övervaka förloppsprocenten på jobbnivå för att batchprofilinmatningsdataflödet ska köras. Den här funktionen gör att man kan se hur batchimporten fortskrider i realtid, inklusive viktiga kontrollpunkter som anger om inmatningen är klar för kundsegmentering och Adobe Journey Optimizer-sökningar. För stora inmatningar som kan ta flera timmar att bearbeta, hjälper den här förloppsindikatorn dig att förstå om jobbet går normalt eller stöter på problem, vilket minskar osäkerheten under databearbetningen. Mer information finns i [guiden för bildskärmsprofiler](/help/dataflows/ui/monitor-profiles.md). |
| Förbättringar av profilvisningsprogram (GA) | Följande förbättringar av profilvisningsprogrammet är nu allmänt tillgängliga. <ul><li>**Kombinerad vy**: Attribut, händelser och insikter har kombinerats till en enda vy.</li><li>**AI-genererade insikter**: Sidan med profilinformation visar nu AI-genererade insikter, som visar information som genererats från din profil. Dessa insikter kan innehålla information som benägenhetspoäng och trendanalyser.</li><li>**Stiluppdatering**: Sidan med profilinformation har uppdaterats visuellt.</li><li>**Bläddra**: Nu kan du utforska dina profiler via en interaktiv kortbaserad karusell med sökning och anpassning.</li></ul> Mer information finns i [profilvisningsguiden](/help/profile/ui/user-guide.md). |

{style="table-layout:auto"}

Mer information finns i [[!DNL Real-Time Customer Profile] översikten](../../profile/home.md).

## Segmenteringstjänst {#segmentation-service}

[!DNL Segmentation Service] definierar en viss deluppsättning av profiler genom att beskriva de kriterier som skiljer en säljbar grupp människor inom din kundbas. Målgrupper kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ditt varumärke.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Uppdatera utgångsdatum för externa målgruppsdata | Externa målgrupper (t.ex. CSV-överföringar) har nu stöd för en tvingad uppdateringsfunktion för inställningar för förfallodatum för data. Med den här funktionen kan användare uppdatera utgångsdatumet för data manuellt för externa målgrupper, vilket ger bättre kontroll över hanteringen av målgruppernas livscykler. Detta är särskilt användbart för målgrupper som måste stanna kvar efter sin ursprungliga förfalloperiod eller som behöver aktiveras på nytt utan att överföra informationen på nytt. Mer information om den här funktionen finns i [Översikt över målportalen](../../segmentation/ui/audience-portal.md#audience-summary). |
| Målgruppsvalidering | Experience Platform har nu inbyggda valideringar för att säkerställa att era målgrupper är korrekta, stabila och skalbara. Dessa kontroller körs automatiskt i realtid när du skapar målgruppsdefinitioner. Mer information finns i [publikverifieringsöversikten](/help/segmentation/validation.md). |

Mer information finns i [[!DNL Segmentation Service] översikten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

**Nya eller uppdaterade källor**

| Källa | Beskrivning |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2-källa | En ny [!DNL Oracle Eloqua]-källkoppling är nu tillgänglig och ersätter den [inaktuella kopplingen](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Den här uppdaterade anslutningen ger förbättrad funktionalitet och förbättrad tillförlitlighet vid inmatning av data från [!DNL Oracle Eloqua] till Experience Platform. Kunder som använder den befintliga anslutningen bör migrera till den nya implementeringen eftersom befintliga anslutningar inte längre fungerar. Den nya kopplingen stöder alla installations- och konfigurationssteg som behövs för att ansluta till [!DNL Oracle Eloqua] och data för automatiserad import. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2-källa | En ny [!DNL Salesforce Marketing Cloud]-källkoppling är nu tillgänglig och ersätter den [inaktuella kopplingen](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Den här uppdaterade anslutningen ger bättre prestanda och ytterligare funktioner för inmatning av data från [!DNL Salesforce Marketing Cloud] till Experience Platform. Kunder som använder den befintliga kopplingen bör gå över till den nya implementeringen. Den nya kopplingen innehåller omfattande konfigurationsinstruktioner för anslutning till [!DNL Salesforce Marketing Cloud] och inmatning av automatiserade marknadsföringsdata. |

Mer information finns i [översikten över källor](../../sources/home.md).

