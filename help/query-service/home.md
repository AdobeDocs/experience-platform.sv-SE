---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Fråga
solution: Experience Platform
title: Översikt över frågetjänsten
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över frågetjänstens roll i Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# [!DNL Query Service] översikt

Adobe Experience Platform importerar data från en mängd olika källor. En stor utmaning för marknadsförarna är att förstå dessa data för att få insikter om sina kunder. Adobe Experience Platform [!DNL Query Service] gör det lättare att använda standard-SQL för att fråga data i [!DNL Platform]. Använda [!DNL Query Service]kan du ansluta till valfri datauppsättning i [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för att lägga in [!DNL Real-Time Customer Profile]. Det här dokumentet innehåller en översikt över rollen för [!DNL Query Service] inom [!DNL Experience Platform].

[!DNL Query Service] gör det möjligt för varumärken att koppla samman kundresan online-till-offline och förstå flerkanalsattribuering. I följande video visas hur ett upplevelseföretag kan utnyttja [!DNL Query Service] för att hantera viktiga användningsfall och hur [!DNL Query Service] fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Använda [!DNL Query Service]

[!DNL Query Service] innehåller ett användargränssnitt och ett RESTful API från vilket du kan skapa SQL-frågor för att bättre analysera dina data. Med användargränssnittet kan du skriva och köra frågor, visa frågor som körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation. Användargränssnittet är avsett att användas som en sandlåda för att testa dina frågor innan de körs på din bredare datauppsättning. Mer information om hur du använder den interaktiva tjänsten i [!DNL Platform] finns i [Användargränssnittshandbok för frågetjänsten](ui/overview.md). RESTful API har en liknande upplevelse, vilket gör att du kan skriva och köra frågor programmatiskt, schemalägga frågor för framtida bruk och upprepning samt skapa mallar för frågor som du vill skriva. Mer information om hur du använder [!DNL Query Service] API finns i [Handbok för frågetjänstutvecklare](api/getting-started.md).

## [!DNL Query Service] och [!DNL Experience Platform] tjänster

[!DNL Query Service] interagerar och kan användas tillsammans med flera [!DNL Experience Platform] tjänster. För att få ut så mycket som möjligt av [!DNL Query Service's] vi rekommenderar att du bekanta dig med dessa tjänster och hur de interagerar med [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i [!DNL Experience Platform]. [!DNL Data Science Workspace] gör det möjligt för datavetare att bygga recept baserat på uppgifter om register och tidsserier om kunder och deras aktiviteter, vilket underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen sannolikt kommer att uppskatta och använda. Du kan använda SQL i [!DNL Data Science Workspace] genom integrering [!DNL Query Service] till [!DNL JupyterLab]så att ni kan utforska, omvandla och analysera Adobe Analytics-data. Läs [!DNL Data Science Workspace] översikt för mer information om [!DNL Data Science Workspace]och [!DNL Query Service] integreringsguiden för mer information om hur [!DNL Data Science Workspace] interagerar med [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] gör det möjligt för användare att dela upp sina kunder i mindre grupper som delar liknande egenskaper. Dessa segment kan sedan utvärderas för att ge bättre analys av dina [!DNL Real-Time Customer Profile] data. [!DNL Query Service] kan användas för att tillhandahålla den här analysen genom att köra frågor på segmentdata i [!DNL Data Lake]. Läs [!DNL Segmentation Service] för mer information om segmentering och [!DNL Profile Query Language] (PQL) guide för mer information om hur du analyserar segment.

## Användningsfall

[!DNL Query Service] erbjuder ett flexibelt sätt att hantera data i många syften. Det kan bland annat minska bördan av segmentering från marknadsförare och bidra till att generera åtgärdbara målgrupper och meningsfulla affärsinsikter. Följande exempel innehåller fler djupgående exempel på [!DNL Query Service].

### Adobe Analytics browse-nedläggning

Detta [exempel på övergivna användare centrerar sig på Adobe [!DNL Analytics]](./use-cases/abandoned-browse.md) data för att skapa en viss användbar målgrupp. [!DNL Query Service] använder komplex logik för segmentering för att beräkna olika anpassade attribut för användning längre fram i kedjan, eller för att avsevärt förenkla hur ni bygger upp era segment.

### Kontrollpaneler för Looker BI

Med Adobe Experience Platform kan ni importera, lagra, strukturera och hämta in alla lagrade datauppsättningar - inklusive beteendes-, CRM- och försäljningsdata. Använda [!DNL Experience Platform's Query Service]kan ni fråga om dessa datauppsättningar och besvara specifika frågor om verksamheten och sedan börja generera slagkraftiga insikter. I följande video visas värdet av att bygga instrumentpaneler i BI-verktyg (Business Intelligence) med [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nästa steg och ytterligare resurser

Genom att läsa det här dokumentet har du introducerats till [!DNL Query Service] och hur det fungerar i större utsträckning [!DNL Experience Platform]. Mer information om interaktion med olika slutpunkter i [!DNL Query Service] API, läs [Handbok för frågetjänstutvecklare](api/getting-started.md). Mer information om hur du använder den interaktiva tjänsten i [!DNL Platform], kan du läsa [Användargränssnittshandbok för frågetjänsten](ui/overview.md). En omfattande lista över hur du ansluter externa klienter med [!DNL Query Service], kan du läsa [Översikt över frågetjänstklienter](clients/overview.md).

Titta på följande video om du vill förbereda dig för att köra frågor. I den här videon får du tips och tips om hur du kan köra frågor i frågeredigeringsgränssnittet, PSQL-klienter, Business Intelligence-lösningar (BI) och HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
