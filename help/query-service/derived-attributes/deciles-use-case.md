---
title: Använd skiftläge för dekorbaserade härledda attribut
description: Den här guiden visar de steg som krävs för att använda frågetjänsten för att skapa decimalbaserade härledda attribut som kan användas med dina profildata.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 1%

---

# Argumentbaserade härledda attribut använder skiftläge

Härledda attribut underlättar komplicerade användningsfall för att analysera data från datasjön som kan användas tillsammans med andra plattformstjänster längre fram i kedjan eller publiceras i kundprofildata i realtid.

I det här exemplet visas hur du skapar dekorbaserade härledda attribut som kan användas med dina kundprofildata i realtid. Om du använder ett lojalitetsscenario för ett flygbolag som exempel får du information i den här guiden om hur du skapar en datauppsättning som använder kategoriserade deciler för att segmentera och skapa målgrupper baserat på rankade attribut.

Följande viktiga begrepp visas:

* Schema skapas för dekorblockering.
* Skapa kategorisisk decimal.
* Skapande av komplexa härledda attribut.
* Beräkning av deciler över en uppslagsperiod.
* En exempelfråga för att demonstrera aggregering, rankning och lägga till unika identiteter så att målgrupper kan genereras baserat på dessa decimalgrupper.

## Komma igång

Den här guiden kräver en fungerande förståelse av [frågekörning i frågetjänsten](../best-practices/writing-queries.md) och följande komponenter i Adobe Experience Platform:

* [Översikt över kundprofiler i realtid](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Grunderna för schemakomposition](../../xdm/schema/composition.md): En introduktion till XDM-scheman (Experience Data Model) och byggstenar, principer och bästa metoder för att komponera scheman.
* [Så här aktiverar du ett schema för kundprofil i realtid](../../profile/tutorials/add-profile-data.md): I den här självstudien beskrivs de steg som krävs för att lägga till data i kundprofilen i realtid.
* [Definiera en anpassad datatyp](../../xdm/api/data-types.md): Datatyper används som referenstypfält i klasser eller schemafältgrupper och möjliggör konsekvent användning av en flerfältstruktur som kan inkluderas var som helst i schemat.

## Mål

Exemplet i det här dokumentet använder deciler för att skapa härledda attribut för rankningsdata från ett lojalitetsschema för flygbolag. Med härledda attribut kan ni maximera dataanvändningen genom att identifiera en målgrupp baserat på de högsta &#39;n&#39; % för en vald kategori.

## Skapa decimalbaserade härledda attribut

Om du vill definiera decimalernas rangordning baserat på en viss dimension och ett motsvarande mått, måste ett schema utformas så att det går att dekorera spärrning.

I den här guiden används en datauppsättning om flygbolagets lojalitet för att visa hur frågetjänsten kan användas för att skapa deciler baserat på de engelska mil som följer av olika uppslagsperioder.

## Använd frågetjänsten för att skapa decimaler

Med hjälp av frågetjänsten kan du skapa en datauppsättning som innehåller kategoriserade decilar, som sedan kan segmenteras för att skapa målgrupper baserat på attribueringsrankning. De begrepp som visas i följande exempel kan användas för att skapa andra datauppsättningar med decimalintervall, så länge som en kategori definieras och ett mätvärde är tillgängligt.

I exemplet med flygbolagets lojalitetsdata används en [Klassen XDM ExperienceEvents](../../xdm/classes/experienceevent.md). Varje händelse är ett kvitto på en affärstransaktion för milage, antingen krediterad eller debiterad, och medlemskapets lojalitetsstatus för antingen &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; eller &quot;Gold&quot;. Det primära identitetsfältet är `membershipNumber`.

### Exempeldatauppsättningar

Den första datamängden för flygbolagets lojalitet i det här exemplet är&quot;Airline Loyalty Data&quot; och har följande schema. Observera att schemats primära identitet är `_profilefoundationreportingstg.membershipNumber`.

![Ett diagram över Airline Loyalty Data-schemat.](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**Exempeldata**

I följande tabell visas exempeldata i `_profilefoundationreportingstg` som används för det här exemplet. Det ger kontext för användning av decimalluckor för att skapa komplexa härledda attribut.

>[!NOTE]
>
>Klient-ID `_profilefoundationreportingstg` har utelämnats från början av namnutrymmet i kolumnrubrikerna och efterföljande omnämnanden i hela dokumentet.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Ny medlem | 5000 | FLYGER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | SILVER |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nytt kreditkort | 10000 | FLYGER |

{style=&quot;table-layout:auto&quot;}

## Generera decimaldatauppsättningar

I de data om flygbolagets lojalitet som visas ovan `.mileage` Värdet anger antalet engelska mil som en medlem flyger med för varje enskild flygning som utförs. Dessa data används för att skapa deciler för antalet engelska mil som flugit över livslängdslookback och en mängd olika lookback-perioder. För detta ändamål skapas en datauppsättning som innehåller deciler i en kartdatatyp för varje uppslagsperiod och en lämplig decimal för varje uppslagsperiod som tilldelas enligt `membershipNumber`.

Skapa ett&quot;Airline Loyalty Decile Schema&quot; om du vill skapa en decimaldatauppsättning med hjälp av Query Service.

![Ett diagram över&quot;Airline Loyalty Decile Schema&quot;.](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### Aktivera schemat för kundprofil i realtid

Data som hämtas in till Experience Platform för användning av kundprofilen i realtid måste överensstämma med [ett XDM-schema (Experience Data Model) som är aktiverat för profilen](../../xdm/ui/resources/schemas.md). För att ett schema ska kunna aktiveras för profilen måste det implementera antingen klassen XDM Individual Profile eller klassen XDM ExperienceEvent.

[Aktivera schemat för användning i kundprofilen i realtid med API:t för schemaregister](../../xdm/tutorials/create-schema-api.md) eller [Användargränssnittet i Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md).  Detaljerade anvisningar om hur du aktiverar ett schema för profil finns i deras respektive dokumentation.

Skapa sedan en datatyp som ska återanvändas för alla decimalrelaterade fältgrupper. Skapandet av decimalfältgruppen är ett steg per sandlåda. Den kan också återanvändas för alla decimalrelaterade scheman.

### Skapa ett identitetsnamnutrymme och markera det som primär identifierare {#identity-namespace}

Alla scheman som skapas för användning med deciler måste ha en primär identitet tilldelad. Du kan [definiera ett identitetsfält i användargränssnittet för Adobe Experience Platform-scheman](../../xdm/ui/fields/identity.md#define-an-identity-field)eller genom [API för schemaregister](../../xdm/api/descriptors.md#create).

Med frågetjänsten kan du även ange en identitet eller en primär identitet för ad hoc-schemadatauppsättningsfält direkt via SQL. Läs dokumentationen om [ange en sekundär identitet och primär identitet i ad hoc-schemaidentiteter](../data-governance/ad-hoc-schema-identities.md) för mer information.

### Skapa en fråga för att beräkna decimaler över en uppslagsperiod {#create-a-query}

I följande exempel visas SQL-frågan för att beräkna en decimal över en uppslagsperiod.

En mall kan skapas antingen med hjälp av Frågeredigeraren i användargränssnittet eller via [API för frågetjänst](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### Granskning av fråga

Avsnitt i exempelfrågan granskas närmare nedan.

#### Återställningsperioder

Datatypen decile innehåller en bucket för 1, 3, 6, 9, 12 och livstidssökningar. Frågan använder uppslagsperioderna 1, 3 och 6 månader, så varje avsnitt innehåller några&quot;upprepade&quot; frågor för att skapa temporära tabeller för varje uppslagsperiod.

>[!NOTE]
>
>Om källdata inte har någon kolumn som kan användas för att bestämma en uppslagsperiod, kommer alla decile-klassrankningar att utföras under `decileMonthAll`.

#### Aggregera

Använd vanliga tabelluttryck (CTE) för att samla ihop körsträckan innan du skapar decimalluckor. Detta anger det totala antalet mil för en specifik uppslagsperiod. CTE:er finns tillfälligt och kan bara användas inom omfånget för den större frågan.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

Blocket upprepas två gånger i mallen (`summed_miles_3` och `summed_miles_6`) med en ändring i datumberäkningen för att generera data för de andra uppslagsperioderna.

Det är viktigt att notera identitets-, dimension- och måttkolumnerna för frågan (`membershipNumber`, `loyaltyStatus` och `totalMiles` ).

#### Rankning

Med Deciles kan du utföra kategoriserad bucketing. Om du vill skapa ett rangordningsnummer `NTILE` -funktionen används med en parameter för `10` i ett FÖNSTER grupperat efter `loyaltyStatus` fält. Detta resulterar i en rankning från 1 till 10. Ange `ORDER BY` -satsen i `WINDOW` till `DESC` för att säkerställa att ett rankningsvärde på `1` ges till **störst** mått i dimensionen.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### Kartaggregering

Om du har flera uppslagsperioder måste du skapa en decimal-karta i förväg med `MAP_FROM_ARRAYS` och `COLLECT_LIST` funktioner. I exempelfragmentet `MAP_FROM_ARRAYS` skapar en karta med ett par tangenter (`loyaltyStatus`) och värden (`decileBucket`) arrayer. `COLLECT_LIST` returnerar en array med alla värden i den angivna kolumnen.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>Kartaggregering behövs inte om decimalrangordning bara krävs för en livstid.

#### Unika identiteter

Listan med unika identiteter (`membershipNumber`) krävs för att skapa en unik lista över alla medlemskap.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Om decimalrangordning bara krävs för en livstid kan det här steget utelämnas och aggregeras med `membershipNumber` kan göras i det sista steget.

#### Sammanfoga alla temporära data

Det sista steget är att sammanfoga alla temporära data till en form som är identisk med decimalstrukturen i fältgruppen.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

Om bara livstidsdata är tillgängliga visas din fråga så här:

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

Ett samband mellan rangordningsnumret och percentilen garanteras i frågeresultatet på grund av användning av deciler. Varje rankning motsvarar 10 %, så att en målgrupp som baseras på de 30 högsta procenten bara behöver ha rankningarna 1, 2 och 3 som mål.

### Kör frågemallen

Kör frågan för att fylla i decimaldatauppsättningen. Du kan också spara frågan som en mall och schemalägga den så att den körs vid en avslutning. När frågan sparas som en mall kan den också uppdateras för att använda mönstret för att skapa och infoga som refererar till `table_exists` -kommando. Mer information om hur du använder `table_exists`finns i [SQL-syntaxguide](../sql/syntax.md#table-exists).

## Nästa steg

Exemplet visar hur man gör decimalattribut tillgängliga i kundprofilen i realtid. På så sätt kan segmenteringstjänsten, antingen via ett användargränssnitt eller RESTful API, generera målgrupper baserat på dessa decimalgrupper. Se [Översikt över segmenteringstjänsten](../../segmentation/home.md) om du vill ha information om hur du skapar, utvärderar och får tillgång till segment.
