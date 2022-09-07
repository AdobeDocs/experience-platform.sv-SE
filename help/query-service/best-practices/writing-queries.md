---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;skriva frågor;skriva fråga;
solution: Experience Platform
title: Allmänna riktlinjer för frågekörning i frågetjänsten
topic-legacy: queries
type: Tutorial
description: Det här dokumentet innehåller viktiga detaljer som du bör känna till när du skriver frågor i Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 2%

---

# Allmän vägledning för frågekörning i [!DNL Query Service]

Det här dokumentet innehåller viktig information som du bör känna till när du skriver frågor i Adobe Experience Platform [!DNL Query Service].

Detaljerad information om SQL-syntaxen som används i [!DNL Query Service], kan du läsa [SQL-syntaxdokumentation](../sql/syntax.md).

## Frågekörningsmodeller

Adobe Experience Platform [!DNL Query Service] har två modeller för frågekörning: interaktiva och icke-interaktiva. Interaktiv körning används för frågeutveckling och rapportgenerering i verktyg för affärsinformation, medan icke-interaktiv används för större jobb och operativa frågor som en del av ett arbetsflöde för databearbetning.

### Interaktiv frågekörning

Du kan köra frågor interaktivt genom att skicka dem via [!DNL Query Service] Gränssnitt eller [via en ansluten klient](../clients/overview.md). Vid körning [!DNL Query Service] via en ansluten klient, körs en aktiv session mellan klienten och [!DNL Query Service] tills den skickade frågan returneras eller timeout inträffar.

Interaktiv frågekörning har följande begränsningar:

| Parameter | Begränsning |
| --------- | ---------- |
| Timeout för fråga | 10 minuter |
| Maximalt antal rader har returnerats | 50 000 |
| Maximalt antal samtidiga frågor | 5 |

>[!NOTE]
>
>Om du vill åsidosätta den maximala radbegränsningen inkluderar du `LIMIT 0` i din fråga. Frågetidsgränsen på 10 minuter gäller fortfarande.

Som standard returneras resultatet av interaktiva frågor till klienten och är **not** beständig. För att behålla resultaten som en datauppsättning i [!DNL Experience Platform]måste frågan använda `CREATE TABLE AS SELECT` syntax.

### Icke-interaktiv frågekörning

Frågor som skickats via [!DNL Query Service] API körs icke-interaktivt. Icke-interaktivt genomförande innebär att [!DNL Query Service] tar emot API-anropet och kör frågan i den ordning som den tas emot. Icke-interaktiva frågor leder alltid till att en ny datauppsättning skapas i [!DNL Experience Platform] för att ta emot resultaten eller för att infoga nya rader i en befintlig datauppsättning.

## Åtkomst till ett specifikt fält i ett objekt

Om du vill få åtkomst till ett fält i ett objekt i frågan kan du antingen använda punktnotation (`.`) eller hakparenteser (`[]`). Följande SQL-sats använder punktnotation för att gå igenom `endUserIds` objektet ned till `mcid` -objekt.

>[!NOTE]
>
>Experience Cloud ID (ECID) kallas även MCID och används även i namnutrymmen.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Namnet på analystabellen. |

Följande SQL-sats använder hakparenteser för att gå igenom `endUserIds` objektet ned till `mcid` -objekt.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Namnet på analystabellen. |

>[!NOTE]
>
>Eftersom varje notationstyp returnerar samma resultat, beror det på vad du föredrar.

Båda exempelfrågorna ovan returnerar ett förenklat objekt i stället för ett enda värde:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Den returnerade `endUserIds._experience.mcid` -objektet innehåller motsvarande värden för följande parametrar:

- `id`
- `namespace`
- `primary`

När kolumnen bara deklareras ned till objektet returneras hela objektet som en sträng. Om du bara vill visa ID:t använder du:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Citat

Enkla citattecken, dubbla citattecken och bakåtcitattecken kan användas på olika sätt i frågor om frågetjänsten.

### Enkla citattecken

Ett enkelt citattecken (`'`) används för att skapa textsträngar. Den kan till exempel användas i `SELECT` -programsats för att returnera ett statiskt textvärde i resultatet och i `WHERE` -sats för att utvärdera innehållet i en kolumn.

Följande fråga deklarerar ett statiskt textvärde (`'datasetA'`) för en kolumn:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Följande fråga använder en sträng med bara citattecken (`'homepage'`) i WHERE-satsen för att returnera händelser för en viss sida.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### Citattecken

Dubbelt citattecken (`"`) används för att deklarera en identifierare med blanksteg.

I följande fråga används dubbla citattecken för att returnera värden från angivna kolumner när en kolumn innehåller ett blanksteg i sin identifierare:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Citattecken **inte** användas med åtkomst till punktnoteringsfält.

### Bakåtcitat

Bakåtcitat `` ` `` används för att undvika reserverade kolumnnamn **endast** när punktnoteringssyntax används. Till exempel har `order` är ett reserverat ord i SQL, du måste använda citattecken för att komma åt fältet `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Bakåtcitattecken används också för att komma åt ett fält som börjar med en siffra. Till exempel för att komma åt fältet `30_day_value`måste du använda citattecken.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Bakåtcitattecken är **not** behövs om du använder hakparenteser.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Visa tabellinformation

När du har anslutit till frågetjänsten kan du se alla tillgängliga tabeller på plattformen med antingen `\d` eller `SHOW TABLES` kommandon.

### Standardtabellvy

The `\d` -kommandot visar PostgreSQL-standardvyn för listtabeller. Ett exempel på det här kommandots utdata visas nedan:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Detaljerad tabellvy

`SHOW TABLES` är ett anpassat kommando som ger mer detaljerad information om tabellerna. Ett exempel på det här kommandots utdata visas nedan:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Schemainformation

Om du vill visa mer detaljerad information om scheman i tabellen kan du använda `\d {TABLE_NAME}` kommando, där `{TABLE_NAME}` är namnet på tabellen vars schemainformation du vill visa.

I följande exempel visas schemainformationen för `luma_midvalues` tabell, som skulle visas med `\d luma_midvalues`:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Du kan dessutom få mer information om en viss kolumn genom att lägga till namnet på kolumnen till tabellnamnet. Detta skrivs i formatet `\d {TABLE_NAME}_{COLUMN}`.

I följande exempel visas ytterligare information för `web` och anropas med följande kommando: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Sammanfoga datauppsättningar

Du kan sammanfoga flera datauppsättningar för att inkludera data från andra datauppsättningar i din fråga.

Följande exempel skulle ansluta till följande två datauppsättningar (`your_analytics_table` och `custom_operating_system_lookup`) och skapar `SELECT` för de 50 främsta operativsystemen efter antal sidvisningar.

**Fråga**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Resultat**

| Operativsystem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003 och XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## Deduplicering

Frågetjänsten stöder datadeduplicering eller borttagning av dubblettrader från data. Mer information om borttagning av dubbletter finns i [Handbok för borttagning av dubbletter i frågetjänsten](./deduplication.md).

## Tidszonsberäkningar i frågetjänsten

Frågetjänsten standardiserar beständiga data i Adobe Experience Platform med UTC-tidsstämpelformatet. Mer information om hur du översätter dina krav på tidszon till och från en UTC-tidsstämpel finns i [Frågor och svar om hur du ändrar tidszon till och från en UTC-tidsstämpel](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Nästa steg

Genom att läsa det här dokumentet har du fått en del viktiga synpunkter när du skriver frågor med [!DNL Query Service]. Mer information om hur du använder SQL-syntaxen för att skriva egna frågor finns i [SQL-syntaxdokumentation](../sql/syntax.md).

Fler exempel på frågor som kan användas i Query Service finns i följande dokumentation:

- [Analysinsikter](../use-cases/analytics-insights.md)
- [Aktivitetsanalys med Adobe Target](../use-cases/activity-analysis-with-adobe-target.md)
- [Exempelfrågor för ExperienceEvent](../sample-queries/experience-event.md).
