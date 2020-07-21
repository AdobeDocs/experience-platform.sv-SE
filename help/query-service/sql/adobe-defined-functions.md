---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe-definierade funktioner
topic: functions
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 2%

---


# Adobe-definierade funktioner

Adobe-definierade funktioner (ADF) är färdiga funktioner i [!DNL Query Service] vilka man utför vanliga affärsrelaterade [!DNL ExperienceEvent] datauppgifter. Bland dessa finns funktioner för professionalisering och Attribution som liknar de som finns i Adobe Analytics. Läs [Adobe Analytics-dokumentationen](https://docs.adobe.com/content/help/sv-SE/analytics/landing/home.html) om du vill ha mer information om Adobe Analytics och begreppen bakom de ADF:er som finns definierade på den här sidan. Det här dokumentet innehåller information om de Adobe-definierade funktionerna som finns i [!DNL Query Service].

## Fönsterfunktioner

Huvuddelen av affärslogiken kräver att man samlar kontaktytorna för en kund och beställer dem med tiden. Det här stödet tillhandahålls av [!DNL Spark] SQL i form av fönsterfunktioner. Fönsterfunktioner är en del av standard-SQL och stöds av många andra SQL-motorer.

En fönsterfunktion uppdaterar en aggregering och returnerar ett enda objekt för varje rad i den ordnade delmängden. Den mest grundläggande aggregeringsfunktionen är `SUM()`. `SUM()` tar raderna och ger en summa. Om du i stället använder `SUM()` ett fönster och förvandlar det till en fönsterfunktion, får du en kumulativ summa för varje rad.

Huvuddelen av hjälpen i SQL- [!DNL Spark] programmet är fönsterfunktioner som uppdaterar varje rad i fönstret, med radstatus tillagd.

### Specifikation

Syntax: `OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| [partition] | En undergrupp av raderna som baseras på en kolumn eller ett tillgängligt fält. Exempel, `PARTITION BY endUserIds._experience.mcid.id` |
| [order] | En kolumn eller ett tillgängligt fält som används för att ordna delmängden eller raderna. Exempel, `ORDER BY timestamp` |
| [frame] | En undergrupp av raderna i en partition. Exempel, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Yrkesställning

När du arbetar med [!DNL ExperienceEvent] data som kommer från en webbplats, en mobilapp, ett interaktivt röstsvarssystem eller någon annan kundinteraktionskanal är det bra om händelser kan grupperas runt en relaterad aktivitetsperiod. Vanligtvis har du en specifik avsikt att driva din aktivitet, som att söka efter en produkt, betala en räkning, kontrollera kontosaldot, fylla i ett program och så vidare. Den här grupperingen hjälper till att associera händelserna för att hitta mer kontext om kundupplevelsen.

Mer information om sessioner i Adobe Analytics finns i dokumentationen om [sammanhangsberoende sessioner](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

### Specifikation

Syntax: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen |
| `expirationInSeconds` | Antal sekunder mellan händelser som krävs för att kvalificera slutet av den aktuella sessionen och början av en ny session |

| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `timestamp_diff` | Tid i sekunder mellan aktuell post och föregående post |
| `num` | Ett unikt sessionsnummer, med början vid 1, för nyckeln som definieras i `PARTITION BY` fönsterfunktionen. |
| `is_new` | Ett booleskt värde som används för att identifiera om en post är den första i en session |
| `depth` | Djup på den aktuella posten i sessionen |

#### Exempelfråga

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

#### Resultat

```
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

## Attribuering

Att knyta kundåtgärder till framgång är en viktig del av att förstå de faktorer som påverkar kundupplevelsen. Följande ADF:er har stöd för första och sista attributet med olika förfalloinställningar.

Mer information om attribuering i Adobe Analytics finns i [Attribution IQ overview](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/panels/attribution.html) i [!DNL Analytics] Analyze Guide.

### Första beröringsattribuering

Returnerar det första beröringsattribueringsvärdet och detaljer för en enskild kanal i måldatauppsättningen [!DNL ExperienceEvent] . Frågan returnerar ett `struct` objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se vilken interaktion som ledde till en serie kundåtgärder. I exemplet nedan tilldelas den inledande spårningskoden (`em:946426`) i [!DNL ExperienceEvent] data 100 % (`1.0`) ansvar för kundens åtgärder när det var den första interaktionen.

### Specifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen |
| `channelName` | Ett eget namn som ska användas som etikett i det returnerade objektet |
| `channelValue` | Kolumnen eller fältet som är målkanalen för frågan |


| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `name` | Den `channelName` som anges som en etikett i ADF |
| `value` | Värdet från `channelValue` det är den första beröringen i [!DNL ExperienceEvent] |
| `timestamp` | Tidsstämpeln för den [!DNL ExperienceEvent] plats där den första beröringen inträffade |
| `fraction` | Tilldelning av den första kontakten uttryckt som fraktionskredit |

#### Exempelfråga

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

#### Resultat

```
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

### Senaste beröringsattribuering

Returnerar det sista beröringsattribueringsvärdet och detaljer för en enskild kanal i måldatauppsättningen. [!DNL ExperienceEvent] Frågan returnerar ett `struct` objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se den slutliga interaktionen i en serie kundåtgärder. I exemplet nedan är spårningskoden i det returnerade objektet den sista interaktionen i varje [!DNL ExperienceEvent] post. Varje kod tilldelas 100 % (`1.0`) ansvar för kundens åtgärder när det var den senaste interaktionen.

### Specifikation

Syntax: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen |
| `channelName` | Ett eget namn som ska användas som etikett i det returnerade objektet |
| `channelValue` | Kolumnen eller fältet som är målkanalen för frågan |


| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `name` | Den `channelName` som anges som en etikett i ADF |
| `value` | Värdet från `channelValue` det är den sista beröringen i [!DNL ExperienceEvent] |
| `timestamp` | Tidsstämpeln för den [!DNL ExperienceEvent] plats där `channelValue` användes |
| `fraction` | Tilldelning av den senaste beröringen uttryckt som fraktionskredit |

#### Exempelfråga

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

#### Resultat

```
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

### Första beröringsattribuering med förfallovillkor

Returnerar det första beröringsattribueringsvärdet och information för en enskild kanal i måldatauppsättningen, som [!DNL ExperienceEvent] förfaller efter eller före ett villkor. Frågan returnerar ett `struct` objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

Den här frågan är användbar om du vill se vilken interaktion som ledde till en serie kundåtgärder inom en del av [!DNL ExperienceEvent] datauppsättningen som bestäms av ett villkor i valet. I exemplet nedan registreras ett köp (`commerce.purchases.value IS NOT NULL`) för var och en av de fyra dagar som visas i resultaten (15, 21, 23 och 29 juli) och den inledande spårningskoden för varje dag tilldelas 100 % (`1.0`) ansvar för kundens åtgärder.

#### Specifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen |
| `channelName` | Ett eget namn som ska användas som etikett i det returnerade objektet |
| `channelValue` | Kolumnen eller fältet som är målkanalen för frågan |
| `expCondition` | Villkoret som bestämmer kanalens slutpunkt |
| `expBefore` | Defaults to `false`. Boolesk för att ange om kanalen går ut före eller efter att det angivna villkoret är uppfyllt. Primiärt aktiverat för ett sessionsförfallovillkor (till exempel `sess.depth = 1, true`) för att säkerställa att den första beröringen inte väljs från en tidigare session. |

| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `name` | Den `channelName` som anges som en etikett i ADF |
| `value` | Värdet från `channelValue` det som är den första beröringen i [!DNL ExperienceEvent] föregående `expCondition` |
| `timestamp` | Tidsstämpeln för den [!DNL ExperienceEvent] plats där den första beröringen inträffade |
| `fraction` | Tilldelning av den första kontakten uttryckt som fraktionskredit |

#### Exempelfråga

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

#### Resultat

```
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

### Första beröringsattribuering med tidsgräns för förfallodatum

Returnerar det första beröringsattribueringsvärdet och detaljer för en enskild kanal i måldatauppsättningen [!DNL ExperienceEvent] för en angiven tidsperiod. Frågan returnerar ett `struct` objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen. Den här frågan är användbar om du vill se vilken interaktion, inom ett valt tidsintervall, som ledde till en kundåtgärd. I exemplet nedan är den första beröringen som returneras för varje kundåtgärd den tidigaste interaktionen inom de föregående sju dagarna (`expTimeout = 86400 * 7`).

#### Specifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen |
| `channelName` | Ett eget namn som ska användas som etikett i det returnerade objektet |
| `channelValue` | Kolumnen eller fältet som är målkanalen för frågan |
| `expTimeout` | Tidsfönstret (i sekunder) före den kanalhändelse som frågan söker efter en första beröringshändelse |

| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `name` | Den `channelName` som anges som en etikett i ADF |
| `value` | Värdet från `channelValue` den första beröringen inom det angivna `expTimeout` intervallet |
| `timestamp` | Tidsstämpeln för den [!DNL ExperienceEvent] plats där den första beröringen inträffade |
| `fraction` | Tilldelning av den första kontakten uttryckt som fraktionskredit |

#### Exempelfråga

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

#### Resultat

```
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

### Senaste beröringsattribuering med förfallovillkor

Returnerar det sista beröringsattribueringsvärdet och information för en enskild kanal i måldatauppsättningen, [!DNL ExperienceEvent] som förfaller efter eller före ett villkor. Frågan returnerar ett `struct` objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen. Den här frågan är användbar om du vill se den senaste interaktionen i en serie kundåtgärder inom en del av [!DNL ExperienceEvent] datauppsättningen som bestäms av ett villkor i valet. I exemplet nedan registreras ett köp (`commerce.purchases.value IS NOT NULL`) för var och en av de fyra dagar som visas i resultaten (15, 21, 23 och 29 juli) och den sista spårningskoden varje dag tilldelas 100 % (`1.0`) ansvar för kundens åtgärder.

#### Specifikation

Syntax: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen |
| `channelName` | Ett eget namn som ska användas som etikett i det returnerade objektet |
| `channelValue` | Kolumnen eller fältet som är målkanalen för frågan |
| `expCondition` | Villkoret som bestämmer kanalens slutpunkt |
| `expBefore` | Defaults to `false`. Boolesk för att ange om kanalen går ut före eller efter att det angivna villkoret är uppfyllt. Aktiveras främst för sessionens förfallovillkor (till exempel `sess.depth = 1, true`) för att säkerställa att den senaste beröringen inte väljs från en tidigare session. |

| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `name` | Den `channelName` som anges som en etikett i ADF |
| `value` | Värdet från `channelValue` det som är den sista beröringen i [!DNL ExperienceEvent] början av `expCondition` |
| `timestamp` | Tidsstämpeln för den [!DNL ExperienceEvent] plats där den senaste beröringen inträffade |
| `percentage` | Tilldelning av den senaste beröringen uttryckt som fraktionskredit |

#### Exempelfråga

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

#### Resultat

```
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

### Senaste beröringsattribuering med tidsgräns för förfallodatum

Returnerar det sista beröringsattribueringsvärdet och detaljer för en enskild kanal i måldatauppsättningen [!DNL ExperienceEvent] för en angiven tidsperiod. Frågan returnerar ett `struct` objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen. Den här frågan är användbar om du vill se den senaste interaktionen inom ett valt tidsintervall. I exemplet nedan är den sista beröringen som returneras för varje kundåtgärd den slutliga interaktionen inom de följande sju dagarna (`expTimeout = 86400 * 7`).

#### Specifikation

Syntax: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen |
| `channelName` | Ett eget namn som ska användas som etikett i det returnerade objektet |
| `channelValue` | Kolumnen eller fältet som är målkanalen för frågan |
| `expTimeout` | Tidsfönstret (i sekunder) efter den kanalhändelse som frågan söker efter en senaste beröringshändelse |

| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `name` | Den `channelName` som anges som en etikett i ADF |
| `value` | Värdet från `channelValue` det som är den sista beröringen inom det angivna `expTimeout` intervallet |
| `timestamp` | Tidsstämpeln för den [!DNL ExperienceEvent] plats där den senaste beröringen inträffade |
| `percentage` | Tilldelning av den senaste beröringen uttryckt som fraktionskredit |

#### Exempelfråga

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

#### Resultat

```
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

## Föregående/nästa beröring

Det är viktigt att förstå hur kunderna navigerar i en upplevelse. Det kan användas för att förstå kundens engagemang, bekräfta de tänkta stegen i en upplevelse som fungerar som avsett och identifiera potentiella problempunkter som påverkar kunden. Följande ADF:er har stöd för att skapa sökningsvyer från sina tidigare och nästa relationer. Du kan skapa Föregående sida och Nästa sida, eller stega dig igenom flera händelser för att skapa Pathing.

### Föregående beröring

Avgör det föregående värdet för ett visst fält ett definierat antal steg bort i fönstret. Observera i exemplet att `WINDOW` Funktionen är konfigurerad med en bildruta där ADF `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` ställs in så att den tittar på den aktuella raden och alla före den.

#### Specifikation

Syntax: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `key` | Kolumnen eller fältet från händelsen. |
| `shift` | (valfritt) Antalet händelser utanför den aktuella händelsen. Standardvärdet är 1. |
| `ingnoreNulls` | Boolean som ska anges om null- `key` värden ska ignoreras. Standardvärdet är `false`. |


| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `value` | Värdet baseras på det `key` som används i ADF |

#### Exempelfråga

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### Resultat

```
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

### Nästa beröring

Bestämmer nästa värde för ett visst fält med ett definierat antal steg bort i fönstret. Observera i exemplet att `WINDOW` Funktionen är konfigurerad med en bildruta där ADF `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` ställs in så att den tittar på den aktuella raden och allt efter den.

#### Specifikation

Syntax: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `key` | Kolumnen eller fältet från händelsen |
| `shift` | (valfritt) Antalet händelser utanför den aktuella händelsen. Standardvärdet är 1. |
| `ingnoreNulls` | Boolean som ska anges om null- `key` värden ska ignoreras. Standardvärdet är `false`. |


| Returnerade objektparametrar | Beskrivning |
| ---------------------- | ------------- |
| `value` | Värdet baseras på det `key` som används i ADF |

#### Exempelfråga

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### Resultat

```
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

## Tid mellan

Med tidsintervallet kan ni utforska latent kundbeteende inom en period före eller efter det att en händelse inträffar. Titta på händelserna inom 7 dagar efter en kampanj eller en annan typ av händelse för alla era kunder.

### Tid mellan föregående matchning

Ger en ny dimension som mäter den tid som har gått sedan en viss incident.

#### Specifikation

Syntax: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen som fyllts i för alla händelser. |
| `eventDefintion` | Uttryck som kvalificerar föregående händelse. |
| `timeUnit` | Utdataenhet: dagar, timmar, minuter och sekunder. Standard är sekunder. |

Utdata: Returnerar ett tal som representerar tidsenheten sedan den föregående matchande händelsen sågs eller förblir null om ingen matchande händelse hittades.

#### Exempelfråga

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

#### Resultat

```
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

### Tid mellan nästa matchning

Ger en ny dimension som mäter tiden innan en viss händelse inträffar.

#### Specifikation

Syntax: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parameter | Beskrivning |
| --- | --- |
| `timestamp` | Tidsstämpelfält hittades i datauppsättningen som fyllts i för alla händelser. |
| `eventDefintion` | Uttryck för att kvalificera nästa händelse. |
| `timeUnit` | Utdataenhet: dagar, timmar, minuter och sekunder. Standard är sekunder. |

Utdata: Returnerar ett negativt tal som representerar tidsenheten bakom nästa matchande händelse eller förblir null om ingen matchande händelse hittas.

#### Exempelfråga

```
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

#### Resultat

```
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

## Nästa steg

Med funktionerna som beskrivs här kan du skriva frågor för att få tillgång till dina egna [!DNL ExperienceEvent] datauppsättningar med [!DNL Query Service]. Mer information om hur du skapar frågor i [!DNL Query Service]finns i dokumentationen om hur du [skapar frågor](../creating-queries/creating-queries.md).
