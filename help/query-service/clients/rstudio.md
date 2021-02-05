---
keywords: Experience Platform;home;populära topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Anslut RStudio till frågetjänsten
topic: connect
description: Det här dokumentet går igenom stegen för att ansluta R Studio med Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# Anslut [!DNL RStudio] till frågetjänsten

Det här dokumentet går igenom stegen för att ansluta [!DNL RStudio] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL RStudio] och är bekant med hur du använder den. Mer information om [!DNL RStudio] finns i [officiell [!DNL RStudio] dokumentation](https://rstudio.com/products/rstudio/).

## Skapa en [!DNL Query Service]-anslutning i gränssnittet [!DNL RStudio]

När du har installerat [!DNL RStudio] måste du först förbereda R-skriptet för att använda [!DNL PostgreSQL] på skärmen **[!DNL Console]**.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

När du har förberett R-skriptet att använda [!DNL PostgreSQL] kan du nu ansluta [!DNL RStudio] till [!DNL Query Service] genom att läsa in drivrutinen [!DNL PostgreSQL].

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{DATABASE_NAME}` | Namnet på den databas som ska användas. |
| `{HOST_NUMBER` och `{PORT_NUMBER}` | Värdslutpunkten och dess port för Query Service. |
| `{USERNAME}` och `{PASSWORD}` | De inloggningsuppgifter som ska användas. Användarnamnet har formatet `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>Mer information om hur du hittar databasnamn, värd, port och inloggningsuppgifter finns på sidan [inloggningsuppgifter på Platform](https://platform.adobe.com/query/configuration). Logga in på [!DNL Platform] och välj **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina inloggningsuppgifter.

## Skriver frågor

Nu när du har anslutit till [!DNL Query Service] kan du skriva frågor för att köra och redigera SQL-satser. Du kan till exempel använda `dbGetQuery(con, sql)` för att köra frågor, där `sql` är den SQL-fråga som du vill köra.

Följande fråga använder en datauppsättning som innehåller [Experience Events](../best-practices/experience-event-queries.md) och skapar ett histogram med sidvyer för en webbplats utifrån enhetens skärmhöjd.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

Ett svar returnerar resultatet av frågan:

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

## Nästa steg

Mer information om hur du skriver och kör frågor finns i guiden [kör frågor](../best-practices/writing-queries.md).