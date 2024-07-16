---
keywords: Experience Platform;home;populära topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Anslut RStudio till frågetjänsten
description: Det här dokumentet går igenom stegen för att ansluta R Studio med Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Anslut [!DNL RStudio] till frågetjänsten

Det här dokumentet går igenom stegen för att ansluta [!DNL RStudio] till Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] har nu omklassificerats som [!DNL Posit]. [!DNL RStudio] produkter har bytt namn till [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Manager, [!DNL Posit Cloud] och [!DNL Posit Academy].
>
> Den här handboken förutsätter att du redan har tillgång till [!DNL RStudio] och är bekant med hur du använder den. Mer information om [!DNL RStudio] finns i [officiell [!DNL RStudio] dokumentation](https://rstudio.com/products/rstudio/).
> 
> Om du vill använda [!DNL RStudio] med Query Service måste du installera drivrutinen [!DNL PostgreSQL] JDBC 4.2. Du kan hämta JDBC-drivrutinen från den [[!DNL PostgreSQL] officiella platsen](https://jdbc.postgresql.org/download/).

## Skapa en [!DNL Query Service]-anslutning i gränssnittet [!DNL RStudio]

När du har installerat [!DNL RStudio] måste du installera RJDBC-paketet. Instruktioner om hur du [ansluter en databas via kommandoraden](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) finns i den officiella besöksdokumentationen.

Om du använder ett Mac-operativsystem kan du välja **[!UICONTROL Tools]** på menyraden följt av **[!UICONTROL Install Packages]** på den nedrullningsbara menyn. Du kan också välja fliken **[!DNL Packages]** i användargränssnittet för RStudio och välja **[!DNL Install]**.

Ett popup-fönster med skärmen **[!DNL Install Packages]** visas. Kontrollera att **[!DNL Repository (CRAN)]** är markerat för avsnittet **[!DNL Install from]**. Värdet för **[!DNL Packages]** ska vara `RJDBC`. Kontrollera att **[!DNL Install dependencies]** är markerat. När du har bekräftat att alla värden är korrekta väljer du **[!DNL Install]** för att installera paketen. Nu när RJDBC-paketet har installerats startar du om [!DNL RStudio] för att slutföra installationsprocessen.

När [!DNL RStudio] har startats om kan du ansluta till frågetjänsten. Markera paketet **[!DNL RJDBC]** i rutan **[!DNL Packages]** och ange följande kommando i konsolen:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Där `{PATH TO THE POSTGRESQL JDBC JAR}` representerar sökvägen till den [!DNL PostgreSQL] JDBC JAR som installerades på datorn.

Nu kan du skapa anslutningen till frågetjänsten. Ange följande kommando i konsolen:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Läs [[!DNL Query Service] SSL-dokumentationen](./ssl-modes.md) om du vill veta mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter i SSL-läge `verify-full`.

Mer information om hur du söker efter databasnamn, värd, port och inloggningsuppgifter finns i [referenshandboken](../ui/credentials.md). Logga in på [!DNL Platform] och välj sedan **[!UICONTROL Queries]** följt av **[!UICONTROL Credentials]** för att hitta dina autentiseringsuppgifter.

Ett meddelande i konsolutdata bekräftar anslutningen till frågetjänsten.

## Skriver frågor

Nu när du har anslutit till [!DNL Query Service] kan du skriva frågor för att köra och redigera SQL-satser. Du kan till exempel använda `dbGetQuery(con, sql)` för att köra frågor, där `sql` är den SQL-fråga som du vill köra.

Följande fråga använder en datauppsättning som innehåller [Experience Events](../../xdm/classes/experienceevent.md) och skapar ett histogram med sidvyer för en webbplats utifrån enhetens skärmhöjd.

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

Mer information om hur du skriver och kör frågor finns i guiden för [frågor som körs](../best-practices/writing-queries.md).
