---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anslut till Power BI
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Anslut med Power BI (PC)

Datoranvändare kan installera Power BI från [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/).

## Konfigurera Power BI

När du har installerat Power BI måste du konfigurera de komponenter som behövs för att stödja PostgreSQL-anslutningen. Följ de här stegen:

- Hitta och installera `npgsql`ett .NET-drivrutinspaket för PostgreSQL som är det officiella sättet för PowerBI att ansluta.

- Välj v4.0.10 (nyare versioner ger för närvarande ett fel).

- Under &quot;Installation av Npgsql GAC&quot; på skärmen Custom Setup (Anpassade inställningar) väljer du **Will vara installerad på den lokala hårddisken**. Om du inte installerar GAC kommer Power BI att misslyckas senare.

- Starta om Windows.

- Hitta utvärderingsversionen av PowerBI Desktop.

## Anslut Power BI till frågetjänsten

När du har utfört dessa förberedande steg kan du ansluta Power BI till frågetjänsten:

- Öppna Power BI.

- Klicka på **Hämta data** på menyfliksområdet på den översta menyn.

- Välj **PostgreSQL-databas** och klicka sedan på **Anslut**.

- Ange värden för servern och databasen. **Server** är den värddator som finns under anslutningsinformationen. För produktion lägger du till port `:80` i slutet av värdsträngen. **Databasen** kan antingen vara &quot;all&quot; eller ett datamängdstabellnamn. (Prova någon av de CTAS-härledda datauppsättningarna.)

- Klicka på **Avancerade alternativ** och avmarkera sedan **Inkludera relationskolumner**. Kontrollera inte **Navigera med fullständig hierarki**.

- *(Valfritt men rekommenderas när&quot;all&quot; deklareras för databasen)* Ange en SQL-sats.

>[!NOTE]
>
>Om ingen SQL-sats anges förhandsgranskar Power BI alla tabeller i databasen. För hierarkiska data bör en anpassad SQL-sats användas. Om tabellschemat är platt kommer det att fungera med eller utan en anpassad SQL-sats. Sammansatta typer stöds ännu inte av Power BI - för att hämta primitiva typer från sammansatta typer måste du skriva SQL-satser för att härleda dem.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Välj **läget DirectQuery** eller **Import** . I **importläget** importeras data i Power BI. I **DirectQuery** -läge skickas alla frågor till Query Service för körning.

- Klicka på **OK**. Power BI ansluter nu till frågetjänsten och skapar en förhandsgranskning om det inte finns några fel. Det finns ett känt fel med återgivningen av numeriska kolumner i förhandsvisningen. Gå vidare till nästa steg.

- Klicka på **Läs in** för att hämta datauppsättningen till Power BI.
