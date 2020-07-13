---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Query Service
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Översikt över frågetjänsten

Adobe Experience Platform importerar data från en mängd olika källor. En stor utmaning för marknadsförarna är att förstå dessa data för att få insikter om sina kunder. Adobe Experience Platform Query Service underlättar detta genom att du kan använda standard-SQL för att fråga data i Platform. Med hjälp av frågetjänsten kan du ansluta alla datauppsättningar i datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för förtäring i kundprofilen i realtid. Det här dokumentet innehåller en översikt över frågetjänstens roll i Experience Platform.

Med Query Service kan varumärken koppla samman kundresan online-till-offline och förstå flerkanalsattribuering. I följande video visas hur ett upplevelseföretag kan utnyttja frågetjänsten för att hantera viktiga användningsfall och hur frågetjänsten fungerar.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Använda frågetjänsten

Frågetjänsten tillhandahåller ett användargränssnitt och ett RESTful API från vilket du kan skapa SQL-frågor för att bättre analysera dina data. Med användargränssnittet kan du skriva och köra frågor, visa frågor som körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation. Användargränssnittet är avsett att användas som en sandlåda för att testa dina frågor innan de körs på din bredare datauppsättning. Mer information om hur du använder den interaktiva tjänsten i Platform finns i användargränssnittshandboken [för](ui/overview.md)frågetjänsten. RESTful API har en liknande upplevelse, vilket gör att du kan skriva och köra frågor programmatiskt, schemalägga frågor för framtida bruk och upprepning samt skapa mallar för frågor som du vill skriva. Mer information om hur du använder API:t för frågetjänsten finns i utvecklarhandboken [för](api/getting-started.md)frågetjänsten.

## Frågetjänster och Experience Platform

Frågetjänsten samverkar och kan användas tillsammans med flera Experience Platform-tjänster. För att få ut så mycket som möjligt av frågetjänstens funktioner rekommenderar vi att du behärskar dessa tjänster och hur de interagerar med frågetjänsten.

### Datavetenskapens arbetsyta

Adobe Experience Platform Data Science Workspace använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i Experience Platform. Med Data Science Workspace kan datavetare skapa recept baserat på data från register- och tidsserier om kunder och deras aktiviteter, vilket underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen troligtvis uppskattar och använder. Du kan använda SQL i Data Science Workspace genom att integrera Query Service i JupyterLab, så att du kan utforska, omvandla och analysera Adobe Analytics-data. Läs översikten över arbetsytan Data Science Workspace om du vill ha mer information om arbetsytan Data Science och integreringsguiden för Query Service om du vill ha mer information om hur Data Science Workspace interagerar med Query Service.

### Segmenteringstjänst

Med Adobe Experience Platform segmenteringstjänst kan användare dela upp sina kunder i mindre grupper som delar liknande egenskaper. Dessa segment kan därefter utvärderas för att ge en bättre analys av kundprofildata i realtid. Frågetjänsten kan användas för att tillhandahålla den här analysen genom att köra frågor på segmentdata i datasjön. Läs översikten över segmenteringstjänsten för mer information om segmentering och guiden för profilfrågespråk (PQL) för mer information om hur du analyserar segment.

### Användningsexempel för Looker BI

Med Adobe Experience Platform kan ni importera, lagra, strukturera och hämta in alla lagrade datauppsättningar, inklusive beteendedata, CRM-data och butiksdata. Med [!DNL Experience Platform's Query Service]kan ni hämta frågor om dessa datauppsättningar och besvara specifika frågor om verksamheten och sedan börja generera slagkraftiga insikter. I följande video visas värdet av att bygga instrumentpaneler i affärsinformationsverktyg (BI) med [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nästa steg och ytterligare resurser

Genom att läsa det här dokumentet har du lagts till i Query Service och fått veta hur det fungerar i större utsträckning i Experience Platform. Mer information om interaktion med olika slutpunkter i API:t för frågetjänsten finns i [Utvecklarhandboken](api/getting-started.md)för frågetjänsten. Mer information om hur du använder den interaktiva tjänsten i Platform finns i användargränssnittshandboken [för](ui/overview.md)frågetjänsten. En omfattande lista över hur du ansluter externa klienter med Query Service finns i [Query Service-klientöversikten](clients/overview.md).

Titta på följande video om du vill förbereda dig för att köra frågor. I den här videon får du tips och tips om hur du kan köra frågor i frågeredigeringsgränssnittet, PSQL-klienter, Business Intelligence-lösningar (BI) och HTTP API.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
