---
title: Attributanalys
description: I det här dokumentet förklaras hur du kan använda Query Service för att skapa en mätningsteknik för marknadsföringseffektivitet som baseras på marknadsattribueringsmodellen för första och sista beröringen.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Attributanalys

Attribution är ett analytiskt koncept som hjälper till att fastställa marknadsföringstaktik som kanaler, erbjudanden och meddelanden som bidrar till affärsförsäljningen eller konverteringarna. Detta koncept utvärderar den kundresa (den process genom vilken en kund interagerar med ett företag för att uppnå ett mål) som resulterar i ett köp eller en värvning baserat på kundens kontaktytor (när som helst där en kund interagerar med ert varumärke). Genom attribueringsanalys kan marknadsförarna bedöma avkastningen på investeringar i de kanaler som kopplar dem till en potentiell kund.

## Komma igång

SQL-exemplen i det här dokumentet är frågor som ofta används med Adobe Analytics-data. Den här självstudiekursen kräver en fungerande förståelse av följande komponenter:

* [Adobe Analytics-källkopplingen för rapportsvitens dataöversikt](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Analysfältmappningsdokumentationen](../../sources/connectors/adobe-applications/mapping/analytics.md) innehåller mer information om hur analysdata hämtas och mappas för användning med frågetjänsten.
* [Attribution IQ - översikt](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=sv-SE)
* [Guiden för Adobe Analytics-panelen Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=sv-SE).

En förklaring av parametrarna i funktionen `OVER()` finns i avsnittet [fönsterfunktioner](../sql/adobe-defined-functions.md#window-functions). [Adobe Marketing och Commerce Term Glossary](https://business.adobe.com/glossary/index.html) kan också användas.

För vart och ett av följande användningsfall anges ett parametriserat SQL-frågeexempel som en mall som du kan anpassa. Ange parametrar där du ser `{ }` i de SQL-exempel som du är intresserad av att utvärdera.

## Mål

I ett attribueringsexempel används Adobe Analytics-data för att hjälpa till att koppla kundåtgärder till ett lyckat resultat. Den här föreningen är en viktig del av förståelsen av de faktorer som påverkar kundupplevelserna. Attributionsanalysdata kan användas för att förstå betydelsen av en kunds kontaktyta under kundresan.

Frågeexemplen i det här dokumentet har stöd för olika användningsexempel för första berörings- och sista beröringsattribuering med olika förfalloinställningar. Den här guiden illustrerar följande viktiga begrepp:

* Första beröringen och sista beröringsattribueringen.
* Första beröring och sista beröringsattribuering med tidsgräns för förfallodatum.
* Första beröring och sista beröringsattribuering med förfallovillkor.

## Parametrar för attributfråga {#attribution-query-parameters}

Tabellen nedan innehåller en beskrivning av parametrarna och deras beskrivningar som används i första beröringen och sista beröringsattribueringsfrågor:

| Parameter | Beskrivning |
|---|---|
| `{TIMESTAMP}` | Tidsstämpelfältet i datauppsättningen. |
| `{CHANNEL_NAME}` | Etiketten för det returnerade objektet. |
| `{CHANNEL_VALUE}` | Kolumnen eller fältet som är målkanalen för frågan. |
| `{EXP_TIMEOUT}` | Tidsfönstret före kanalhändelsen, i sekunder, som frågan söker efter en första beröringshändelse. |
| `{EXP_CONDITION}` | Villkoret som bestämmer kanalens slutpunkt. |
| `{EXP_BEFORE}` | Ett booleskt värde som anger om kanalen går ut före eller efter det angivna villkoret, `{EXP_CONDITION}`, är uppfyllt. Detta är i första hand aktiverat för en sessions förfallovillkor, för att säkerställa att den första beröringen inte väljs från en tidigare session. Som standard är det här värdet inställt på `false`. |

## Frågeresultatkolumnkomponenter {#query-result-column-components}

Resultaten för attribueringsfrågorna anges antingen i kolumnen `first_touch` eller `last_touch`. Kolumnerna består av följande komponenter:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parametrar | Beskrivning |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`, angiven som en etikett i Azure Data Factory (ADF). |
| `{VALUE}` | Värdet från `{CHANNEL_VALUE}` som är den sista beröringen inom det angivna `{EXP_TIMEOUT}`-intervallet |
| `{TIMESTAMP}` | Tidsstämpeln för [!DNL Experience Event] där den senaste beröringen inträffade |
| `{FRACTION}` | Den sista pektens attribuering, uttryckt i decimaltal. |

### Första beröringsattribuering {#first-touch}

Den första beröringsattribueringen ger 100 % av ansvaret för ett lyckat resultat för den initiala kanal som konsumenten stötte på. Det här SQL-exemplet används för att markera den interaktion som ledde till en serie kundåtgärder.

Frågan nedan returnerar det första beröringsattribueringsvärdet och kanalens information i måldatauppsättningen [!DNL Experience Event]. Det returnerar också ett `struct`-objekt för den valda kanalen med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad.

>[!NOTE]
>
>Experience Cloud ID (ECID) kallas även MCID och används även i namnutrymmen.

**Frågesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

En fullständig lista över parametrar som kan vara obligatoriska och deras beskrivningar finns i avsnittet [attribueringsfrågeparametrar](#attribution-query-parameters).

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

I resultaten nedan hämtas den inledande spårningskoden `em:946426` från datamängden [!DNL Experience Event]. Den här spårningskoden tilldelas 100 % (`1.0`) av ansvaret för kundens åtgärder eftersom det var den första interaktionen.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

En beskrivning av resultaten som visas i kolumnen `first_touch` finns i avsnittet [kolumnkomponenter](#query-result-column-components).

### Senaste beröringsattribuering {#second-touch}

Senaste beröringsattribuering ger 100 % av ansvaret för ett lyckat resultat till den sista kanal som konsumenten stötte på. Det här SQL-exemplet används för att markera den slutliga interaktionen i en serie kundåtgärder.

Frågan returnerar det sista beröringsattributvärdet och kanalens detaljer i måldatauppsättningen [!DNL Experience Event]. Det returnerar också ett `struct`-objekt för den valda kanalen med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad.

**Frågesyntax**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

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

I resultaten som visas nedan är spårningskoden i det returnerade objektet den sista interaktionen i varje [!DNL Experience Event]-post. Varje kod tilldelas 100 % (`1.0`) ansvar för kundens åtgärder, eftersom det var den senaste interaktionen.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
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

En beskrivning av resultaten som visas i kolumnen `last_touch` finns i avsnittet [kolumnkomponenter](#query-result-column-components).

### Första beröringsattribuering med förfallovillkor {#first-touch-attribution-with-expiration-condition}

Den här frågan används för att se vilken interaktion som ledde till en serie kundåtgärder inom en del av datamängden [!DNL Experience Event] som bestäms av ett villkor som du väljer.

Frågan returnerar det första beröringsattribueringsvärdet och information för en enskild kanal i måldatauppsättningen [!DNL Experience Event], som går ut efter eller före ett villkor. Det returnerar också ett `struct`-objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

**Frågesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

En fullständig lista över parametrar som kan vara obligatoriska och deras beskrivningar finns i avsnittet [attribueringsfrågeparametrar](#attribution-query-parameters).

**Exempelfråga**

I exemplet nedan registreras ett köp (`commerce.purchases.value IS NOT NULL`) för var och en av de fyra dagar som visas i resultaten (15, 21, 23 och 29 juli), och den inledande spårningskoden för varje dag tilldelas 100 % (`1.0`) ansvar för kundåtgärderna.

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
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
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

En beskrivning av resultaten som visas i kolumnen `first_touch` finns i avsnittet [kolumnkomponenter](#query-result-column-components).

### Första beröringsattribuering med tidsgräns för förfallodatum {#first-touch-attribution-with-expiration-timeout}

Den här frågan används för att hitta den interaktion, inom en viss tidsperiod, som ledde till att kunden slutfördes.

Frågan nedan returnerar det första beröringsattribueringsvärdet och information för en enskild kanal i måldatauppsättningen [!DNL Experience Event] för en angiven tidsperiod. Frågan returnerar ett `struct`-objekt med det första beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

**Frågesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

En fullständig lista över parametrar som kan vara obligatoriska och deras beskrivningar finns i avsnittet [attribueringsfrågeparametrar](#attribution-query-parameters).

**Exempelfråga**

I exemplet som visas nedan är den första beröringen som returneras för varje kundåtgärd den tidigaste interaktionen inom de föregående sju dagarna (expTimeout = 86400 * 7).

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
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

En beskrivning av resultaten som visas i kolumnen `first_touch` finns i avsnittet [kolumnkomponenter](#query-result-column-components).

### Senaste beröringsattribuering med förfallovillkor {#last-touch-attribution-with-expiration-condition}

Den här frågan används för att hitta den senaste interaktionen i en serie kundåtgärder inom en del av datamängden [!DNL Experience Event] som bestäms av ett villkor som du väljer.

Frågan nedan returnerar det sista beröringsattributvärdet och information för en enskild kanal i måldatauppsättningen [!DNL Experience Event], som går ut efter eller före ett villkor. Frågan returnerar ett `struct`-objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

**Frågesyntax**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

En fullständig lista över parametrar som kan vara obligatoriska och deras beskrivningar finns i avsnittet [attribueringsfrågeparametrar](#attribution-query-parameters).

**Exempelfråga**

I exemplet nedan registreras ett köp (`commerce.purchases.value IS NOT NULL`) för var och en av de fyra dagar som visas i resultaten (15, 21, 23 och 29 juli), och den sista spårningskoden varje dag tilldelas 100 % (`1.0`) ansvar för kundåtgärderna.

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
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
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

En beskrivning av resultaten som visas i kolumnen `last_touch` finns i avsnittet [kolumnkomponenter](#query-result-column-components).

### Senaste beröringsattribuering med tidsgräns för förfallodatum {#last-touch-attribution-with-expiration-timeout}

Den här frågan används för att hitta den senaste interaktionen inom ett valt tidsintervall. Frågan returnerar det sista beröringsattributvärdet och detaljer för en enskild kanal i måldatauppsättningen [!DNL Experience Event] för en angiven tidsperiod. Frågan returnerar ett `struct`-objekt med det senaste beröringsvärdet, tidsstämpeln och attribueringen för varje rad som returneras för den valda kanalen.

**Frågesyntax**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

En fullständig lista över parametrar som kan vara obligatoriska och deras beskrivningar finns i avsnittet [attribueringsfrågeparametrar](#attribution-query-parameters).

**Exempelfråga**

I exemplet som visas nedan är den sista beröringen som returneras för varje kundåtgärd den slutliga interaktionen inom de följande sju dagarna (`expTimeout = 86400 * 7`).

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

En beskrivning av resultaten som visas i kolumnen `last_touch` finns i avsnittet [kolumnkomponenter](#query-result-column-components).
