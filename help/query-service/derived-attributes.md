---
title: Härledda attribut
description: Med härledda attribut kan du beräkna attribut på en vanlig cadence och eventuellt publicera dessa härledda attribut i kundprofilen i realtid som profilattribut. Det här dokumentet innehåller en översikt över hur du använder frågetjänsten för att skapa härledda attribut som kan användas med dina profildata.
source-git-commit: 72e157e0a6310ebf2f55205b03b60600a56e3cf6
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---

# Härledda attribut

Med härledda attribut kan du beräkna attribut på en vanlig cadence och eventuellt publicera dessa härledda attribut i kundprofilen i realtid som profilattribut.

Härledda attribut, t.ex. sådana som har skapats med decimaldata, behövs för en mängd olika användningsfall som analyserar profildata. Med hjälp av decimaldata kan ni skapa målgrupper från segment baserat på deras percentil eller rankning för ett visst attribut. Exempel på möjliga användningsområden kan vara:

* Identifiera de lägsta 10 % av prenumeranterna baserat på tittarupplevelsen per kanal. Detta skulle göra det möjligt för marknadsförarna att inrikta sig på en viss målgrupp och sälja ett nytt prenumerationspaket.
* Identifiera en målgrupp som befinner sig i de tio största flygbolagen baserat på den totala tillryggalagda sträckan och som har statusen&quot;Flyer&quot;. Den här målgruppen kan användas för att selektivt rikta sig till försäljningen av ett nytt kreditkortserbjudande.

## Komma igång

Den här översikten kräver en fungerande förståelse av [API-anrop för plattformar](../landing/api-guide.md) och följande komponenter i Adobe Experience Platform:

* [Översikt över kundprofiler i realtid](../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Grunderna för schemakomposition](../xdm/schema/composition.md): En introduktion till XDM-scheman (Experience Data Model) och byggstenar, principer och bästa metoder för att komponera scheman.
* [Så här aktiverar du ett schema för kundprofil i realtid](../profile/tutorials/add-profile-data.md): I den här självstudien beskrivs de steg som krävs för att lägga till data i kundprofilen i realtid.

## SQL-stöd för härledda attribut

Om du vill definiera decimalordningen baserat på en viss dimension (kategori) och ett motsvarande mått (intäkt, poäng, visningstid osv.) måste ett schema utformas så att det går att dekorera spärrning. Det här schemat kan användas som en del av det större profilschemat.

### Skapa ett ID-namnområde för profilschemat {#identity-namespace}

Identitetsnamnutrymmen är en komponent i [Identitetstjänst](../identity-service/home.md) som fungerar som indikatorer för det sammanhang som en identitet hör till. En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme. När postdata matchas och sammanfogas mellan profilfragment måste både identitetsvärdet och namnutrymmet matcha.

Datauppsättningar som skapas som relaterar till identitet kan grupperas tillsammans som en datagrupp och bidrar till att upprätthålla datalivscykeln. Du kan skapa egna namnutrymmen med [Identitetstjänstens API](../identity-service/api/create-custom-namespace.md) eller via användargränssnittet. Se [hantera dokumentation för anpassade namnutrymmen](../identity-service/namespaces.md#manage-namespaces) för vägledning om hur du gör detta i användargränssnittet.

Den primära identitetsbeskrivningen kan antingen tilldelas till ett fält i schemagränssnittet eller skapas med API:t för schemaregistret. I dokumentationen finns instruktioner om hur du [definiera ett identitetsfält i Adobe Experience Platform användargränssnitt](../xdm/ui/fields/identity.md#define-an-identity-field)eller genom [API för schemaregister](../xdm/api/descriptors.md#create).

Med frågetjänsten kan du även ange en identitet eller en primär identitet för ad hoc-schemadatauppsättningsfält direkt via SQL. Läs dokumentationen om [ange en sekundär identitet och primär identitet i ad hoc-schemaidentiteter](./data-governance/ad-hoc-schema-identities.md) för mer information.

## Skapa härledda attribut

Exempelfrågan i det här dokumentet fokuserar på decimaler för att kategorisera stora datauppsättningar och rangordna data från det högsta till det lägsta värdet (eller vice versa), och filtrera baserat på tidsperioden.

### Deciles {#deciles}

En decile är en metod för att dela upp en uppsättning rankade data i 10 lika stora delar. När data delas upp i decilar tilldelas varje rad i datauppsättningen en decimalrankning. Detta gör att data kan sorteras i fallande eller stigande ordning.

Med decimalrangordning ordnas data i ordning från det lägsta till det högsta och görs på en skala från 1 till 10 där varje successiv siffra motsvarar en ökning på 10 procentenheter.

Lövbucklar representerar antalet rankade grupper och används för att tilldela en rankning till en dimension (kategori) i datauppsättningen. Bucket kan vara ett tal eller ett uttryck som utvärderas till ett positivt heltalsvärde för varje partition. Bucketerna får inte ha ett null-värde.

Kvartilarna används för att dividera fördelningen med fyra och percentiler med 100.

### Skapa schemat för dekorblock {#create-schema}

Schemat som har skapats för dekorgrupper består av tre delar: en datatyp, en fältgrupp för datatypen (per källdatamängd) och ett primärt identitetsfält.

>[!NOTE]
>
>Ett identitetsnamnområde måste skapas innan schemat kan skapas. Se [identity namespace](#identity-namespace) för mer information.

Adobe tillhandahåller flera standardklasser (&quot;core&quot;) för XDM, inklusive XDM Individual Profile och XDM ExperienceEvent. Förutom dessa huvudklasser kan du även skapa egna anpassade klasser som beskriver mer specifika användningsfall för organisationen. Visa guiderna om hur man [skapa och redigera scheman i användargränssnittet](../xdm/ui/resources/schemas.md#create) eller med [Schemas-slutpunkt i API:t för schemaregister](../xdm/api/schemas.md#create) för mer information.

Data som hämtas in till Experience Platform för användning av kundprofilen i realtid måste överensstämma med ett XDM-schema (Experience Data Model) som är aktiverat för profilen. För att ett schema ska kunna aktiveras för profilen måste det implementera antingen klassen XDM Individual Profile eller klassen XDM ExperienceEvent.

Du kan [aktivera ett schema för användning i kundprofilen i realtid med API:t för schemaregister](../xdm/tutorials/create-schema-api.md) eller [Användargränssnittet i Schemaredigeraren](../xdm/tutorials/create-schema-ui.md).  Detaljerade anvisningar om hur du aktiverar ett schema för profil finns i deras respektive dokumentation.

### Skapa en datatyp {#create-data-type}

Datatyper används som referenstypfält i klasser eller schemafältgrupper och möjliggör konsekvent användning av en flerfältstruktur som kan inkluderas var som helst i schemat. Att skapa datatypen är ett engångssteg per sandlåda, eftersom den kan återanvändas för alla decimalrelaterade fältgrupper.

I dokumentationen finns instruktioner om hur du [definiera en anpassad datatyp](../xdm/api/data-types.md) med [API för schemaregister](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### Skapa decimalfältgruppen {#create-field-group}

Skapandet av fältgruppen är ett steg per sandlåda. Den kan också återanvändas för alla decimalrelaterade scheman.

I dokumentationen finns instruktioner om hur du [skapa fältgrupper via användargränssnittet](../xdm/ui/resources/field-groups.md#create)

## Använd frågetjänsten för att skapa decimaler

Med frågetjänsten kan du skapa en datauppsättning som innehåller kategoriserade decilar. Detta kan sedan användas tillsammans med segmenteringstjänsten för att skapa målgrupper baserat på attributrankning.

De begrepp som visas i följande exempel kan användas för att skapa andra datauppsättningar med decimalintervall, förutsatt att en kategori (dimension) har definierats och ett mätvärde är tillgängligt. Exemplen är baserade på data för ett lojalitetsprogram för flygbolag. Flygbolagets lojalitetsdata använder klassen Experience Events där varje händelse är en post för en affärstransaktion för **milkostnad**, antingen krediterad eller debiterad, samt medlemskapet **lojalitetsstatus** antingen &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; eller &quot;Gold&quot;. Det primära identitetsfältet är `membershipNumber`.

### Skapa en frågemall {#create-a-query-template}

Mallen kan skapas antingen med hjälp av Frågeredigeraren i användargränssnittet eller via [API för frågetjänst](./api/query-templates.md#create-a-query-template).

Avsnitten i frågemallen som visas nedan kommer att granskas mer ingående.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### Synpunkter

Datatypen decile innehåller en bucket för 1, 3, 6, 9, 12 och livstidssummor. Frågan använder summeringsperioderna 1, 3 och 6 månader, så varje avsnitt innehåller några&quot;upprepade&quot; frågor för att skapa temporära tabeller för varje summeringsperiod.

>[!NOTE]
>
>Om källdata inte har någon kolumn som kan användas för att bestämma en summeringsperiod, kommer alla decile-klassrankningar att utföras under `decileMonthAll`.

#### Aggregera

Använd vanliga tabelluttryck (CTE) för att samla ihop körsträckan innan du skapar decimalluckor. Detta anger det totala antalet mil för en specifik summeringsperiod. CTE:er finns tillfälligt och kan bara användas inom omfånget för den större frågan.

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

Blocket upprepas två gånger i mallen (`summed_miles_3` och `summed_miles_6`) med en ändring av datumberäkningen för att generera data för de andra summeringsperioderna.

Observera kolumnerna identity, dimension och metric för frågan (`membershipNumber`, `loyaltyStatus` och `totalMiles` ).

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

Om du har flera summeringsperioder måste du skapa en decimal-karta i förväg med `MAP_FROM_ARRAYS` och `COLLECT_LIST` funktioner. I exempelfragmentet `MAP_FROM_ARRAYS` skapar en karta med ett par tangenter (`loyaltyStatus`) och värden (`decileBucket`) arrayer. `COLLECT_LIST` returnerar en array med alla värden i den angivna kolumnen.

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

### Kör frågemallen

Frågor kan [utförd antingen via användargränssnittet](./ui/user-guide.md#executing-queries) eller [API för frågetjänst](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

Ett samband mellan rangordningsnumret och percentilen garanteras i frågeresultatet på grund av användning av deciler. Varje rankning motsvarar 10 %, så att en målgrupp som baseras på de 30 högsta procenten bara behöver ha rankningarna 1, 2 och 3 som mål.

## Nästa steg

Segmenteringstjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du kan generera målgrupper baserat på dessa decimalgrupper. Se [Översikt över segmenteringstjänsten](../segmentation/home.md) om du vill ha information om hur du skapar, utvärderar och får tillgång till segment.

Mer information om hur du skapar och använder segment i segmentbyggaren (gränssnittsimplementeringen av segmenteringstjänsten) finns i [Segment Builder Guide](../segmentation/ui/overview.md).

Mer information om hur du skapar segmentdefinitioner med API:t finns i självstudiekursen om [skapa målgruppssegment med API](../segmentation/tutorials/create-a-segment.md).
