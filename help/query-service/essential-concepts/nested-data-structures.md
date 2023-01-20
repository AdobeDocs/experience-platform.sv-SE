---
keywords: Experience Platform;frågetjänst;frågetjänst;kapslade datastrukturer;kapslade data;
title: Arbeta med kapslade datastrukturer i frågetjänsten
description: Det här dokumentet innehåller ett fungerande exempel för bearbetning och omformning av kapslade datafält med hjälp av CTAS- och INSERT INTO-satser.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Arbeta med kapslade datastrukturer i frågetjänsten

Adobe Experience Platform Query Service stöder användning av kapslade datafält. Komplexiteten i företagsdatastrukturerna kan göra det svårt att omforma eller bearbeta data. Det här dokumentet innehåller exempel på hur du skapar, bearbetar eller omformar datauppsättningar med komplexa datatyper, inklusive kapslade datastrukturer.

Frågetjänsten tillhandahåller en [!DNL PostgreSQL] för att köra SQL-frågor på alla datauppsättningar som hanteras av Experience Platform. Platform stöder användning av antingen primitiva eller komplexa datatyper i tabellkolumner som struktur, arrayer, kartor och djupt inkapslade strukturer, arrayer och kartor. Datauppsättningar kan också innehålla kapslade strukturer där kolumndatatypen kan vara så komplex som en matris med kapslade strukturer, eller en karta med kartor där värdet för ett nyckelvärdepar kan vara en struktur med flera kapslingsnivåer.

## Komma igång

I den här självstudien måste du använda en PSQL-klient från en annan leverantör eller verktyget Frågeredigeraren för att skriva, validera och köra frågor i användargränssnittet i Experience Platform. Mer information om hur du kör frågor via användargränssnittet finns i [Användargränssnittshandbok för frågeredigeraren](../ui/user-guide.md). En detaljerad lista över vilka skrivbordsklienter från tredje part som kan ansluta till frågetjänsten finns i [översikt över klientanslutningar](../clients/overview.md).

Du bör också ha god förståelse för `INSERT INTO` och `CTAS` syntax. Specifik information om hur de används finns i [`INSERT INTO`](../sql/syntax.md#insert-into) och [`CTAS`](../sql/syntax.md#create-table-as-select) avsnitt i [Referensdokumentation för SQL-syntax](../sql/syntax.md).

## Skapa en datauppsättning

Frågetjänsten tillhandahåller Skapa tabell som markerad (`CTAS`) för att skapa en tabell baserat på utdata från en `SELECT` eller som i det här fallet genom att använda en referens till ett befintligt XDM-schema i Adobe Experience Platform. Nedan visas XDM-schemat för `Final_subscription` som har skapats för det här exemplet.

![Ett diagram över schema för final_subscription.](../images/best-practices/final-subscription-schema.png)

I följande exempel demonstreras den SQL som används för att skapa `final_subscription_test2` datauppsättning. `final_subscription_test2` skapas med `Final_subscription` schema. Data extraheras från källan med en `SELECT` -sats för att fylla i några rader.

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

I den första datauppsättningen `final_subscription_test2`används strukturdatatypen för att innehålla båda `subscription` fält och `userid` som är unik för varje användare. The `subscription` beskriver produktprenumerationer för en användare. Det kan finnas flera prenumerationer, men en tabell kan bara innehålla information för en prenumeration per rad.

## Använd INSERT INTO för att uppdatera kapslade datafält

Efter `final_subscription_test2` datauppsättningen har skapats, `INSERT INTO` -programsatsen används för att lägga till ytterligare data i tabellen. När data kopieras måste datatyperna i källan och målet matcha. Alternativt måste källdatatypen vara `CAST` till måldatatypen. Inkrementella data läggs sedan till i måldatauppsättningen med följande SQL.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## Bearbeta data från en kapslad datauppsättning

Om du vill ta reda på listan över en användares aktiva prenumerationer från en datauppsättning måste du skriva en fråga som avgränsar elementen i en array i flera rader och kolumner. För att kunna göra detta måste du först förstå datamodellens form eftersom prenumerationsinformationen lagras i en array som är kapslad i datauppsättningen.

PSQL `\d` används för att navigera nivå för nivå till de prenumerationsdata som krävs. Tabellerna visar strukturen för `final_subscription_test2` datauppsättning. Komplexa datatyper känns igen direkt eftersom de inte är typvärden som text, boolesk, tidsstämpel osv.

| Kolumn | Typ |
|--------|-------|
| `_lumaservices3` | final_subscription_test2_lumaservices3 |

Fälten i nästa kolumn visas med `\d final_subscription_test2__lumaservices3` -kommando.

| Kolumn | Typ |
|---------|-------|
| `userid` | text |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` är en array med strukturelement. Fälten visas med `\d _lumaservices3_subscription_e[]` -kommando.

| Kolumn | Typ |
|---------|-------|
| `last_eventtime` | tidsstämpel |
| `last_status` | text |
| `offer_id` | text |
| `subscription_id` | text |

Om du vill fråga efter de kapslade fälten i prenumerationen måste du först separera elementen i `subscription` matris i flera rader och returnera resultatet med hjälp av exploderingsfunktionen. Följande SQL-exempel returnerar den aktiva prenumerationen för en användare baserat på `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Denna förenklade exempellösning tillåter endast en aktiv användarprenumeration. Det kan finnas många aktiva prenumerationer för en enskild användare. I följande exempel ändras föregående fråga så att flera samtidiga aktiva prenumerationer tillåts.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

Trots den växande komplexiteten i det här SQL-exemplet har `collect_list` för aktiva prenumerationer inte garanterar att utdata kommer att vara i samma ordning som källan. Om du vill skapa en lista över aktiva prenumerationer för en användare måste du använda GROUP BY eller blandningfunktionen för att sammanställa resultatet av listan.

## Nästa steg

Genom att läsa det här dokumentet kan du nu förstå hur du bearbetar eller omformar datauppsättningar som använder komplexa datatyper i Adobe Experience Platform Query Service. Se [körningsvägledning för frågor](../best-practices/writing-queries.md) om du vill ha mer information om hur du kör SQL-frågor på datauppsättningar i Data Lake.
