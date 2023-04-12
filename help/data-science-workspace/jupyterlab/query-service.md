---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populära topics;query service
solution: Experience Platform
title: Frågetjänst i Jupyter-anteckningsbok
type: Tutorial
description: Med Adobe Experience Platform kan du använda SQL (Structured Query Language) i arbetsytan Data Science genom att integrera Query Service i JupyterLab som standardfunktion. I den här självstudiekursen visas exempel på SQL-frågor för vanliga användningsområden för att utforska, omvandla och analysera Adobe Analytics-data.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# Frågetjänst i Jupyter-anteckningsbok

[!DNL Adobe Experience Platform] I kan du använda SQL (Structured Query Language) i [!DNL Data Science Workspace] genom integrering [!DNL Query Service] till [!DNL JupyterLab] som en standardfunktion.

I den här självstudiekursen visas exempel på SQL-frågor för vanliga användningsområden för att utforska, omvandla och analysera [!DNL Adobe Analytics] data.

## Komma igång

Innan du startar den här självstudiekursen måste du ha följande krav:

- Åtkomst till [!DNL Adobe Experience Platform]. Om du inte har tillgång till en organisation i [!DNL Experience Platform]bör du kontakta systemadministratören innan du fortsätter

- An [!DNL Adobe Analytics] datauppsättning

- En fungerande förståelse för följande viktiga begrepp som används i den här självstudiekursen:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Åtkomst [!DNL JupyterLab] och [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. I [[!DNL Experience Platform]](https://platform.adobe.com), navigera till **[!UICONTROL Notebooks]** från den vänstra navigeringskolumnen. Tillåt ett ögonblick för JupyterLab att läsas in.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Om en ny startflik inte visas automatiskt öppnar du en ny startflik genom att klicka på **[!UICONTROL File]** välj **[!UICONTROL New Launcher]**.

2. På fliken Launcher klickar du på **[!UICONTROL Blank]** i en Python 3-miljö för att öppna en tom anteckningsbok.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3 är för närvarande den enda miljö som stöds för frågetjänsten i bärbara datorer.

3. Klicka på **[!UICONTROL Data]** och dubbelklicka på **[!UICONTROL Datasets]** katalog för att lista alla datauppsättningar.

   ![](../images/jupyterlab/query/dataset.png)

4. Hitta en [!DNL Adobe Analytics] datauppsättning att utforska och högerklicka på listan, klicka på **[!UICONTROL Query Data in Notebook]** för att generera SQL-frågor i den tomma anteckningsboken.

5. Klicka på den första genererade cellen som innehåller funktionen `qs_connect()` och kör den genom att klicka på uppspelningsknappen. Den här funktionen skapar en anslutning mellan din anteckningsboksinstans och [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Kopiera nedåt [!DNL Adobe Analytics] datauppsättningsnamn från den andra genererade SQL-frågan, det blir värdet efter `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Infoga en ny anteckningsbokscell genom att klicka på **+** -knappen.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Kopiera, klistra in och kör följande importsatser i en ny cell. Programsatserna används för att visualisera dina data:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Kopiera och klistra sedan in följande variabler i en ny cell. Ändra deras värden efter behov och kör dem sedan.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`: Ditt namn [!DNL Adobe Analytics] datauppsättning.
   - `target_year`: Det specifika år som måldata kommer från.
   - `target_month`: Den månad som målet kommer från.
   - `target_day`: Den specifika dag som måldata kommer från.

   >[!NOTE]
   >
   >Du kan ändra dessa värden när som helst. När du gör det måste du se till att variablecellen körs för de ändringar som ska tillämpas.

## Fråga dina data {#query-your-data}

Ange följande SQL-frågor i enskilda anteckningsboksceller. Kör en fråga genom att markera i cellen och sedan markera **[!UICONTROL play]** -knappen. Slutförda frågeresultat eller felloggar visas under den körda cellen.

När en anteckningsbok är inaktiv under en längre tid är anslutningen mellan den bärbara datorn och [!DNL Query Service] kan gå sönder. I sådana fall startar du om [!DNL JupyterLab] genom att välja **Starta om** knapp ![knappen starta om](../images/jupyterlab/user-guide/restart_button.png) i det övre högra hörnet bredvid strömknappen.

Anteckningsbokens kärna återställs men cellerna finns kvar. Kör om alla celler för att fortsätta där du slutade.

### Antal besökare per timme {#hourly-visitor-count}

Följande fråga returnerar antalet besökare per timme för ett angivet datum:

#### Fråga

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

I ovanstående fråga finns tidsstämpeln i `WHERE` -satsen är inställd på att vara värdet för `target_year`. Inkludera variabler i SQL-frågor genom att innesluta dem i klammerparenteser (`{}`).

Den första raden i frågan innehåller den valfria variabeln `hourly_visitor`. Frågeresultat lagras i den här variabeln som en Pandas-dataram. Om du lagrar resultat i en dataram kan du senare visualisera frågeresultaten med ett önskat [!DNL Python] paket. Utför följande [!DNL Python] kod i en ny cell för att generera ett stapeldiagram:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### Antal aktiviteter per timme {#hourly-activity-count}

Följande fråga returnerar antalet timåtgärder för ett angivet datum:

#### Förfrågan <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

Om du kör frågan ovan sparas resultaten i `hourly_actions` som en databildruta. Kör följande funktion i en ny cell för att förhandsgranska resultatet:

```python
hourly_actions.head()
```

Ovanstående fråga kan ändras för att returnera antalet timåtgärder för ett angivet datumintervall med hjälp av logiska operatorer i **VAR** -sats:

#### Förfrågan <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

När den ändrade frågan körs sparas resultaten i `hourly_actions_date_range` som en databildruta. Kör följande funktion i en ny cell för att förhandsgranska resultatet:

```python
hourly_actions_date_rage.head()
```

### Antal händelser per besökarsession {#number-of-events-per-visitor-session}

Följande fråga returnerar antalet händelser per besökarsession för ett angivet datum:

#### Förfrågan <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Utför följande [!DNL Python] kod som genererar ett histogram för antalet händelser per besökssession:

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### Populära sidor för en viss dag {#popular-pages-for-a-given-day}

Följande fråga returnerar de tio vanligaste sidorna för ett angivet datum:

#### Förfrågan <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Aktiva användare för en viss dag {#active-users-for-a-given-day}

Följande fråga returnerar de tio mest aktiva användarna för ett angivet datum:

#### Förfrågan <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Aktiva städer efter användaraktivitet {#active-cities-by-user-activity}

Följande fråga returnerar de tio städer som genererar de flesta användaraktiviteter för ett angivet datum:

#### Förfrågan <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Nästa steg

I den här självstudiekursen visas några exempel på hur man använder [!DNL Query Service] in [!DNL Jupyter] bärbara datorer. Följ [Analysera dina data med Jupyter Notebooks](./analyze-your-data.md) självstudiekurs för att se hur liknande åtgärder utförs med SDK för dataåtkomst.
