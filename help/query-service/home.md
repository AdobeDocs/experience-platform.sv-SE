---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Fråga
solution: Experience Platform
title: Översikt över frågetjänsten
topic: overview
description: Det här dokumentet innehåller en översikt över frågetjänstens roll i Experience Platform.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# [!DNL Query Service] översikt

Adobe Experience Platform importerar data från en mängd olika källor. En stor utmaning för marknadsförarna är att förstå dessa data för att få insikter om sina kunder. Adobe Experience Platform [!DNL Query Service] underlättar detta genom att du kan använda standard-SQL för att fråga data i [!DNL Platform]. Med [!DNL Query Service] kan du ansluta till valfri datauppsättning i [!DNL Data Lake] och hämta frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för förtäring i [!DNL Real-time Customer Profile]. Det här dokumentet innehåller en översikt över rollen för [!DNL Query Service] i [!DNL Experience Platform].

[!DNL Query Service] gör det möjligt för varumärken att koppla samman kundresan online-till-offline och förstå flerkanalsattribuering. I följande video visas hur ett upplevelseföretag kan utnyttja [!DNL Query Service] för att hantera viktiga användningsfall och hur [!DNL Query Service] fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Använda [!DNL Query Service]

[!DNL Query Service] innehåller ett användargränssnitt och ett RESTful API från vilket du kan skapa SQL-frågor för att bättre analysera dina data. Med användargränssnittet kan du skriva och köra frågor, visa frågor som körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation. Användargränssnittet är avsett att användas som en sandlåda för att testa dina frågor innan de körs på din bredare datauppsättning. Mer information om hur du använder den interaktiva tjänsten i [!DNL Platform] finns i [Användargränssnittshandboken för frågetjänsten](ui/overview.md). RESTful API har en liknande upplevelse, vilket gör att du kan skriva och köra frågor programmatiskt, schemalägga frågor för framtida bruk och upprepning samt skapa mallar för frågor som du vill skriva. Mer information om hur du använder API:t [!DNL Query Service] finns i [Utvecklarhandbok för frågetjänst](api/getting-started.md).

## [!DNL Query Service] och  [!DNL Experience Platform] tjänster

[!DNL Query Service] interagerar och kan användas tillsammans med flera  [!DNL Experience Platform] tjänster. För att få ut så mycket som möjligt av [!DNL Query Service's]-funktionerna rekommenderar vi att du lär dig mer om dessa tjänster och hur de interagerar med [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i [!DNL Experience Platform]. [!DNL Data Science Workspace] gör det möjligt för datavetare att bygga recept baserat på uppgifter om register och tidsserier om kunder och deras aktiviteter, vilket underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen sannolikt kommer att uppskatta och använda. Du kan använda SQL i [!DNL Data Science Workspace] genom att integrera [!DNL Query Service] i [!DNL JupyterLab], så att du kan utforska, omvandla och analysera Adobe Analytics-data. Läs översikten [!DNL Data Science Workspace] om du vill ha mer information om [!DNL Data Science Workspace] och [!DNL Query Service] integreringsguiden om du vill ha mer information om hur [!DNL Data Science Workspace] interagerar med [!DNL Query Service].

### [!DNL Segmentation Service]

Med Adobe Experience Platform [!DNL Segmentation Service] kan användare dela upp sina kunder i mindre grupper som delar liknande egenskaper. Dessa segment kan därefter utvärderas för att ge en bättre analys av dina [!DNL Real-time Customer Profile]-data. [!DNL Query Service] kan användas för att utföra den här analysen genom att köra frågor på segmentdata i  [!DNL Data Lake]. Läs översikten [!DNL Segmentation Service] om du vill ha mer information om segmentering och guiden [!DNL Profile Query Language] (PQL) om du vill ha mer information om hur du analyserar segment.

### Användningsexempel för Looker BI

Med Adobe Experience Platform kan ni importera, lagra, strukturera och hämta in alla lagrade datauppsättningar - inklusive beteendes-, CRM- och försäljningsdata. Med [!DNL Experience Platform's Query Service] kan du ställa frågor om dessa datauppsättningar och besvara specifika frågor om verksamheten och sedan börja generera slagkraftiga insikter. I följande video visas värdet av att bygga kontrollpaneler i Business Intelligence-verktyg (BI) med [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nästa steg och ytterligare resurser

Genom att läsa det här dokumentet har du introducerats till [!DNL Query Service] och hur det fungerar i det större omfånget [!DNL Experience Platform]. Mer information om interaktion med olika slutpunkter i [!DNL Query Service] API:t finns i [Query Service developer guide](api/getting-started.md). Mer information om hur du använder den interaktiva tjänsten i [!DNL Platform] finns i [Användargränssnittshandboken för frågetjänsten](ui/overview.md). En omfattande lista över hur du ansluter externa klienter med [!DNL Query Service] finns i översikten [Query Service-klienter](clients/overview.md).

Titta på följande video om du vill förbereda dig för att köra frågor. I den här videon får du tips och tips om hur du kan köra frågor i frågeredigeringsgränssnittet, PSQL-klienter, Business Intelligence-lösningar (BI) och HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
