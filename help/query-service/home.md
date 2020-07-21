---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Query Service
topic: overview
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# [!DNL Query Service] översikt

Adobe Experience Platform importerar data från en mängd olika källor. En stor utmaning för marknadsförarna är att förstå dessa data för att få insikter om sina kunder. Adobe Experience Platform underlättar detta genom att du kan använda standard-SQL för att fråga data i [!DNL Query Service] [!DNL Platform]. Med [!DNL Query Service]kan du ansluta alla datauppsättningar i [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för förtäring i [!DNL Real-time Customer Profile]. Det här dokumentet innehåller en översikt över rollen för [!DNL Query Service] i [!DNL Experience Platform].

[!DNL Query Service] gör det möjligt för varumärken att koppla samman kundresan online-till-offline och förstå flerkanalsattribuering. I följande video visas hur ett upplevelseföretag kan utnyttja [!DNL Query Service] för att hantera viktiga användningsfall och hur [!DNL Query Service] fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Använda [!DNL Query Service]

[!DNL Query Service] innehåller ett användargränssnitt och ett RESTful API från vilket du kan skapa SQL-frågor för att bättre analysera dina data. Med användargränssnittet kan du skriva och köra frågor, visa frågor som körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation. Användargränssnittet är avsett att användas som en sandlåda för att testa dina frågor innan de körs på din bredare datauppsättning. Mer information om hur du använder den interaktiva tjänsten i [!DNL Platform] finns i användargränssnittshandboken [för](ui/overview.md)frågetjänsten. RESTful API har en liknande upplevelse, vilket gör att du kan skriva och köra frågor programmatiskt, schemalägga frågor för framtida bruk och upprepning samt skapa mallar för frågor som du vill skriva. Mer information om hur du använder API:t finns i [!DNL Query Service] Utvecklarhandbok [](api/getting-started.md)för frågetjänsten.

## [!DNL Query Service] och [!DNL Experience Platform] tjänster

[!DNL Query Service] interagerar och kan användas tillsammans med flera [!DNL Experience Platform] tjänster. För att du ska få ut så mycket som möjligt av funktionerna rekommenderar vi att du lär dig mer om dessa tjänster och hur de interagerar med [!DNL Query Service's] [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i [!DNL Experience Platform]. [!DNL Data Science Workspace] gör det möjligt för datavetare att bygga recept baserat på uppgifter om register och tidsserier om kunder och deras aktiviteter, vilket underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen sannolikt kommer att uppskatta och använda. Du kan använda SQL inifrån [!DNL Data Science Workspace] genom att integrera [!DNL Query Service] i [!DNL JupyterLab]och utforska, omvandla och analysera Adobe Analytics-data. Läs [!DNL Data Science Workspace] översikten för mer information om [!DNL Data Science Workspace]och [!DNL Query Service] integreringsguiden för mer information om hur [!DNL Data Science Workspace] interagerar med [!DNL Query Service].

### [!DNL Segmentation Service]

Med Adobe Experience Platform [!DNL Segmentation Service] kan användare dela upp sina kunder i mindre grupper som delar liknande egenskaper. Dessa segment kan därefter utvärderas för att ge bättre analys av era [!DNL Real-time Customer Profile] data. [!DNL Query Service] kan användas för att utföra den här analysen genom att köra frågor på segmentdata i [!DNL Data Lake]. Mer information om segmentering finns i översikten och i handboken [!DNL Segmentation Service] [!DNL Profile Query Language] (PQL) finns mer information om hur du analyserar segment.

### Användningsexempel för Looker BI

Med Adobe Experience Platform kan ni importera, lagra, strukturera och hämta in alla lagrade datauppsättningar, inklusive beteendedata, CRM-data och butiksdata. Med [!DNL Experience Platform's Query Service]kan ni hämta frågor om dessa datauppsättningar och besvara specifika frågor om verksamheten och sedan börja generera slagkraftiga insikter. I följande video visas värdet av att bygga kontrollpaneler i affärsinformationsverktyg (BI) med [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nästa steg och ytterligare resurser

Genom att läsa det här dokumentet har du lagts till [!DNL Query Service] och fått veta hur det fungerar i det större omfånget av [!DNL Experience Platform]. Mer information om interaktion med olika slutpunkter i [!DNL Query Service] API:t finns i [Utvecklarhandbok](api/getting-started.md)för frågetjänst. Mer information om hur du använder den interaktiva tjänsten i [!DNL Platform]finns i användargränssnittshandboken [för](ui/overview.md)frågetjänsten. En omfattande lista över hur du ansluter externa klienter med [!DNL Query Service]finns i [Query Service-klientöversikten](clients/overview.md).

Titta på följande video om du vill förbereda dig för att köra frågor. I den här videon får du tips och tips om hur du kan köra frågor i frågeredigeringsgränssnittet, PSQL-klienter, Business Intelligence-lösningar (BI) och HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
