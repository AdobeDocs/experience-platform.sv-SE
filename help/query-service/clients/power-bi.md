---
keywords: Experience Platform;home;popular topics;query service;Query service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Anslut till Power BI
topic: connect
description: Det här dokumentet går igenom stegen för att ansluta Power BI med Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Anslut med [!DNL Power BI] (PC)

PC-användare kan installera [!DNL Power BI] från [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Set up [!DNL Power BI]

När du har [!DNL Power BI] installerat måste du konfigurera de komponenter som behövs för att stödja PostgreSQL-kopplingen. Följ de här stegen:

- Hitta och installera `npgsql`ett .NET-drivrutinspaket för PostgreSQL som är det officiella sättet för PowerBI att ansluta.

- Välj v4.0.10 (nyare versioner ger för närvarande ett fel).

- Välj **[!UICONTROL Will be installed on local hard drive]** under Installation av Npgsql GAC på skärmen Anpassade inställningar. Om du inte installerar GAC kommer Power BI att misslyckas senare.

- Starta om Windows.

- Hitta utvärderingsversionen för [!DNL PowerBI] Skrivbordet.

## Anslut [!DNL Power BI] till [!DNL Query Service]

När du har utfört dessa förberedande steg kan du ansluta [!DNL Power BI] till [!DNL Query Service]:

- Öppna [!DNL Power BI].

- Klicka **[!UICONTROL Get Data]** på menyfliksområdet på den översta menyn.

- Välj **[!UICONTROL PostgreSQL database]** och klicka sedan på **[!UICONTROL Connect]**.

- Ange värden för servern och databasen. **[!UICONTROL Server]** är värddatorn som finns under anslutningsinformationen. För produktion lägger du till port `:80` i slutet av värdsträngen. **[!UICONTROL Database]** kan vara antingen&quot;all&quot; eller ett datamängdstabellnamn. (Prova någon av de CTAS-härledda datauppsättningarna.)

- Click **[!UICONTROL Advanced options]**, and then uncheck **[!UICONTROL include relationship columns]**. Kontrollera inte **[!UICONTROL Navigate using full hierarchy]**.

- *(Valfritt men rekommenderas när&quot;all&quot; deklareras för databasen)* Ange en SQL-sats.

>[!NOTE]
>
>Om ingen SQL-sats anges [!DNL Power BI] förhandsvisas alla tabeller i databasen. För hierarkiska data bör en anpassad SQL-sats användas. Om tabellschemat är platt kommer det att fungera med eller utan en anpassad SQL-sats. Sammansatta typer stöds ännu inte av [!DNL Power BI] - för att hämta primitiva typer från sammansatta typer måste du skriva SQL-satser för att härleda dem.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE TIMESTAMP >= to_timestamp('2018-11-20')
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Välj antingen &quot;[!UICONTROL DirectQuery]&quot; eller &quot;[!UICONTROL Import]&quot;. I [!UICONTROL DirectQuery] läget skickas alla frågor till [!DNL Query Service] för körning. I [!UICONTROL Import] läget importeras data i [!DNL Power BI].

- Klicka på **[!UICONTROL OK]**. Ansluter nu [!DNL Power BI] till [!DNL Query Service] och skapar en förhandsgranskning om det inte finns några fel. Det finns ett känt fel med återgivningen av numeriska kolumner i förhandsvisningen. Gå vidare till nästa steg.

- Klicka **[!UICONTROL Load]** för att hämta datauppsättningen till [!DNL Power BI].
