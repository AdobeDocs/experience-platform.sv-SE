---
title: Exempel på lambda-funktion - Hämta liknande poster
description: Lär dig hur du identifierar och hämtar liknande eller relaterade poster från en eller flera datauppsättningar baserat på ett likhetsmått och likhetströskelvärde. Det här arbetsflödet kan framhäva meningsfulla relationer eller överlappningar mellan olika datauppsättningar.
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 20624b916bcb3c17e39a402d9d9df87d0585d4b8
workflow-type: tm+mt
source-wordcount: '4011'
ht-degree: 2%

---

# Exempel på lambda-funktion: Hämta liknande poster

Lös flera vanliga användningsfall genom att använda Data Distiller lambda-funktioner för att identifiera och hämta liknande eller relaterade poster från en eller flera datauppsättningar. Du kan använda den här vägledningen när du vill identifiera produkter från olika datauppsättningar som har en betydande likhet i deras egenskaper eller attribut. Metoden i det här dokumentet innehåller bland annat lösningar för datadeduplicering, postkoppling, rekommendationssystem, informationshämtning och textanalys.

Dokumentet beskriver processen att implementera en likhetskoppling och använder sedan Data Distiller lambda-funktioner för att beräkna likheten mellan datauppsättningar och filtrera dem baserat på valda attribut. SQL-kodfragment och förklaringar tillhandahålls för varje steg i processen. Arbetsflödet implementerar likhetskopplingar med Jaccards likhetsmått och tokenisering med Data Distiller lambda-funktioner. Dessa metoder används sedan för att identifiera och hämta liknande eller relaterade poster från en eller flera datauppsättningar baserade på ett likhetsmått. Processens huvudavsnitt är: [tokenisering med lambda-funktioner](#data-transformation), [sammanfogning av unika element](#cross-join-unique-elements), [Beräkning av likhet med jaccard](#compute-the-jaccard-similarity-measure)och [tröskelbaserad filtrering](#similarity-threshold-filter).

## Förutsättningar

Innan du fortsätter med det här dokumentet bör du känna till följande koncept:

- A **likhetskoppling** är en åtgärd som identifierar och hämtar postpar från en eller flera tabeller baserat på ett mått på likhet mellan posterna. De viktigaste kraven för likhetsförening är följande:
   - **Likhetsmått**: Ett likhetskoppling är beroende av ett fördefinierat likhetsmått eller mått. Exempel på sådana mått är Jaccard-likheter, cosinus-likheter, redigeringsavstånd och så vidare. Mätvärdet beror på datatypen och användningsfallet. Detta mått anger hur likartade eller avvikande två poster är.
   - **Tröskelvärde**: Ett likhetströskelvärde används för att avgöra när de två posterna anses vara tillräckligt lika för att inkluderas i kopplingsresultatet. Poster med en likhetspoäng över tröskelvärdet räknas som träffar.
- The **Jaccard-likhet** index, eller Jaccard-likhetsmätning, är en statistik som används för att mäta likheter och mångfald hos samplingsuppsättningar. Den definieras som skärningspunktens storlek dividerad med storleken på den förening som provuppsättningarna har. Jaccards likhetsmätning varierar från noll till ett. En Jaccard-likhet på noll innebär att det inte finns någon likhet mellan uppsättningarna, och en Jaccard-likhet på ett innebär att uppsättningarna är identiska.
  ![Ett venn-diagram som illustrerar likhetsmätningen i jacard.](../images/use-cases/jaccard-similarity.png)
- **Lambda-funktioner** i Data Distiller är anonyma, infogade funktioner som kan definieras och användas i SQL-satser. De används ofta med funktioner i högre ordning på grund av deras förmåga att skapa snabba funktioner som kan skickas som data. Lambda-funktioner används ofta med funktioner i högre ordning som `transform`, `filter`och `array_sort`. Lambda-funktioner är särskilt användbara i situationer där det inte är nödvändigt att definiera en fullständig funktion, och en kort engångsfunktion kan användas textbundet.

## Komma igång

Data Distiller SKU krävs för att utföra lambda-funktionerna på dina Adobe Experience Platform-data. Om du inte har Data Distiller SKU kontaktar du Adobe kundtjänstrepresentanten för mer information.

## Fastställ likhet {#establish-similarity}

Det här användningsfallet kräver ett likhetsmått mellan textsträngar som kan användas senare för att fastställa ett tröskelvärde för filtrering. I det här exemplet representerar produkterna i Set A och Set B orden i två dokument.

Jaccards likhetsmått kan användas på ett stort antal datatyper, inklusive textdata, kategoriserade data och binära data. Den är även lämplig för realtids- eller batchbearbetning eftersom den kan vara beräkningsmässigt effektiv att beräkna för stora datamängder.

Produktgrupp A och B innehåller testdata för det här arbetsflödet.

- Produktgrupp A: `{iPhone, iPad, iWatch, iPad Mini}`
- Produktgrupp B: `{iPhone, iPad, Macbook Pro}`

För att beräkna Jaccards likheter mellan produktuppsättningarna A och B, ska du först hitta **skärningspunkt** (gemensamma element) i produktuppsättningarna. I detta fall `{iPhone, iPad}`. Gå till **union** (alla unika element) i båda produktuppsättningarna. I detta exempel `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Slutligen använder du likhetsformeln för Jaccard: `J(A,B) = A∪B / A∩B` för att beräkna likheterna.

J = Jackavstånd A = set 1 B = set 2

Jaccards likhet mellan produktuppsättningarna A och B är 0,4. Detta visar på en viss grad av likhet mellan de ord som används i de två dokumenten. Denna likhet mellan de två uppsättningarna definierar kolumnerna i likhetskopplingen. Dessa kolumner representerar information, eller egenskaper som är kopplade till data, som lagras i en tabell och används för att utföra likhetsberäkningar.

### Parvis Jaccard-beräkning med stränglikhet {#pairwise-similarity}

Om likheterna mellan strängar ska jämföras på ett mer exakt sätt måste den parvisa likheten beräknas. Med parvis likhet delas högdimensionella objekt upp i mindre dimensionella objekt för jämförelse och analys. För att göra detta delas en textsträng upp i mindre delar eller enheter (tokens). Det kan vara enskilda bokstäver, grupper av bokstäver (som stavelser) eller hela ord. Likheten beräknas för varje par av tokens mellan varje element i Set A med varje element i Set B. Denna tokenisering utgör grunden för analytiska och beräkningsmässiga jämförelser, relationer och insikter som ska hämtas från data.

För den parvisa likhetsberäkningen används i det här exemplet teckenbit i gram (två teckenvariabler) för att jämföra en likhetsmatchning mellan textsträngarna för produkterna i Uppsättning A och Uppsättning B. Ett bigram är en sekvens av två objekt eller element i en given sekvens eller text. Du kan generalisera detta till n-gram.

I det här exemplet antas att fallet inte har någon betydelse och att blanksteg inte ska tas med i beräkningen. Enligt dessa kriterier har set A och Set B följande bigram:

Produktgrupp A bigram:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- iWatch (5): &quot;iw&quot;, &quot;wa&quot;, &quot;at&quot;, &quot;tc&quot;, &quot;ch&quot;
- iPad Mini (7): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;, &quot;dm&quot;, &quot;mi&quot;, &quot;in&quot;, &quot;ni&quot;

Bigram för produktgrupp B:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- Macbook Pro (9): &quot;Ma&quot;, &quot;ac&quot;, &quot;cb&quot;, &quot;bo&quot;, &quot;oo&quot;, &quot;ok&quot;, &quot;kp&quot;, &quot;pr&quot;, &quot;ro&quot;

Beräkna sedan Jaccards likhetskoefficient för varje par:

|                   | iPhone (uppsättning B) | iPad (uppsättning B) | Macbook Pro (Set B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (Set A) | (Skärningspunkt: 5, union: 5) = 5 / 5 = 1 | (Skärningspunkt: 1, union: 7) =1 / 7 ~0,14 | (Skärningspunkt: 0, union: 14) = 0 / 14 = 0 |
| iPad (Set A) | (Skärningspunkt: 1, union: 7) = 1 / 7 ~0,14 | (Skärningspunkt: 3, union: 3) = 3 / 3 = 1 | (Skärningspunkt: 0, union: 12) = 0 / 12 = 0 |
| iWatch (Set A) | (Skärningspunkt: 0, union: 8) = 0 / 8 = 0 | (Skärningspunkt: 0, union: 8) = 0 / 8 = 0 | (Skärningspunkt: 0, union: 8) = 0 / 8 =0 |
| iPad Mini (A) | (Skärningspunkt: 1, union: 11) = 1 / 11 ~0,09 | (Skärningspunkt: 3, union: 7) = 3 / 7 ~0,43 | (Skärningspunkt: 0, union: 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Skapa testdata med SQL {#create-test-data}

Om du vill skapa en testtabell manuellt för produktuppsättningarna använder du SQL CREATE TABLE-satsen.

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

I följande beskrivningar finns en beskrivning av SQL-kodblocket ovan:

- Rad 1: `CREATE TEMP TABLE featurevector1 AS`: Den här programsatsen skapar en temporär tabell med namnet `featurevector1`. Tillfälliga tabeller är vanligtvis bara tillgängliga i den aktuella sessionen och tas automatiskt bort i slutet av sessionen.
- Rad 1 och 2: `SELECT * FROM (...)`: Den här delen av koden är en underfråga som används för att generera data som infogas i `featurevector1` tabell.
I underfrågan, flera `SELECT` programsatser kombineras med `UNION ALL` -kommando. Varje `SELECT` -programsatsen genererar en rad med data med de angivna värdena för `ProductName` kolumn.
- Rad 3: `SELECT 'iPad' AS ProductName`: Detta genererar en rad med värdet `iPad` i `ProductName` kolumn.
- Rad 5: `SELECT 'iPhone'`: Detta genererar en rad med värdet `iPhone` i `ProductName` kolumn.

SQL-satsen skapar en tabell enligt nedan:

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Använd följande SQL-sats för att skapa den andra funktionsvektorn:

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## Dataomvandlingar {#data-transformation}

I det här exemplet måste flera åtgärder utföras för att uppsättningarna ska kunna jämföras korrekt. För det första tas alla blanksteg bort från funktionsvektorerna eftersom det antas att de inte bidrar till likhetsmåttet. Alla dubbletter som finns i funktionsvektorn tas sedan bort eftersom de tar bort databearbetning. Därefter extraheras tokens med två tecken (bigram) från funktionsvektorerna. I det här exemplet antas de överlappa varandra.

>[!NOTE]
>
>I illustrationssyfte läggs de bearbetade kolumnerna till bredvid funktionsvektorn för varje steg.

Följande avsnitt visar de nödvändiga dataomvandlingarna som borttagning av dubbletter, borttagning av tomt utrymme och konvertering av gemener innan tokeniseringsprocessen startas.

### Deduplicering {#deduplication}

Använd sedan `DISTINCT` -sats för att ta bort dubbletter. Det finns inga dubbletter i det här exemplet, men det är ett viktigt steg att förbättra exaktheten i alla jämförelser. Nödvändig SQL visas nedan:

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Borttagning av tomt utrymme {#whitespace-removal}

I följande SQL-sats tas blanktecken bort från funktionsvektorerna. The `replace(ProductName, ' ', '') AS featurevector1_nospaces` en del av frågan `ProductName` kolumn från `featurevector1` tabellen och använder `replace()` funktion. The `REPLACE` ersätts alla förekomster av ett blanksteg (&#39; &#39;) med en tom sträng (&#39;&#39;&#39;). Detta tar bort alla blanksteg från `ProductName` värden. Resultatet kantutjämnas som `featurevector1_nospaces`.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

Resultaten visas i tabellen nedan:

|   | featurevector1_distinkt | featurevector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

SQL-satsen och dess resultat för den andra funktionsvektorn visas nedan:

+++Markera för att expandera

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

Resultatet visas enligt nedan:

|   | featurevector2_distinkt | featurevector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Konvertera till gemener {#lowercase-conversion}

Därefter har SQL förbättrats så att produktnamnen konverteras till gemener och blanksteg tas bort. Funktionen lower (`lower(...)`) används på resultatet av `replace()` funktion. Funktionen lower konverterar alla tecken i den ändrade `ProductName` värden till gemener. Detta garanterar att värdena är i gemener oavsett ursprungligt skiftläge.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

Resultatet av programsatsen är:

|   | featurevector1_distinkt | featurevector1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

SQL-satsen och dess resultat för den andra funktionsvektorn visas nedan:

+++Markera för att expandera

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

Resultatet visas enligt nedan:

|   | featurevector2_distinkt | featurevector2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### Extrahera variabler med SQL {#tokenization}

Nästa steg är tokenisering eller textdelning. Tokenisering är processen att ta text och bryta ned den till individuella termer. Vanligtvis innebär detta att meningar delas upp i ord. I det här exemplet delas strängar upp i bigram (och i högre ordning n-gram) genom att tokens extraheras med SQL-funktioner som `regexp_extract_all`. Överlappande bigram måste genereras för effektiv tokenisering.

SQL har förbättrats ytterligare så att du kan använda `regexp_extract_all`. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` Den här delen av frågan bearbetar den ändrade `ProductName` värden som skapades i föregående steg. Den använder `regexp_extract_all()` funktion för att extrahera alla icke-överlappande delsträngar med ett till två tecken från det ändrade och gemena `ProductName` värden. The `.{2}` mönstret för reguljära uttryck matchar delsträngarna med två tecken. The `regexp_extract_all(..., '.{2}', 0)` delar av funktionen extraherar sedan alla matchande delsträngar från indatatexten.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

Resultaten visas i tabellen nedan:

+++Markera för att expandera

|   | featurevector1_distinkt | featurevector1_transform | variabler |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;, &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Om du vill förbättra precisionen ytterligare måste du använda SQL för att skapa överlappande tokens. Strängen &quot;iPad&quot; ovan saknar till exempel variabeln &quot;pa&quot;. Du åtgärdar detta genom att skifta lookahead-operatorn (med `substring`) i ett steg och generera bigram.

Liknar föregående steg, `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` extraherar sekvenser med två tecken från det ändrade produktnamnet, men börjar med det andra tecknet med `substring` metod för att skapa överlappande token. Nästa, på rad 3-7 (`array_union(...) AS tokens`), `array_union()` funktionen kombinerar arrayerna för sekvenser med två tecken som hämtas av de två reguljära uttrycksextraktionerna. Detta garanterar att resultatet innehåller unika variabler från både icke-överlappande och överlappande sekvenser.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

Resultaten visas i tabellen nedan:

+++Markera för att expandera

|   | featurevector1_distinkt | featurevector1_transform | variabler |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;,&quot;pa&quot;,&quot;dm&quot;,&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;,&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;,&quot;ch&quot;,&quot;wa&quot;,&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;,&quot;ph&quot;,&quot;on&quot;} |

{style="table-layout:auto"}

+++

Användning av `substring` som en lösning på problemet har begränsningar. Om du gör tokens från texten baserat på tre gram (tre tecken) måste du använda två `substrings` att titta framåt två gånger för att få de ändringar som krävs. Om du ska göra 10 gram behöver du nio `substring` uttryck. Detta skulle göra att koden blottar och blir ohållbar. Användning av reguljära uttryck är inte lämpligt. Det krävs en ny strategi.

### Justera för längden på produktnamnet {#length-adjustment}

SQl kan förbättras med sekvens- och längdfunktionerna. I följande exempel `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` genererar en nummersekvens från ett till längden på det ändrade produktnamnet minus tre. Om det ändrade produktnamnet till exempel är&quot;ipadmini&quot; med teckenlängden åtta, genereras nummer från ett till fem (åtta-tre).

Programsatsen nedan extraherar unika produktnamn och delar sedan upp varje namn i teckensekvenser (tokens) med fyra teckenlängder, exklusive blanksteg, och visar dem som två kolumner. En kolumn visar de unika produktnamnen och den andra kolumnen visar deras genererade tokens.

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

Resultaten visas i tabellen nedan:

+++Markera för att expandera

|   | featurevector1_distinkt | variabler |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;,&quot;padm&quot;,&quot;admi&quot;,&quot;dmin&quot;,&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;wat&quot;,&quot;watc&quot;,&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;,&quot;phon&quot;,&quot;hone&quot;} |

{style="table-layout:auto"}

+++

### Ange tokenlängd

Ytterligare villkor kan läggas till i programsatsen för att säkerställa att de genererade sekvenserna har en viss längd. Följande SQL-sats utökas på tokengenereringslogiken genom att göra `transform` funktionen är mer komplex. Programsatsen använder `filter` funktion inom `transform` för att säkerställa att de genererade sekvenserna är sex tecken långa. Den hanterar fall där det inte är möjligt genom att tilldela NULL-värden till dessa positioner.

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

Resultaten visas i tabellen nedan:

+++Markera för att expandera

|   | featurevector1_distinkt | variabler |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;,&quot;padmin&quot;,&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## Utforska lösningar med Data Distiller lambda-funktioner {#lambda-function-solutions}

Lambda-funktioner är kraftfulla konstruktioner som gör att du kan implementera&quot;programmering&quot; som syntax i Data Distiller. De kan användas för att iterera en funktion över flera värden i en array.

I Data Distiller är lambda-funktioner idealiska för att skapa n-gram och iterera över teckensekvenser.

The `reduce` funktion, särskilt när den används i sekvenser som genereras av `transform`, ger ett sätt att härleda kumulativa värden eller aggregat, som kan vara avgörande i olika analys- och planeringsprocesser.

I SQl-programsatsen nedan är `reduce()` function aggregerar element i en array med hjälp av en anpassad aggregator. Den simulerar en for-slinga till **skapa kumulativa summor för alla heltal** från en till fem. `1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`.

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Lambda function to add numbers
    )
) AS sum_result;
```

Här följer en analys av SQL-satsen:

- Rad 1: `transform` använder funktionen `x -> reduce` för varje element som genereras i sekvensen.
- Rad 2: `sequence(1, 5)` genererar en nummersekvens från ett till fem.
- Rad 3: `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` utför en reduceringsåtgärd för varje element x i sekvensen (från 1 till 5).
   - The `reduce` funktionen har ett inledande ackumulatorvärde på 0, en sekvens från ett till det aktuella värdet för `x`och en lambda-funktion `(acc, y) -> acc + y` om du vill lägga till siffrorna.
   - Funktionen lambda `acc + y` ackumulerar summan genom att lägga till det aktuella värdet `y` till ackumulatorn `acc`.
- Rad 8: `AS sum_result` byter namn på den resulterande kolumnen till sum_result.

Sammanfattningsvis tar den här lambda-funktionen två parametrar (`acc` och `y`) och definierar åtgärden som ska utföras, som i det här fallet lägger till `y` till ackumulatorn `acc`. Den här lambda-funktionen körs för varje element i sekvensen under reduceringsprocessen.

Utdata för den här programsatsen är en enda kolumn (`sum_result`) som innehåller de ackumulerade summorna av tal från ett till fem.

### Värdet för lambda-funktioner {#value-of-lambda-functions}

I det här avsnittet analyseras en nedbantad version av en SQL-sats på tre gram för att bättre förstå värdet på lambda-funktioner i Data Distiller och skapa n-gram mer effektivt.

Programsatsen nedan fungerar på `ProductName` -kolumnen i `featurevector1` tabell. Den skapar en uppsättning treteckendelsträngar som härleds från de ändrade produktnamnen i tabellen, med hjälp av positioner som hämtas från den sekvens som genereras.

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

Här följer en analys av SQL-satsen:

- Rad 2: `transform` använder en lambda-funktion på varje heltal i sekvensen.
- Rad 3: `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` genererar en serie heltal från `1` till längden på det ändrade produktnamnet minus två.
   - `length(lower(replace(ProductName, ' ', '')))` beräknar längden på `ProductName` när du har skapat den med gemener och tagit bort blanksteg.
   - `- 2` subtraherar två från längden för att säkerställa att sekvensen genererar giltiga startpositioner för delsträngar med tre tecken. Genom att subtrahera 2 ser du till att du har tillräckligt många tecken efter varje startposition för att kunna extrahera en delsträng med 3 tecken. Delsträngsfunktionen här fungerar som en lookahead-operator.
- Rad 4: `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` är en lambda-funktion som fungerar på varje heltal `i` i den genererade sekvensen.
   - The `substring(...)` funktionen extraherar en delsträng med 3 tecken från `ProductName` kolumn.
   - Innan du extraherar delsträngen `lower(replace(ProductName, ' ', ''))` konverterar `ProductName` till gemener och tar bort blanksteg för att säkerställa konsekvens.

Resultatet är en lista med delsträngar med tre tecken i längd, som extraheras från de ändrade produktnamnen, baserat på de positioner som anges i sekvensen.

## Filtrera resultaten {#filter-results}

The `filter` funktion, med efterföljande [dataomvandlingar](#data-transformation), ger en mer detaljerad extrahering av relevant information från textdata. På så sätt kan ni få insikter, förbättra datakvaliteten och underlätta bättre beslutsprocesser.

The `filter` funktionen i följande SQL-sats används för att förfina och begränsa positionssekvensen i strängen från vilken delsträngar extraheras med den efterföljande omformningsfunktionen.

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

The `filter` funktionen genererar en sekvens med giltiga startpositioner inom den ändrade `ProductName` och extraherar delsträngar med en viss längd. Endast startpositioner som tillåter extrahering av en delsträng med sju tecken tillåts.

Villkoret `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` ser till att startpositionen `i` plus `6` (längden på den önskade delsträngen med sju tecken minus ett) överstiger inte längden på den ändrade `ProductName`.

The `CASE` -programsatsen används för att villkorligt inkludera eller exkludera delsträngar baserat på deras längd. Endast delsträngar med sju tecken ingår, andra ersätts med NULL. Dessa delsträngar används sedan av `transform` funktionen för att skapa en sekvens med delsträngar från `ProductName` kolumn i `featurevector1` tabell.

>[!TIP]
>
>Du kan använda [parametriserade mallar](../ui/parameterized-queries.md) för att återanvända och abstrakt logik i dina frågor. När du till exempel skapar allmänna verktygsfunktioner (till exempel den som visas ovan för tokeniseringssträngar) kan du använda parameteriserade mallar för Data Distiller där antalet tecken är en parameter.

## Beräkna korskopplingen mellan unika element i två funktionsvektorer {#cross-join-unique-elements}

Att identifiera skillnader eller avvikelser mellan de två datauppsättningarna baserat på en specifik omvandling av data är en vanlig process för att bibehålla datakvaliteten, förbättra datakvaliteten och säkerställa konsekvens mellan datauppsättningarna.

Den här SQL-satsen nedan extraherar de unika produktnamnen som finns i `featurevector2` men inte i `featurevector1` efter att du har använt omformningarna.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Förutom `EXCEPT`kan du också använda `UNION` och `INTERSECT` beroende på ditt användningssätt. Du kan också experimentera med `ALL` eller `DISTINCT` -satser för att se skillnaden mellan att inkludera alla värden och bara returnera de unika värdena för de angivna kolumnerna.

Resultaten visas i tabellen nedan:

+++Markera för att expandera

|   | lower(replace(ProductName, &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

Utför sedan en korskoppling för att kombinera element från de två funktionsvektorerna och skapa par av element för jämförelse. Det första steget i den här processen är att skapa en tokeniserad vektor.

En tokeniserad vektor är en strukturerad representation av textdata där varje ord, fras eller meningsenhet (token) konverteras till ett numeriskt format. Med den här konverteringen kan naturliga språkbearbetningsalgoritmer förstå och analysera textinformation.

SQl nedan skapar en tokeniserad vektor.

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>Om du använder [!DNL DbVisualizer]När du har skapat eller tagit bort en tabell uppdaterar du databasanslutningen så att tabellens metadatacache uppdateras. Data Distiller skickar inte ut metadatauppdateringar.

Resultaten visas i tabellen nedan:

+++Markera för att expandera

|   | featurevector1_distinkt | variabler |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 3 | iwatch | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Upprepa sedan processen för `featurevector2`:

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

Resultaten visas i tabellen nedan:

+++Markera för att expandera

|   | featurevector2_distinkt | variabler |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

När båda tokeniserade vektorerna är klara kan du nu skapa krysset. Detta visas i SQL nedan:

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

Här följer en sammanfattning av SQl som används för att skapa krysset:

- Rad 2: `A.featurevector1_distinct AS SetA_ProductNames` markerar `featurevector1_distinct` kolumn från tabellen `A` och tilldelar det ett alias `SetA_ProductNames`. Det här avsnittet av SQL resulterar i en lista med olika produktnamn från den första datauppsättningen.
- Rad 4: `A.tokens AS SetA_tokens1` markerar `tokens` kolumn från tabellen eller underfrågan `A` och tilldelar det ett alias `SetA_tokens1`. Det här avsnittet av SQL resulterar i en lista med tokeniserade värden som är associerade med produktnamnen från den första datauppsättningen.
- Rad 8: `CROSS JOIN` -åtgärden kombinerar alla möjliga kombinationer av rader från de två datauppsättningarna. Med andra ord paras varje produktnamn och tillhörande tokens från den första tabellen (`A`) med varje produktnamn och tillhörande tokens från den andra tabellen (`B`). Detta resulterar i en kartesisk produkt av de två datauppsättningarna, där varje rad i utdata representerar en kombination av ett produktnamn och tillhörande tokens från båda datauppsättningarna.

Resultaten visas i tabellen nedan:

+++Markera för att expandera

| * | SetA_ProductNames | AngeB_Produktnamn | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## Beräkna likhetsmåttet för Jaccard {#compute-the-jaccard-similarity-measure}

Beräkna sedan med Jaccards likhetskoefficient för att utföra en likhetsanalys mellan de två uppsättningarna produktnamn genom att jämföra deras tokeniserade representationer. Utdata från SQL-skriptet nedan ger följande: produktnamn från båda uppsättningarna, deras tokeniserade representationer, antal gemensamma och totala unika tokens samt den beräknade Jaccard-likhetskoefficienten för varje par med datauppsättningar.


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

Nedan följer en sammanfattning av den SQL som används för att beräkna likhetskoefficienten för Jaccard:

- Rad 6: `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` beräknar antalet variabler som är gemensamma för båda `SetA_tokens1` och `SetB_tokens2`. Beräkningen görs genom att storleken på skärningspunkten för de två tokenarrayerna beräknas.
- Rad 7: `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` beräknar det totala antalet unika token i båda `SetA_tokens1` och `SetB_tokens2`. Den här raden beräknar storleken på unionen av de två tokenarrayerna.
- Rad 8-10: `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` beräknar Jaccard-likheterna mellan tokenuppsättningarna. Dessa rader dividerar storleken på tokenöverlappningen med storleken på tokenunionen och avrundar resultatet till två decimaler. Resultatet är ett värde mellan noll och ett, där ett värde anger fullständig likhet.

Resultaten visas i tabellen nedan:

+++Markera för att expandera

| * | SetA_ProductNames | AngeB_Produktnamn | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Jaccard-likhet |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 7 | 0,43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 16 | 0,0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 11 | 0,09 |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 3 | 1,0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 12 | 0,0 |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 7 | 0,14 |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 0 | 8 | 0,0 |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 0 | 10 | 0,0 |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 1 | 7 | 0,14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 5 | 5 | 1,0 |

{style="table-layout:auto"}

+++

## Filtrera resultat baserat på tröskelvärdet för jacard-likhet {#similarity-threshold-filter}

Filtrera slutligen resultaten baserat på ett fördefinierat tröskelvärde för att endast markera de par som uppfyller likhetskriterierna. SQL-satsen nedan filtrerar produkterna med en Jaccard-likhetskoefficient på minst 0,4. Detta minskar resultaten till par som uppvisar en avsevärd grad av likhet.

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

Resultatet av den här frågan ger kolumnerna för likhetskopplingen enligt nedan:

+++Markera för att expandera

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++:

### Nästa steg {#next-steps}

Genom att läsa det här dokumentet kan du nu använda den här logiken för att framhäva meningsfulla relationer eller överlappningar mellan olika datauppsättningar. Möjligheten att identifiera produkter från olika datauppsättningar som har en betydande likhet i egenskaper och attribut har många verkliga program. Denna logik kan användas för scenarier som produktmatchning (för att gruppera eller rekommendera liknande produkter för kunder), datarensning (för att förbättra datakvaliteten) och analys av varukorgar (för att ge insikter i kundbeteende, preferenser och potentiella möjligheter till korsförsäljning).

Om du inte redan har gjort det bör du läsa [Översikt över AI/ML-funktioner](../data-distiller/ml-feature-pipelines/overview.md). Använd den översikten för att lära dig hur Data Distiller och den maskininlärning du föredrar kan skapa anpassade datamodeller som stöder era marknadsföringsfall med data från Experience Platform.
