---
keywords: Experience Platform;frågetjänst;Frågetjänst;kapslade datastrukturer;kapslade data;
title: Arbeta med kapslade datastrukturer i frågetjänsten
description: Det här dokumentet innehåller ett fungerande exempel för bearbetning och omformning av kapslade datafält med hjälp av CTAS- och INSERT INTO-satser.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---

# Arbeta med kapslade datastrukturer i frågetjänsten

Adobe Experience Platform Query Service stöder användning av kapslade datafält. Komplexiteten i företagsdatastrukturerna kan göra det svårt att omforma eller bearbeta data. Det här dokumentet innehåller exempel på hur du skapar, bearbetar eller omformar datauppsättningar med komplexa datatyper, inklusive kapslade datastrukturer.

Frågetjänsten tillhandahåller ett [!DNL PostgreSQL]-gränssnitt för att köra SQL-frågor på alla datauppsättningar som hanteras av Experience Platform. Experience Platform stöder användning av primitiva eller komplexa datatyper i tabellkolumner som struktur, arrayer, kartor och djupt inkapslade strukturer, arrayer och kartor. Datauppsättningar kan också innehålla kapslade strukturer där kolumndatatypen kan vara så komplex som en matris med kapslade strukturer, eller en karta med kartor där värdet för ett nyckelvärdepar kan vara en struktur med flera kapslingsnivåer.

## Komma igång

I den här självstudien måste du använda en PSQL-klient från en annan leverantör eller verktyget Frågeredigeraren för att skriva, validera och köra frågor i Experience Platform användargränssnitt. Fullständig information om hur du kör frågor via användargränssnittet finns i [Användargränssnittsguiden för frågeredigering](../ui/user-guide.md). En detaljerad lista över vilka skrivbordsklienter från tredje part som kan ansluta till frågetjänsten finns i [översikten över klientanslutningar](../clients/overview.md).

Du bör också ha god förståelse för syntaxen `INSERT INTO` och `CTAS`. Specifik information om hur de används finns i avsnitten [`INSERT INTO`](../sql/syntax.md#insert-into) och [`CTAS`](../sql/syntax.md#create-table-as-select) i [referensdokumentationen för SQL-syntax](../sql/syntax.md).

## Skapa en datauppsättning

Frågetjänsten tillhandahåller funktionen Skapa tabell som markerad (`CTAS`) för att skapa en tabell baserat på utdata från en `SELECT` -sats, eller som i det här fallet, genom att använda en referens till ett befintligt XDM-schema i Adobe Experience Platform. Nedan visas XDM-schemat för `Final_subscription` som skapats för det här exemplet.

![Ett diagram över schema för final_subscription.](../images/best-practices/final-subscription-schema.png)

I följande exempel visas det SQL som används för att skapa datauppsättningen `final_subscription_test2`. `final_subscription_test2` skapas med `Final_subscription`-schemat. Data extraheras från källan med en `SELECT`-sats för att fylla i några rader.

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

I den ursprungliga datauppsättningen `final_subscription_test2` används strukturdatatypen för att innehålla både fältet `subscription` och `userid` som är unika för varje användare. Fältet `subscription` beskriver produktprenumerationer för en användare. Det kan finnas flera prenumerationer, men en tabell kan bara innehålla information för en prenumeration per rad.

## Använd INSERT INTO för att uppdatera kapslade datafält

När datauppsättningen `final_subscription_test2` har skapats används programsatsen `INSERT INTO` för att lägga till ytterligare data i tabellen. När data kopieras måste datatyperna i källan och målet matcha. Alternativt måste källdatatypen vara `CAST` för måldatatypen. Inkrementella data läggs sedan till i måldatauppsättningen med följande SQL.

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

Om du vill ta reda på listan över en användares aktiva prenumerationer från en datauppsättning måste du skriva en fråga som avgränsar elementen i en array i flera rader och kolumner. För att kunna göra detta måste du först förstå datamodellens form eftersom prenumerationsinformationen lagras i en array som är kapslad i datamängden.

PSQL-kommandot `\d` används för att navigera nivå efter nivå till nödvändiga prenumerationsdata. Tabellerna visar strukturen för datauppsättningen `final_subscription_test2`. Komplexa datatyper känns igen direkt eftersom de inte är typvärden som text, boolesk, tidsstämpel osv.

| Kolumn | Typ |
|--------|-------|
| `_lumaservices3` | final_subscription_test2_lumaservices3 |

Fälten i nästa kolumn visas med kommandot `\d final_subscription_test2__lumaservices3`.

| Kolumn | Typ |
|---------|-------|
| `userid` | text |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` är en array med strukturelement. Dess fält visas med kommandot `\d _lumaservices3_subscription_e[]`.

| Kolumn | Typ |
|---------|-------|
| `last_eventtime` | tidsstämpel |
| `last_status` | text |
| `offer_id` | text |
| `subscription_id` | text |

Om du vill fråga efter de kapslade fälten i prenumerationen måste du först separera elementen i `subscription`-arrayen i flera rader och returnera resultaten med hjälp av funktionen explodera. Följande SQL-exempel returnerar den aktiva prenumerationen för en användare baserat på `userid`.

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

Trots den ökande komplexiteten i det här SQL-exemplet garanterar inte `collect_list` för aktiva prenumerationer att utdata kommer att vara i samma ordning som källan. Om du vill skapa en lista över aktiva prenumerationer för en användare måste du använda GROUP BY eller blandningfunktionen för att sammanställa resultatet av listan.

## Nästa steg

Genom att läsa det här dokumentet kan du nu förstå hur du bearbetar eller omformar datauppsättningar som använder komplexa datatyper i Adobe Experience Platform Query Service. Mer information om hur du kör SQL-frågor på datamängder i Data Lake finns i [frågekörningsvägledningen](../best-practices/writing-queries.md).
