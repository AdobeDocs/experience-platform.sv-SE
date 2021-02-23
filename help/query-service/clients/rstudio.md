---
keywords: Experience Platform;home;populära topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Anslut RStudio till frågetjänsten
topic: koppla
description: Det här dokumentet går igenom stegen för att ansluta R Studio med Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: f1b2fd7efd43f317a85c831cd64c09be29688f7a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Anslut [!DNL RStudio] till frågetjänsten

Det här dokumentet går igenom stegen för att ansluta [!DNL RStudio] med Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL RStudio] och är bekant med hur du använder den. Mer information om [!DNL RStudio] finns i [officiell [!DNL RStudio] dokumentation](https://rstudio.com/products/rstudio/).
> 
> Om du vill använda RStudio med Query Service måste du installera drivrutinen PostgreSQL JDBC 4.2. Du kan hämta JDBC-drivrutinen från den [officiella PostgreSQL-platsen](https://jdbc.postgresql.org/download.html).

## Skapa en [!DNL Query Service]-anslutning i gränssnittet [!DNL RStudio]

När du har installerat [!DNL RStudio] måste du installera RJDBC-paketet. Gå till rutan **[!DNL Packages]** och välj **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

Ett popup-fönster med skärmen **[!DNL Install Packages]** visas. Kontrollera att **[!DNL Repository (CRAN)]** är markerat för **[!DNL Install from]**-avsnittet. Värdet för **[!DNL Packages]** ska vara `RJDBC`. Kontrollera att **[!DNL Install dependencies]** är markerat. När du har bekräftat att alla värden är korrekta väljer du **[!DNL Install]** för att installera paketen.

![](../images/clients/rstudio/install-jrdbc.png)

Nu när RJDBC-paketet har installerats startar du om RStudio för att slutföra installationen.

När RStudio har startats om kan du ansluta till frågetjänsten. Markera **[!DNL RJDBC]**-paketet i rutan **[!DNL Packages]** och ange följande kommando i konsolen:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Där {PATH TO THE POSTGRESQL JDBC JAR} representerar sökvägen till PostgreSQL JDBC JAR som installerades på datorn.

Nu kan du skapa anslutningen till frågetjänsten genom att ange följande kommando i konsolen:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>Mer information om hur du hittar databasnamn, värd, port och inloggningsuppgifter finns på sidan [inloggningsuppgifter på Platform](https://platform.adobe.com/query/configuration). Logga in på [!DNL Platform] och välj **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina inloggningsuppgifter.

![](../images/clients/rstudio/connection-rjdbc.png)

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