---
keywords: Experience Platform;home;populära topics;query service;Query service;query
solution: Experience Platform
title: Översikt över frågetjänsten
description: Läs mer om frågetjänstens roll i Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Översikt över frågetjänsten

Adobe Experience Platform importerar data från en mängd olika källor. En stor utmaning för marknadsförarna är att förstå dessa data för att få insikter om sina kunder. Om du vill fråga efter data i Experience Platform kan du använda standardtjänsten för SQL och Adobe Experience Platform Query Service. Du kan använda frågetjänsten för att ansluta till valfri datauppsättning i datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för förtäring i [!DNL Real-Time Customer Profile]. Det här dokumentet innehåller en översikt över frågetjänstens roll i Experience Platform.

Med Query Service kan ni koppla samman kundresan online-till-offline och förstå flerkanalsattribueringen för ert varumärke. I följande video visas hur ett upplevelseföretag kan använda frågetjänsten för att hantera viktiga användningsfall och hur frågetjänsten fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Använda frågetjänsten {#usage}

Om du vill analysera dina data skapar och kör du SQL-frågor med antingen användargränssnittet för frågetjänsten eller RESTful API.
Med användargränssnittet för frågetjänsten kan du skriva, köra och schemalägga frågor, visa frågor som körts tidigare och få åtkomst till frågor som sparats av användare i organisationen. Du kan också testa dina frågor innan du kör dem på din bredare datauppsättning med Frågeredigeraren. En översikt över gränssnittsfunktionerna finns i [gränssnittshandboken för frågetjänsten](ui/overview.md).

RESTful API ger en liknande upplevelse. Du kan använda API:t för frågetjänsten för att skriva och köra frågor programmatiskt, skapa och spara mallar för frågor som du vill anpassa eller schemalägga frågor för automatiserad körning. Mer information om hur du använder API:t för frågetjänsten finns i [Utvecklarhandboken för frågetjänsten](api/getting-started.md).

Du rekommenderas att läsa följande dokument för att snabbt komma igång med att använda funktionerna i frågetjänsten:

- [Allmän vägledning för frågekörning](./best-practices/writing-queries.md)
- [SQL-syntax i Query Service](./sql/syntax.md)
- [Skapa härledda datauppsättningar med SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Frågetjänster och Experience Platform-tjänster {#experience-platform-services}

Frågetjänsten samverkar och kan användas med flera Experience Platform-tjänster. För att få ut så mycket som möjligt av frågetjänstens funktioner bör du känna till dessa tjänster och hur de interagerar med frågetjänsten. Landningssidan för [Experience Platform-dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html) innehåller sammanfattningar och länkar till plattformens funktioner.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i Experience Platform. Datavetare kan använda [!DNL Data Science Workspace] för att skapa recept baserat på data från post- och tidsserier om kunder och deras aktiviteter. Dessa recept underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen troligtvis uppskattar och använder. Du kan använda SQL i [!DNL Data Science Workspace] genom att integrera Query Service i [!DNL JupyterLab] för att utforska, omvandla och analysera Adobe Analytics-data. Läs [[!DNL Data Science Workspace] översikten](../data-science-workspace/home.md) och [Anslutningsguiden för Jupyter-anteckningsbok](./clients/jupyter-notebook.md) om du vill ha mer information om hur [!DNL Data Science Workspace] interagerar med frågetjänsten.

### [!DNL Segmentation Service] {#segmentation}

Använd Adobe Experience Platform segmenteringstjänst för att dela upp kunderna i mindre grupper som delar liknande egenskaper. Dessa målgrupper kan sedan utvärderas för att ge en bättre analys av kundprofildata i realtid. Du kan använda frågetjänsten för att köra frågor om dessa målgruppsdata inom datavjön och tillhandahålla analysen. Läs översikten för [segmenteringstjänsten](../segmentation/home.md) och handboken för [[!DNL Profile Query Language] (PQL)](../segmentation/pql/overview.md) om du vill ha mer information om hur du analyserar målgrupper.

## Användningsfall {#use-cases}

Med frågetjänsten får du ett flexibelt sätt att hantera data i många syften. Det kan bland annat minska bördan av segmentering från marknadsförare och bidra till att generera åtgärdbara målgrupper och meningsfulla affärsinsikter. Följande exempel innehåller fler djupgående exempel på möjligheterna med frågetjänsten.

### Adobe Analytics browse-nedläggning {#abandon-browse}

Det här exemplet på [bläddring handlar om att använda Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md)-data för att skapa en viss åtgärdbar målgrupp. Frågetjänsten har komplex logik för segmentering för att beräkna olika anpassade attribut för användning längre fram i kedjan, eller för att avsevärt förenkla hur ni bygger ut era målgrupper.

## Generera insikter med anpassade instrumentpaneler {#custom-dashboards}

Med Adobe Experience Platform kan ni importera, lagra, strukturera och hämta in alla lagrade datauppsättningar, inklusive beteendedata, CRM-data och butiksdata. Med [!DNL Experience Platform's Query Service] kan du fråga om dessa datauppsättningar och besvara specifika frågor om verksamheten och sedan börja generera slagkraftiga insikter. Lär dig hur du skapar och hanterar anpassade instrumentpaneler där du kan skapa, lägga till och redigera anpassade widgetar för att visualisera nyckelvärden med [användardefinierade instrumentpaneler](../dashboards/standard-dashboards.md). Du kan till och med [anpassa dina egna Real-Time CDP-rapporter](../dashboards/data-models/cdp-insights-data-model-b2c.md) för dina marknadsförings- och KPI-användningsfall genom att använda SQL-frågor med Real-Time Customer Data Platform Insights-datamodeller.

## Nästa steg och ytterligare resurser

Genom att läsa det här dokumentet har du lagts till i Query Service och fått veta hur det fungerar i Experience Platform större omfattning. Om du vill fortsätta lära dig mer om funktionerna i frågetjänsten rekommenderar vi att du läser följande dokument:

- [Utvecklarhandboken för frågetjänsten](api/getting-started.md): Mer information om hur du interagerar med olika slutpunkter i API:t för frågetjänsten.
- Användargränssnittshandboken för [frågetjänsten](ui/overview.md): Mer information om hur du använder frågeredigeraren och användargränssnittet.
- [Översikt över frågetjänstklienter](clients/overview.md): En omfattande lista över externa klienter som ska anslutas till frågetjänsten finns.

Titta på följande video om du vill förbereda dig för att köra frågor. I den här videon får du tips och tips om hur du kan köra frågor i frågeredigeringsgränssnittet, PSQL-klienter, Business Intelligence-lösningar (BI) och HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
