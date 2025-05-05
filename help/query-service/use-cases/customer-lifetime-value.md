---
title: Spåra datasignaler för att generera kundens livstidsvärde
description: Den här guiden ger en heltäckande demonstration av hur man använder Data Distiller och användardefinierade dashboards med Real-Time Customer Data Platform för att mäta och visualisera kundens livstidsvärde.
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 0%

---

# Spåra datasignaler för att generera kundens livstidsvärde

Med Real-Time Customer Data Platform kan ni spåra kundens livstidsvärde (CLV) och visualisera mätvärdet med användardefinierade dashboards. Genom att använda Data Distiller och användardefinierade dashboards kan ni mäta hur värdefull en kund är för ert företag i hela er relation. Att känna till CLV kan hjälpa er att utveckla era affärsstrategier för att förvärva nya kunder samtidigt som ni behåller de befintliga och behåller vinstmarginalerna.

Följande grafik visar den cykel med datainsamling, hantering, analys och aktivering som genererar högpresterande data för att förbättra era marknadsföringskampanjer.

![Grund-trip-infografik för data från observation till analys till åtgärd.](../images/use-cases/infographic-use-case-cycle.png)

Det här heltäckande användningsexemplet visar hur datasignaler kan hämtas och ändras för att beräkna det härledda attributet för kundens livstidsvärde. Dessa härledda datauppsättningar kan sedan tillämpas på dina Real-Time CDP-profildata och kan användas med användardefinierade instrumentpaneler för att skapa en instrumentpanel för insiktsanalys. Med Data Distiller kan ni utöka Real-Time CDP insiktsdatamodell och använda CLV-härledda datauppsättningar och instrumentpanelsinsikter för att skapa en ny målgrupp och aktivera den till önskat mål. Dessa högpresterande målgrupper kan sedan användas som stöd för nästa marknadsföringskampanj.

Den här guiden är utformad för att hjälpa er att förstå kundupplevelsen bättre genom att mäta datasignaler över viktiga kontaktytor som driver CLV och implementerar ett liknande användningsfall i er miljö. Hela processen sammanfattas i bilden nedan.

![En grafik över de steg som krävs för att utnyttja kundens livstidsvärde.](../images/use-cases/implementation-steps.png)

## Komma igång {#getting-started}

Den här handboken kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Frågetjänst](../home.md): Tillhandahåller ett användargränssnitt och ett RESTful API där du kan använda SQL-frågor för att analysera och förbättra dina data.
* [Segmenteringstjänst](../../segmentation/home.md): Gör att du kan generera målgrupper från kundprofildata i realtid.

## Förhandskrav

Den här guiden kräver att du har [Data Distiller](../data-distiller/overview.md) som en del av ditt paketerbjudande. Om du är osäker på om du har detta eller inte kan du kontakta din Adobe-representant.

## Skapa en härledd datauppsättning {#create-derived-dataset}

Det första steget i att etablera CLV är att skapa en härledd datauppsättning från datasignaler som hämtats från användaråtgärder. Det här användningsexemplet finns i ett separat dokument om ett lojalitetsprogram för flygbolag. Se guiden för att lära dig hur du [använder frågetjänsten för att skapa decimalbaserade härledda datauppsättningar som kan användas med dina profildata](./deciles-use-case.md). Fullständiga exempel och förklaringar finns i dokumentet som förklarar följande steg:

* Skapa ett schema som tillåter dekorblockering.
* Använd frågetjänsten för att skapa decimaler.
* Generera decimaldatauppsättningar.
* Aktivera schemat för användning i kundprofilen i realtid.
* Skapa ett identitetsnamnutrymme och markera det som primär identifierare.
* Skapa en fråga för att beräkna decimaltal över en uppslagsperiod.

## Utöka datamodellen för insikter och schemalägg uppdateringar {#extend-data-model-and-set-refresh-schedule}

Därefter måste ni skapa en anpassad datamodell eller utöka en befintlig datamodell från Adobe Real-Time CDP för att kunna utnyttja era insikter i CLV-rapporterna. Läs dokumentationen om du vill veta mer om hur du [skapar en datamodell för rapportinsikter med hjälp av frågetjänsten för användning med accelererade lagringsdata och användardefinierade instrumentpaneler](../data-distiller/sql-insights/reporting-insights-data-model.md#build-a-reporting-insights-data-model). Självstudiekursen innehåller följande steg:

* Skapa en modell för att rapportera insikter med Data Distiller.
* Skapa tabeller, relationer och fyll i data.
* Fråga datamodellen för rapportinsikter.
* Utöka er datamodell med datamodellen Real-Time CDP insights.
* Skapa dimensionstabeller för att utöka er modell för rapportinsikter.
* Fråga om datamodell för utökad accelererad butiksrapportering

Läs dokumentationen för Real-Time Customer Data Platform Insights-datamodellen om du vill veta hur du [anpassar dina SQL-frågemallar för att skapa Real-Time CDP-rapporter för dina KPI-användningsfall ](../../dashboards/data-models/cdp-insights-data-model-b2c.md) för marknadsföring och nyckeltal.

Se till att du ställer in ett schema för att uppdatera din anpassade datamodell med en vanlig stängsel. Detta garanterar att data kommer in igen som en del av din inmatningsprocess efter behov och fyller i dina användardefinierade instrumentpaneler. Se guiden [Schemafrågor](../ui/query-schedules.md#create-schedule) för att lära dig hur du ställer in ditt schema.

## Bygg en instrumentpanel för att få insikter {#build-a-custom-dashboard}

Nu när du har skapat en anpassad datamodell är du redo att visualisera dina data med anpassade frågor och användardefinierade dashboards. Mer information om hur du [skapar en anpassad kontrollpanel](../../dashboards/standard-dashboards.md) finns i översikten över användardefinierade kontrollpaneler. Användargränssnittshandboken innehåller information om:

* Skapa en widget.
* Så här använder du widgetens disposition.

Exempel på anpassade CLV-widgetar som använder decimalluckor visas nedan.

![En samling anpassade decimalbaserade CLTV-widgetar.](../images/use-cases/deciles-user-defined-dashboard.png)

## Skapa och aktivera högpresterande målgrupper {#create-and-activate-audiences}

Nästa steg är att skapa en segmentdefinition och generera målgrupper utifrån kundprofildata i realtid. Se användargränssnittsguiden för segmentbyggaren för att lära dig hur du [skapar och aktiverar målgrupper i Experience Platform](../../segmentation/ui/segment-builder.md). Handboken innehåller avsnitt om hur du:

* Skapa segmentdefinitioner med en kombination av attribut, händelser och befintliga målgrupper som byggstenar.
* Använd regelbyggarens arbetsyta och behållare för att styra i vilken ordning segmenteringsreglerna ska köras.
* Visa uppskattningar av er presumtiva målgrupp, så att ni kan justera era segmentdefinitioner efter behov.
* Aktivera alla segmentdefinitioner för schemalagd segmentering.
* Aktivera angivna segmentdefinitioner för direktuppspelningssegmentering.

Det finns också en videosjälvstudiekurs [för segmentbyggaren](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-segments.html) som ger mer information.

## Aktivera er målgrupp för en e-postkampanj {#activate-audience-for-campaign}

När ni har byggt er målgrupp är ni redo att aktivera den till ett mål. Experience Platform har stöd för ett antal e-postleverantörer (ESP) som gör att du kan hantera dina e-postmarknadsföringsaktiviteter, till exempel skicka e-postkampanjer med reklam.

Kontrollera översikten över [e-postmarknadsföringsmål](../../destinations/catalog/email-marketing/overview.md#connect-destination) för en lista över de mål som stöds och som du vill exportera data till (till exempel sidan [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)).

## Se returnerade analysdata från kampanjen {#post-campaign-data-analysis}

Data från källor kan nu [bearbetas stegvis](../key-concepts/incremental-load.md) som en del av en schemalagd uppdatering av din datamodell i det accelererade datalagret. Kundernas svarshändelser kan hämtas in till Adobe Experience Platform när de inträffar eller gruppvis. Datamodellen kan uppdateras en gång eller flera gånger dagligen beroende på dina inställningar eller källanslutningarna. Mer information finns i översikten över API:t för gruppinhämtning [&#128279;](../../ingestion/batch-ingestion/api-overview.md)eller [översikten över direktuppspelning](../../ingestion/streaming-ingestion/overview.md).

När datamodellen har uppdaterats tillhandahåller dina anpassade widgetar meningsfulla signaler som gör att du kan mäta och visualisera kundens livstidsvärde.

![En anpassad widget som visar antalet e-postmeddelanden som öppnas utifrån målgrupp och e-postkampanj.](../images/use-cases/post-activation-and-email-response-kpis.png)

Det finns en mängd visualiseringsalternativ för din anpassade analys.

![Det e-postmeddelande som öppnas av widgeten för kampanjgrupper.](../images/use-cases/email-opened-by-campaign-buckets.png)

Dessa insikter kan i sin tur hjälpa er att utveckla era affärsstrategier för efterföljande kampanjer.

![En samling med fyra anpassade widgetar som detaljerar resultaten av e-postkampanjen.](../images/use-cases/example-widgets.png)

## Nästa steg

Genom att läsa det här dokumentet bör du få en bättre förståelse för hur du kan använda Real-Time Customer Data Platform för att spåra och visualisera kundens livstidsvärde (CLV). Om du vill veta mer om de många användningsfall som hanteras via Query Service och Experience Platform rekommenderar vi att du läser följande dokument:

* [Ett heltäckande exempel på ett övergivet webbläsaranvändningsfall som demonstrerar mångsidigheten och fördelarna med Query Service.](./abandoned-browse.md)
* [Hur man använder frågetjänsten och maskininlärning för att avgöra och filtrera startaktiviteten från besökstrafiken på en äkta webbplats](./bot-filtering.md)
* [Hur ni ska matcha era Experience Platform-data som kombinerar resultat från flera datauppsättningar genom att i princip matcha en valfri sträng.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
