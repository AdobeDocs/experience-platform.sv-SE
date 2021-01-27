---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: Adobe-definierade funktioner
topic: functions
description: Det här dokumentet innehåller information om de Adobe-definierade funktioner som är tillgängliga i frågetjänsten.
translation-type: tm+mt
source-git-commit: e15229601d35d1155fc9a8ab9296f8c41811ebf9
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 1%

---


# Adobe-definierade funktioner

Funktioner som definieras av Adobe, och som kallas ADF, är färdiga funktioner i Adobe Experience Platform Query Service som hjälper till att utföra vanliga affärsrelaterade uppgifter på [!DNL Experience Event]-data. Dessa innehåller funktioner för [Sessioner](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) och [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) som de som finns i Adobe Analytics.

Det här dokumentet innehåller information om funktioner som definieras av Adobe i [!DNL Query Service].

## Fönsterfunktioner {#window-functions}

Huvuddelen av affärslogiken kräver att man samlar kontaktytorna för en kund och beställer dem med tiden. Det här stödet tillhandahålls av [!DNL Spark] SQL i form av fönsterfunktioner. Fönsterfunktioner är en del av standard-SQL och stöds av många andra SQL-motorer.

En fönsterfunktion uppdaterar en aggregering och returnerar ett enda objekt för varje rad i den ordnade delmängden. Den mest grundläggande aggregeringsfunktionen är `SUM()`. `SUM()` tar raderna och ger en summa. Om du i stället använder `SUM()` på ett fönster och förvandlar det till en fönsterfunktion, får du en kumulativ summa för varje rad.

Huvuddelen av [!DNL Spark] SQL-hjälpen är fönsterfunktioner som uppdaterar varje rad i fönstret, med radstatus tillagd.

**Frågesyntax**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `{PARTITION}` | En undergrupp med rader som baseras på en kolumn eller ett tillgängligt fält. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | En kolumn eller ett tillgängligt fält som används för att ordna delmängden eller raderna. | `ORDER BY timestamp` |
| `{FRAME}` | En undergrupp av raderna i en partition. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Yrkesställning

När du arbetar med [!DNL Experience Event]-data som kommer från en webbplats, en mobilapp, ett interaktivt röstsvarssystem eller någon annan kundinteraktionskanal, är det bra om händelser kan grupperas runt en relaterad aktivitetsperiod. Vanligtvis har du en specifik avsikt att driva din aktivitet, som att söka efter en produkt, betala en räkning, kontrollera kontosaldot, fylla i ett program och så vidare.

Denna gruppering, eller sammanställning av data, hjälper till att associera händelserna för att hitta mer kontext om kundupplevelsen.

Mer information om sessioner i Adobe Analytics finns i dokumentationen om [kontextmedvetna sessioner](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html.

**Frågesyntax**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{EXPIRATION_IN_SECONDS}` | Antalet sekunder som behövs mellan händelser för att kvalificera slutet av den aktuella sessionen och början av en ny session. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

**Resultat**

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `session`. Kolumnen `session` består av följande komponenter:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametrar | Beskrivning |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Skillnaden i tid, i sekunder, mellan den aktuella posten och den föregående posten. |
| `{NUM}` | Ett unikt sessionsnummer, med början vid 1, för nyckeln som definieras i `PARTITION BY` för fönsterfunktionen. |
| `{IS_NEW}` | Ett booleskt värde som används för att identifiera om en post är den första i en session. |
| `{DEPTH}` | Djupet på den aktuella posten i sessionen. |

### SESS_START_IF

Den här frågan returnerar statusen för sessionen för den aktuella raden, baserat på den aktuella tidsstämpeln och det angivna uttrycket, och startar en ny session med den aktuella raden.

**Frågesyntax**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{TEST_EXPRESSION}` | Ett uttryck som du vill kontrollera datafälten mot. Exempel, `application.launches > 0`. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultat**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `session`. Kolumnen `session` består av följande komponenter:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametrar | Beskrivning |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Skillnaden i tid, i sekunder, mellan den aktuella posten och den föregående posten. |
| `{NUM}` | Ett unikt sessionsnummer, med början vid 1, för nyckeln som definieras i `PARTITION BY` för fönsterfunktionen. |
| `{IS_NEW}` | Ett booleskt värde som används för att identifiera om en post är den första i en session. |
| `{DEPTH}` | Djupet på den aktuella posten i sessionen. |

### SESS_END_IF

Den här frågan returnerar statusen för sessionen för den aktuella raden, baserat på den aktuella tidsstämpeln och det angivna uttrycket, avslutar den aktuella sessionen och startar en ny session på nästa rad.

**Frågesyntax**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{TEST_EXPRESSION}` | Ett uttryck som du vill kontrollera datafälten mot. Exempel, `application.launches > 0`. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Resultat**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `session`. Kolumnen `session` består av följande komponenter:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parametrar | Beskrivning |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Skillnaden i tid, i sekunder, mellan den aktuella posten och den föregående posten. |
| `{NUM}` | Ett unikt sessionsnummer, med början vid 1, för nyckeln som definieras i `PARTITION BY` för fönsterfunktionen. |
| `{IS_NEW}` | Ett booleskt värde som används för att identifiera om en post är den första i en session. |
| `{DEPTH}` | Djupet på den aktuella posten i sessionen. |

## Attribuering

Att koppla kundåtgärder till framgång är en viktig del av förståelsen av de faktorer som påverkar kundupplevelserna. Följande ADF:er har stöd för första-touch-attribuering och sista-touch-attribuering med olika förfalloinställningar.

Mer information om attribuering i Adobe Analytics finns i [Attribution IQ overview](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html) i guiden för panelen [!DNL Analytics] Attribution.

### Första kontakten-attribuering

Den här frågan returnerar det första beröringsattributvärdet och information för en enskild kanal i måldatauppsättningen [!DNL Experience Event]. Frågan returnerar ett `struct`-objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se vilken interaktion som ledde till en serie kundåtgärder. I exemplet som visas nedan tilldelas den initiala spårningskoden (`em:946426`) i [!DNL Experience Event]-data 100 % (`1.0`) ansvar för kundens åtgärder, eftersom det var den första interaktionen.

**Frågesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{CHANNEL_NAME}` | Etiketten för det returnerade objektet. |
| `{CHANNEL_VALUE}` | Kolumnen eller fältet som är målkanalen för frågan. |

En förklaring av parametrarna i `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**Resultat**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `first_touch`. Kolumnen `first_touch` består av följande komponenter:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, som angavs som etikett i ADF. |
| `{VALUE}` | Värdet från `{CHANNEL_VALUE}` som är den första beröringen i [!DNL Experience Event] |
| `{TIMESTAMP}` | Tidsstämpeln för den [!DNL Experience Event] där den första beröringen inträffade. |
| `{FRACTION}` | Den första pektens attribuering, uttryckt i decimaltal. |

### Sista-touch-attribuering

Den här frågan returnerar det sista beröringsattributvärdet och detaljer för en enskild kanal i måldatauppsättningen [!DNL Experience Event]. Frågan returnerar ett `struct`-objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se den slutliga interaktionen i en serie kundåtgärder. I exemplet nedan är spårningskoden i det returnerade objektet den sista interaktionen i varje [!DNL Experience Event]-post. Varje kod tilldelas 100 % (`1.0`) ansvar för kundens åtgärder, eftersom det var den senaste interaktionen.

**Frågesyntax**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{CHANNEL_NAME}` | Det returnerade objektets etikett. |
| `{CHANNEL_VALUE}` | Kolumnen eller fältet som är målkanalen för frågan. |

En förklaring av parametrarna i `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultat**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `last_touch`. Kolumnen `last_touch` består av följande komponenter:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametrar | Beskrivning |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, som angavs som etikett i ADF. |
| `{VALUE}` | Värdet från `{CHANNEL_VALUE}` som är den sista beröringen i [!DNL Experience Event] |
| `{TIMESTAMP}` | Tidsstämpeln för den [!DNL Experience Event] där `channelValue` användes. |
| `{FRACTION}` | Den sista pektens attribuering, uttryckt i decimaltal. |

### Första beröringen-attribuering med förfallovillkor

Den här frågan returnerar det första beröringsattribueringsvärdet och information för en enskild kanal i måldatauppsättningen [!DNL Experience Event], som går ut efter eller före ett villkor. Frågan returnerar ett `struct`-objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se vilken interaktion som ledde till en serie kundåtgärder i en del av [!DNL Experience Event]-datauppsättningen som bestäms av ett villkor som du väljer. I exemplet nedan registreras ett köp (`commerce.purchases.value IS NOT NULL`) för var och en av de fyra dagar som visas i resultaten (15, 21, 23 och 29 juli) och den inledande spårningskoden för varje dag tilldelas 100 % (`1.0`) ansvar för kundens åtgärder.

**Frågesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{CHANNEL_NAME}` | Etiketten för det returnerade objektet. |
| `{CHANNEL_VALUE}` | Kolumnen eller fältet som är målkanalen för frågan. |
| `{EXP_CONDITION}` | Villkoret som bestämmer kanalens slutpunkt. |
| `{EXP_BEFORE}` | Ett booleskt värde som anger om kanalen går ut före eller efter det angivna villkoret `{EXP_CONDITION}` är uppfyllt. Detta är i första hand aktiverat för en sessions förfallovillkor, för att säkerställa att den första beröringen inte väljs från en tidigare session. Som standard är det här värdet `false`. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultat**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `first_touch`. Kolumnen `first_touch` består av följande komponenter:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametrar | Beskrivning |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, som angavs som etikett i ADF. |
| `{VALUE}` | Värdet från `CHANNEL_VALUE}` som är den första beröringen i [!DNL Experience Event], före `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Tidsstämpeln för den [!DNL Experience Event] där den första beröringen inträffade. |
| `{FRACTION}` | Den första pektens attribuering, uttryckt i decimaltal. |

### Första beröringen-attribuering med tidsgräns för förfallodatum

Den här frågan returnerar det första beröringsattributvärdet och information för en enskild kanal i måldatauppsättningen [!DNL Experience Event] för en angiven tidsperiod. Frågan returnerar ett `struct`-objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se vilken interaktion, inom ett valt tidsintervall, som ledde till en kundåtgärd. I exemplet nedan är den första beröringen som returneras för varje kundåtgärd den tidigaste interaktionen inom de föregående sju dagarna (`expTimeout = 86400 * 7`).

**Specifikation**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{CHANNEL_NAME}` | Etiketten för det returnerade objektet. |
| `{CHANNEL_VALUE}` | Kolumnen eller fältet som är målkanalen för frågan. |
| `{EXP_TIMEOUT}` | Tidsfönstret före kanalhändelsen, i sekunder, som frågan söker efter en första beröringshändelse. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultat**

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `first_touch`. Kolumnen `first_touch` består av följande komponenter:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametrar | Beskrivning |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, som angavs som etikett i ADF. |
| `{VALUE}` | Värdet från `CHANNEL_VALUE}` som är den första beröringen inom det angivna `{EXP_TIMEOUT}`-intervallet. |
| `{TIMESTAMP}` | Tidsstämpeln för den [!DNL Experience Event] där den första beröringen inträffade. |
| `{FRACTION}` | Den första pektens attribuering, uttryckt i decimaltal. |

### Senaste-beröring-attribuering med förfallovillkor

Den här frågan returnerar det sista beröringsattributvärdet och detaljer för en enskild kanal i måldatauppsättningen [!DNL Experience Event], som förfaller efter eller före ett villkor. Frågan returnerar ett `struct`-objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se den senaste interaktionen i en serie kundåtgärder i en del av [!DNL Experience Event]-datauppsättningen som bestäms av ett villkor som du väljer. I exemplet nedan registreras ett köp (`commerce.purchases.value IS NOT NULL`) för var och en av de fyra dagar som visas i resultaten (15, 21, 23 och 29 juli) och den sista spårningskoden för varje dag tilldelas 100 % (`1.0`) ansvar för kundens åtgärder.

**Frågesyntax**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{CHANNEL_NAME}` | Etiketten för det returnerade objektet. |
| `{CHANNEL_VALUE}` | Kolumnen eller fältet som är målkanalen för frågan. |
| `{EXP_CONDITION}` | Villkoret som bestämmer kanalens slutpunkt. |
| `{EXP_BEFORE}` | Ett booleskt värde som anger om kanalen går ut före eller efter det angivna villkoret `{EXP_CONDITION}` är uppfyllt. Detta är i första hand aktiverat för en sessions förfallovillkor, för att säkerställa att den första beröringen inte väljs från en tidigare session. Som standard är det här värdet `false`. |

**Exempelfråga**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Exempelresultat**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `last_touch`. Kolumnen `last_touch` består av följande komponenter:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametrar | Beskrivning |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, som angavs som etikett i ADF. |
| `{VALUE}` | Värdet från `{CHANNEL_VALUE}` som är den sista beröringen i [!DNL Experience Event], före `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Tidsstämpeln för den [!DNL Experience Event] där den senaste beröringen inträffade. |
| `{FRACTION}` | Den sista pektens attribuering, uttryckt i decimaltal. |

### Senaste beröringsattribuering med tidsgräns för förfallodatum

Den här frågan returnerar det sista beröringsattributvärdet och detaljer för en enskild kanal i måldatauppsättningen [!DNL Experience Event] för en angiven tidsperiod. Frågan returnerar ett `struct`-objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se den senaste interaktionen inom ett valt tidsintervall. I exemplet nedan är den sista beröringen som returneras för varje kundåtgärd den slutliga interaktionen inom de följande sju dagarna (`expTimeout = 86400 * 7`).

**Frågesyntax**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Tidsstämpelfältet som finns i datauppsättningen. |
| `{CHANNEL_NAME}` | Etiketten för det returnerade objektet |
| `{CHANNEL_VALUE}` | Kolumnen eller fältet som är målkanalen för frågan |
| `{EXP_TIMEOUT}` | Tidsfönstret efter kanalhändelsen (i sekunder) som frågan söker efter en sista beröringshändelse. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultat**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `last_touch`. Kolumnen `last_touch` består av följande komponenter:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametrar | Beskrivning |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, som anges som en etikett i ADF. |
| `{VALUE}` | Värdet från `{CHANNEL_VALUE}` som är den sista beröringen inom det angivna `{EXP_TIMEOUT}`-intervallet |
| `{TIMESTAMP}` | Tidsstämpeln för den [!DNL Experience Event] där den senaste beröringen inträffade |
| `{FRACTION}` | Den sista pektens attribuering, uttryckt i decimaltal. |

## Sökvägsanalys

Målningen kan användas för att förstå kundens engagemang, bekräfta att de tänkta stegen i en upplevelse fungerar som avsett och identifiera potentiella problempunkter som påverkar kunden.

Följande ADF:er har stöd för att skapa sökningsvyer från sina tidigare och nästa relationer. Du kan skapa föregående sidor och nästa sidor, eller stega igenom flera händelser för att skapa en plats.

### Föregående sida

Avgör det föregående värdet för ett visst fält ett definierat antal steg bort i fönstret. Observera i exemplet att funktionen `WINDOW` är konfigurerad med bildrutan `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` som ställer in ADF så att den tittar på den aktuella raden och alla efterföljande rader.

**Frågesyntax**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{KEY}` | Kolumnen eller fältet från händelsen. |
| `{SHIFT}` | (Valfritt) Antalet händelser utanför den aktuella händelsen. Som standard är värdet 1. |
| `{IGNORE_NULLS}` | (Valfritt) Ett booleskt värde som anger om null `{KEY}`-värden ska ignoreras. Som standard är värdet `false`. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Resultat**

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `previous_page`. Värdet i kolumnen `previous_page` baseras på `{KEY}` som används i ADF.

### Nästa sida

Bestämmer nästa värde för ett visst fält med ett definierat antal steg bort i fönstret. Observera i exemplet att funktionen `WINDOW` är konfigurerad med bildrutan `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` som ställer in ADF så att den tittar på den aktuella raden och alla efterföljande rader.

**Frågesyntax**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{KEY}` | Kolumnen eller fältet från händelsen. |
| `{SHIFT}` | (Valfritt) Antalet händelser utanför den aktuella händelsen. Som standard är värdet 1. |
| `{IGNORE_NULLS}` | (Valfritt) Ett booleskt värde som anger om null `{KEY}`-värden ska ignoreras. Som standard är värdet `false`. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**Resultat**

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `previous_page`. Värdet i kolumnen `previous_page` baseras på `{KEY}` som används i ADF.

## Tid mellan

Med tidsintervallet kan ni utforska latent kundbeteende inom en viss tidsperiod före eller efter det att en händelse inträffar.

### Tid mellan föregående matchning

Den här frågan returnerar ett tal som representerar tidsenheten sedan den föregående matchande händelsen sågs. Om ingen matchande händelse hittades returneras null.

**Frågesyntax**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Ett tidsstämpelfält hittades i datauppsättningen ifyllt för alla händelser. |
| `{EVENT_DEFINITION}` | Uttrycket som kvalificerar föregående händelse. |
| `{TIME_UNIT}` | Utdataenheten. Möjligt värde är dagar, timmar, minuter och sekunder. Som standard är värdet sekunder. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

**Resultat**

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `average_minutes_since_registration`. Värdet i kolumnen `average_minutes_since_registration` är skillnaden i tid mellan aktuella och tidigare händelser. Tidsenheten definierades tidigare i `{TIME_UNIT}`.

### Tid mellan nästa matchning

Den här frågan returnerar ett negativt tal som representerar tidsenheten bakom nästa matchande händelse. Om ingen matchande händelse hittas returneras null.

**Frågesyntax**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{TIMESTAMP}` | Ett tidsstämpelfält hittades i datauppsättningen ifyllt för alla händelser. |
| `{EVENT_DEFINITION}` | Uttrycket som kvalificerar nästa händelse. |
| `{TIME_UNIT}` | (Valfritt) Utdataenheten. Möjligt värde är dagar, timmar, minuter och sekunder. Som standard är värdet sekunder. |

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](#window-functions).

**Exempelfråga**

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

**Resultat**

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

För den angivna exempelfrågan anges resultaten i kolumnen `average_minutes_until_order_confirmation`. Värdet i kolumnen `average_minutes_until_order_confirmation` är skillnaden i tid mellan den aktuella och nästa händelsen. Tidsenheten definierades tidigare i `{TIME_UNIT}`.

## Nästa steg

Med funktionerna som beskrivs här kan du skriva frågor för att få tillgång till dina egna [!DNL Experience Event]-datauppsättningar med [!DNL Query Service]. Mer information om hur du skapar frågor i [!DNL Query Service] finns i dokumentationen om [hur du skapar frågor](../best-practices/writing-queries.md).

## Ytterligare resurser

I följande video visas hur du kör frågor i Adobe Experience Platform-gränssnittet och i en PSQL-klient. Dessutom används i videon exempel som omfattar enskilda egenskaper i ett XDM-objekt, som använder Adobe-definierade funktioner och som använder CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)