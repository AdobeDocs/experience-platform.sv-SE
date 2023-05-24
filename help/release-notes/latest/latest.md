---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation från maj 2023 för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 85401e3abfd7d5d1d84e082d20a1a064760c4e19
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

>[!IMPORTANT]
>
>Som en förberedelse för den allmänt tillgängliga funktionen Audience Portal uppdaterar Adobe Experience Platform användningen av&quot;målgrupper&quot; och&quot;segment&quot; i systemet och dokumentationen.
>
>- **Målgrupp**: En uppsättning personer, konton, hushåll eller andra enheter som delar gemensamma egenskaper och beteenden.
>
>- **Segmentdefinition**: I Adobe Experience Platform används de regler som beskriver en målgrupps viktigaste egenskaper eller beteenden. Termen kallades tidigare bara&quot;segment&quot;.
>
>- **Segment**: Att dela upp profiler i olika målgrupper. Termen&quot;segment&quot; används nu uteslutande som verb.
>
>- **Segmentering**: Identifiering och uttrycksfullgörande av egenskaperna hos de profiler som ska grupperas tillsammans för att producera ett antal resultat, till exempel en målgrupp.
>
>I Adobe Experience Platform-gränssnittet kommer du att se&quot;Segment&quot; ersatt med&quot;Publiker&quot; för att återspegla den nya vägen för målgruppsframtagning och -hantering.

**Lanseringsdatum: 24 maj 2023**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [Datastyrning](#data-governance)
- [Datainmatning](#data-ingestion)
- [Frågetjänst](#query-service)
- [Källor](#sources)

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Twitter] API-tillägg för konverteringar | The [[!DNL Twitter] Konverterings-API](../../tags/extensions/server/twitter/overview.md) tillägg för händelsevidarebefordran gör att du kan vidarebefordra händelsedatadriven i realtid för händelsekonverteringar med [!DNL Twitter] Konverterings-API. |
| Sökvägshjälp för dataelement | Bestämma sökvägen för dataelementet i [Kärntillägg](../../tags/extensions/client/core/overview.md) är nu enklare än någonsin. Den här förbättringen innehåller ett guidat formulär som hjälper dig att välja och formatera rätt dataelementsökväg. |

{style="table-layout:auto"}

Läs mer om datainsamlingar i [datainsamling, översikt](../../tags/home.md).

## Datastyrning {#data-governance}

Adobe Experience Platform Data Governance är en serie strategier och tekniker som används för att hantera kunddata och säkerställa att regler, begränsningar och policyer som gäller för dataanvändning följs. Det spelar en nyckelroll på olika nivåer inom Experience Platform, bland annat för katalogisering, datalinje, märkning av dataanvändning, dataåtkomstregler och åtkomstkontroll av data för marknadsföringsåtgärder.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Borttagning av etiketter på datamängdsnivå | Möjligheten att använda etiketter på enskilda fält har flyttats från datauppsättningar till scheman. På så sätt kan ni centralisera hanteringen av fältetiketter för datastyrning, samtycke och åtkomstkontroll. Tidigare tillämpade etiketter för datamängdsfält stöds tillfälligt via användargränssnittet i Experience Platform. Befintliga etiketter för datamängdsfält måste migreras manuellt till schemafältetiketterna senast den 31 maj 2024. Läs [handbok för hela datastyrningen](../../data-governance/e2e.md) för mer information om etikettmigrering. |

{style="table-layout:auto"}

Läs mer om datastyrning i [datastyrningsöversikt](../../data-governance/home.md).

## Datainmatning {#data-ingestion}

Adobe Experience Platform har en omfattande uppsättning funktioner för att importera alla typer av data och all fördröjning. Du kan importera med hjälp av API:er för gruppbearbetning eller direktuppspelning, med hjälp av Adobe-byggda källor, dataintegrationspartners eller Adobe Experience Platform användargränssnitt.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Tillgång till mallar för dataöverföring | Med mallar för dataöverföring får dataarkitekter och ingenjörer standardmallar och automatiseringsverktyg som snabbar upp dataöverföringsprocessen, inklusive skapande av scheman och datamängder samt konfiguration av mappningsregler. Mallar för dataöverföring är tillgängliga för [[!DNL Marketo Engage]](../../sources/connectors/adobe-applications/marketo/marketo.md), [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) och [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) källor. Mer information finns i guiden [använda mallar i användargränssnittet](../../sources/tutorials/ui/templates.md). |

Läs mer om dataöverföring i [dataöverföring - översikt](../../ingestion/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform [!DNL data lake]. Du kan ansluta alla datauppsättningar från datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas i rapporter, Data Science Workspace eller för att matas in i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Beräkna kolumnnivåstatistik för ADLS-datauppsättningar | The `ANALYZE TABLE` kommandot har utökats med `COMPUTE STATISTICS` och `SHOW STATISTICS` SQL-kommandon. Du kan nu beräkna statistik för en delmängd av en ADLS-datauppsättning eller för vissa kolumner i den datauppsättningen. Mer information finns i [beräkningsguide för datauppsättningsstatistik](../../query-service/essential-concepts/dataset-statistics.md). |

{style="table-layout:auto"}

Läs mer om Query Services i [Översikt över frågetjänsten](../../query-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och göra det möjligt att strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Utökat API-stöd för utkastläge | Du kan nu pausa och spara förloppet under källarbetsflödet när du använder [!DNL Flow Service] API när som helst. Använd `mode=draft` för att spara bas-, käll- och målanslutningar som utkast. Alla utkastenheter kan granskas för att slutföras vid ett senare tillfälle. Läs guiden på [ange [!DNL Flow Service] enheter till ett utkastläge](../../sources/tutorials/api/draft.md) för mer information. |
| Allmän tillgänglighet till [!DNL Salesforce Marketing Cloud] källa | The [[!DNL Salesforce Marketing Cloud source] är nu med i GA](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Använd den här källan för att ta med [!DNL Salesforce Marketing Cloud] data till Experience Platform. |
| [!DNL Google Ads] autentiseringsuppdateringar | Du kan nu ange ett användar-ID för inloggningskund när du autentiserar [!DNL Google Ads] källkonto för att hämta rapportdata från en viss driftskund. Läs [[!DNL Google Ads] källdokumentation](../../sources/connectors/advertising/ads.md) för mer information. |
| [!DNL Google PubSub] autentiseringsuppdateringar | Nu kan du definiera behörigheter för dina [!DNL Google PubSub] källa när du skapar ett nytt konto. Använd projektbaserad autentisering för att tillåta åtkomst på rotnivå eller använd ämne- och prenumerationsbaserad autentisering för att begränsa åtkomst till ett visst ämne och en viss prenumerationsström. Läs [[!DNL Google PubSub] källdokumentation](../../sources/connectors/cloud-storage/google-pubsub.md) för mer information. |
| Nya parametrar för sidnumreringsfält för `type=PAGE` i självbetjäningskällor (batch-SDK) | Du kan nu använda `initialPageIndex` och `endPageIndex` när du integrerar en källa med `type=PAGE` via Batch SDK. <ul><li>`initialPageIndex`: Med den här parametern kan du definiera det sidnummer som sidnumreringen börjar från. </li><li>`endPageIndex`: Med den här parametern kan du skapa ett slutvillkor och stoppa sidnumreringen.</li></ul> Mer information om de nya parametrarna finns i [Självbetjänad SDK-dokumentation för batchkällor](../../sources/sources-sdk/config/sourcespec.md#page). |
| Gränssnittsstöd för utkastläge | Du kan nu pausa och spara förloppet under källarbetsflödet via användargränssnittet. Du kan välja **[!UICONTROL Save as draft]** under arbetsflödets dataflödesdetaljer, mappning och schemaläggning för att spara dataflödet som ett utkast för senare slutförande. Läs guiden på [spara dataflöden som utkast i användargränssnittet](../../sources/tutorials/ui/draft.md) för mer information. |

{style="table-layout:auto"}

Läs mer om källor i [källöversikt](../../sources/home.md).

<!-- | API support for streaming data from a [!DNL Snowflake] database | You can now stream data from a [[!DNL Snowflake] source](../../sources/connectors/databases/snowflake.md) using the [!DNL Flow Service] API. | -->