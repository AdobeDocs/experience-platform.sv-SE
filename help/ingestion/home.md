---
title: Översikt över dataöverföring
description: I det här dokumentet presenteras de tre viktigaste sätten att överföra data till Experience Platform, med länkar till respektive översiktsdokumentation för mer detaljerad information.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Översikt över datainmatning

I Adobe Experience Platform innebär dataöverföring transport av data från utvalda källor till ett lagringsmedium där det kan nås, användas och analyseras av en organisation. Intag av data i Experience Platform kan grupperas i två huvudkategorier: **direktuppspelning** och **gruppinmatning**.

Under direktuppspelning och gruppinmatning är ett antal olika metoder som du kan använda för att importera data till Experience Platform. Dessa metoder inkluderar användning av en mängd olika **källor** och anslutning till dessa källor för att sedan hämta data till Experience Platform.

I det här dokumentet finns en översikt över de olika sätt som data kan importeras till Experience Platform.

<!-- Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Experience Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Experience Platform services. -->

## Direktinmatning {#streaming}

Du kan använda direktuppspelningsinmatning för att skicka data från klient- och serverenheter till Experience Platform i realtid. Experience Platform stöder användningen av datainmatningar för att strömma inkommande upplevelsedata, som finns kvar i strömningsaktiverade datauppsättningar i datasjön. Datainmatningar kan konfigureras så att de automatiskt autentiserar de data de samlar in, vilket säkerställer att data kommer från en betrodd källa.

Mer information finns i [översikten över direktuppspelning](./streaming-ingestion/overview.md).

## Batchförtäring {#batch}

I Experience Platform är en batch en uppsättning data som samlats in under en tidsperiod och som bearbetas tillsammans som en enda enhet. Datauppsättningar består av grupper. Du kan använda gruppinmatning för att importera data till Experience Platform som gruppfiler. När du har importerat batcharna innehåller de metadata som beskriver antalet poster som har importerats samt eventuella poster som misslyckades och tillhörande felmeddelanden.

Manuellt överförda datafiler som platta CSV-filer (mappade till XDM-scheman) och parquet-filer måste importeras med den här metoden.

Mer information finns i översikten över [gruppöverföring](./batch-ingestion/overview.md).

## Källor {#sources}

Du kan även importera data genom att ansluta till Experience Platform-källor. Experience Platform har en katalog med en mängd olika datakällor som du kan ansluta till och importera data från. Källorna kan vara Adobe-program som Adobe Analytics eller Marketo Engage. Du kan även ansluta till tredjepartskällor som källan [!DNL Amazon S3] och källan [!DNL Google Cloud Storage].

Källor grupperas i olika kategorier, som molnlagring, databaser och CRM-system. En viss källa kan ha stöd för inmatning av grupper eller strömning.

Med källor kan du importera data från ett antal olika datakällor och från olika kategorier av användningsfall. Dessutom ger datainmatning via en källa dig möjlighet att autentisera mot den externa datakällan, konfigurera ett intag-schema och hantera intag-genomströmning.

Mer information finns i [källöversikten](../sources/home.md).

### Skapa ML-stödda scheman {#ml-assisted-schema-creation}

För att snabbt integrera nya datakällor kan du nu använda maskininlärningsalgoritmer för att generera ett schema från exempeldata. Den här automatiseringen förenklar framtagningen av korrekta scheman, minskar antalet fel och snabbar upp processen från datainsamling till analys och insikter.

Mer information om det här arbetsflödet finns i guiden [Skapa XML-stödda scheman](../xdm/ui/ml-assisted-schema-creation.md).

## Dataförberedelse {#data-prep}

Dataförberedelse är inte en metod för konsumtion, men det är en viktig del av dataöverföringsprocessen. Använd prep-funktioner för att mappa, omvandla och validera data till och från Experience Data Model (XDM) innan du skapar ett dataflöde för att importera data till Experience Platform. Dataförinställningen visas som mappningssteget i Experience Platform-användargränssnittet under dataöverföringsprocessen.

Mer information finns i [översikten över dataförinställningar](../data-prep/home.md).

## Direktuppspelningsmetoder {#streaming-ingestion-methods}

I följande tabell visas de olika metoder som du kan använda för att importera direktuppspelningsdata till Experience Platform.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Direktuppspelningskällor</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Metod</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vanliga användningsfall</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokoll</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Överväganden</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=sv-SE" style="color:#0563c1; text-decoration:underline">Adobe Web/Mobile SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Datainsamling från webbplatser och mobilappar.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Önskad metod för klientsidsamling.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Implementera flera Adobe-program med hjälp av en enda SDK.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/sv/docs/experience-platform/sources/connectors/streaming/http" style="color:#0563c1; text-decoration:underline">HTTP API Connector</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Samling från strömningskällor, transaktioner, relevanta kundhändelser och signaler.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Raw- eller XDM-data direktuppspelas direkt till navet utan Edge-segmentering i realtid eller händelsevidarebefordran.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=sv-SE" style="color:#0563c1; text-decoration:underline">[!DNL Edge Network] API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Samling från strömningskällor, transaktioner, relevanta kundhändelser och signaler från den globalt distribuerade [!DNL Edge Network].</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Data direktuppspelas via [!DNL Edge Network]. Stöd för segmentering i realtid och vidarebefordran av event i Edge. </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=sv-SE" style="color:#0563c1; text-decoration:underline">Adobe</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Inläsning av data från program som Adobe Analytics, Marketo Engage, Adobe Campaign Managed Services, Adobe Target, Adobe Audience Manager</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, Source Connectors och API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vi rekommenderar att du migrerar till SDK för webben/mobiler i stället för att använda traditionella SDK:er för program.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=sv-SE" style="color:#0563c1; text-decoration:underline">Direktuppspelningskällor</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Inmatning av en Enterprise-händelseström, som vanligtvis används för att dela företagsdata till flera program längre fram i kedjan. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, REST API, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Data direktuppspelas i JSON-format och kan mappas till XDM-schema.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/sv/docs/experience-platform/sources/sdk/streaming-sdk/getting-started" style="color:#0563c1; text-decoration:underline">Direktuppspelningskällor SDK</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Använd självbetjäningsfunktionerna i Self-Serve Sources Streaming SDK för att integrera din egen datakälla i Experience Platform-källkatalogen.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, HTTP API, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Exempel på partnerintegrerade strömningskällor är: Braze, Pendo och RainFocus.</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

## Gruppintagsmetoder {#batch-ingestion-methods}

I följande tabell visas de olika metoder som du kan använda för att importera batchdata till Experience Platform.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Batchkällor</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Metod</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Vanliga användningsfall</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protokoll</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Överväganden</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/sv/docs/experience-platform/ingestion/batch/overview" style="color:#0563c1; text-decoration:underline">API för gruppinmatning</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Inmatning från en företagshanterad kö. Använd batchintag om dina data behöver förberedas och formateras före intag.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, JSON eller Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Måste hantera grupper och filer för inhämtning.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/sv/docs/experience-platform/sources/home" style="color:#0563c1; text-decoration:underline">Batchkällor</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">En gemensam metod för inmatning av data från molnlagringssystem, CRM och automatiserade marknadsföringsprogram.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Perfekt för konsumtion av stora mängder historiska data.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Intag från Source baserat på förkonfigurerade schemalagda intervall.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=sv-SE" style="color:#0563c1; text-decoration:underline">Datallandningszon</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Adobe-etablerat molnbaserat fillagring. Du har tillgång till en Data Landing Zone-behållare per sandlåda.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Skicka filerna till Data Landing Zone för senare inhämtning i Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Experience Platform tillämpar en strikt 7-dagars förfallotid för alla filer och mappar som överförs till en Data Landing Zone-behållare. Alla filer och mappar tas bort efter sju dagar.</span></span></span></li>
</ul>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=sv-SE" style="color:#0563c1; text-decoration:underline">Batchkällor SDK</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Använd självbetjäningsfunktionerna i Batch SDK för självbetjäning för att integrera din egen datakälla med Experience Platform källkatalog.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Perfekt för partneranslutningar eller för en skräddarsydd arbetsflödesupplevelse för att skapa en företagskontakt.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull, REST API, CSV eller JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Exempel på partnerintegrerade batchkällor är: Mailchimp, OneTrust, Zendesk</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>

## Nästa steg och ytterligare resurser

Det här dokumentet innehåller en kort introduktion till de olika aspekterna av [!DNL Data Ingestion] i [!DNL Experience Platform]. Fortsätt att läsa översiktsdokumentationen för varje intagsmetod för att bekanta dig med deras olika funktioner, användningsfall och bästa metoder. Du kan även komplettera din inlärning genom att titta på videon med en översikt över importen nedan. Mer information om hur [!DNL Experience Platform] spårar metadata för kapslade poster finns i [Katalogtjänstöversikt](../catalog/home.md).

>[!WARNING]
>
>Termen Enhetlig profil som används i följande video är inaktuell. Termerna [!DNL "Profile"] eller [!DNL "Real-Time Customer Profile"] är rätt termer som används i dokumentationen för [!DNL Experience Platform]. Läs dokumentationen om de senaste funktionerna.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
