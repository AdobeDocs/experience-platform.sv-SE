---
title: Models
description: Modelllivscykelhantering med Data Distiller SQL-tillägget. Lär dig skapa, utbilda och hantera avancerade statistiska modeller med SQL, inklusive nyckelprocesser som modellversionshantering, utvärdering och förutsägelse, för att få användbara insikter från era data.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 09129d9d19816b4d93b4979305f4ad532e5ffde4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 0%

---

# Models

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Data Distiller-tillägget. Kontakta din Adobe-representant om du vill veta mer.

Frågetjänsten har nu stöd för kärnprocesserna för att bygga och driftsätta en modell. Du kan använda SQL för att utbilda modellen med dina data, utvärdera dess exakthet och sedan använda den tränade modellen för att göra prognoser på nya data. Du kan sedan använda modellen för att generera från tidigare data och fatta välgrundade beslut om verkliga scenarier.

De tre stegen i modelllivscykeln för att generera åtgärdbara insikter är:

1. **Utbildning**: Modellen lär sig mönster från den angivna datauppsättningen. (skapa eller ersätta modell)
2. **Testning/utvärdering**: Modellens prestanda utvärderas med en separat datamängd. (`model_evaluate`)
3. **Förutsägelse**: Den tränade modellen används för att göra prognoser på nya, osynliga data.

Använd SQL-modelltillägget, som lagts till i den befintliga SQL-grammatiken, för att hantera modellens livscykel efter dina affärsbehov. Det här dokumentet innehåller den SQL som krävs för att skapa eller ersätta en modell, utbilda, utvärdera, utbilda om vid behov och förutse insikter.

## Skapa och utbilda modeller {#create-and-train}

Lär dig att definiera, konfigurera och utbilda en maskininlärningsmodell med hjälp av SQL-kommandon. I SQL nedan visas hur du skapar en modell, tillämpar omformningar av funktionstekniska funktioner och initierar utbildningsprocessen för att säkerställa att modellen är korrekt konfigurerad för framtida bruk. Följande SQL-kommandon beskriver olika alternativ för att skapa och hantera modeller:

- **SKAPA MODELL**: Skapar och utbildar en ny modell på en angiven datauppsättning. Om det redan finns en modell med samma namn returneras ett fel.
- **SKAPA MODELL OM FINNS INTE**: Skapar och tränar bara en ny modell om det inte redan finns en modell med samma namn i den angivna datauppsättningen.
- **SKAPA ELLER ERSÄTT MODELL**: Skapar och utbildar en modell och ersätter den senaste versionen av en befintlig modell med samma namn på den angivna datauppsättningen.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**Exempel**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

För att du ska få en förståelse för de viktigaste komponenterna och konfigurationerna i processen för att skapa och utbilda modeller, beskrivs syftet och funktionen för varje element i SQL-exemplet ovan.

- `<model_alias>`: Modellaliaset är ett återanvändbart namn som tilldelats modellen och som senare kan refereras till. Du måste ge modellen ett namn.
- `transform`: Transform-satsen används för att tillämpa funktionstekniska omformningar (till exempel kodning med en aktivering och strängindexering) på datauppsättningen innan modellen tränas. Den sista satsen i programsatsen `TRANSFORM` ska vara antingen en `vector_assembler` med en lista över kolumner som skulle utgöra funktionerna för modellutbildning, eller en härledd typ av `vector_assembler` (till exempel `max_abs_scaler(feature)`, `standard_scaler(feature)`). Endast de kolumner som nämns i den sista satsen används för utbildning. Alla andra kolumner, även om de ingår i frågan `SELECT`, kommer att exkluderas.
- `label = <label-COLUMN>`: Etikettkolumnen i utbildningsdatauppsättningen som anger målet eller resultatet som modellen ska förutsäga.
- `training-dataset`: Den här syntaxen väljer data som används för att utbilda modellen.
- `type = 'LogisticRegression'`: Den här syntaxen anger vilken typ av maskininlärningsalgoritm som ska användas. Alternativen är `LinearRegression`, `LogisticRegression` och `KMeans`.
- `options`: Det här nyckelordet innehåller en flexibel uppsättning nyckelvärdepar för att konfigurera modellen.
   - `Key model_type`: `model_type = '<supported algorithm>'`: Anger vilken typ av maskininlärningsalgoritm som ska användas. De alternativ som stöds är `LinearRegression`, `LogisticRegression` och `KMeans`.
   - `Key label`: `label = <label_COLUMN>`: Definierar etikettkolumnen i utbildningsdatauppsättningen, vilket anger målet eller resultatet som modellen har som mål att förutsäga.

Använd SQL för att referera till datauppsättningen som används för utbildning.

>[!TIP]
>
>En fullständig referens om `TRANSFORM`-satsen, inklusive funktioner och användning som stöds i både `CREATE MODEL` och `CREATE TABLE`, finns i [`TRANSFORM`-satsen i SQL Syntax-dokumentationen ](../sql/syntax.md#transform).

## Uppdatera en modell {#update}

Lär dig hur du uppdaterar en befintlig maskininlärningsmodell genom att använda nya funktionskonverteringar och konfigureringsalternativ som algoritmtyp och etikettkolumn. Varje uppdatering skapar en ny version av modellen, som ökas stegvis från den senaste versionen. Detta säkerställer att ändringarna spåras och att modellen kan återanvändas i framtida utvärderings- eller förutsägelsesteg.

I följande exempel visas hur du uppdaterar en modell med nya omformningar och alternativ:

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**Exempel**

Ta följande kommando för att få en bättre förståelse för versionsprocessen:

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

När det här kommandot har körts har modellen en ny version, vilket visas i tabellen nedan:

| Uppdaterat modell-ID | Uppdaterad modell | Ny version |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

Följande anmärkningar beskriver de viktigaste komponenterna och alternativen i arbetsflödet för modelluppdatering.

- `UPDATE model <model_alias>`: Uppdateringskommandot hanterar versionshantering och skapar en ny modellversion som har ökats från den senaste versionen.
- `version`: Ett valfritt nyckelord som bara används under uppdateringar för att explicit ange att en ny version ska skapas. Om det utelämnas ökas versionen automatiskt.

### Förhandsgranska och bevara omformade funktioner {#preview-transform-output}

Använd satsen `TRANSFORM` i programsatserna `CREATE TABLE` och `CREATE TEMP TABLE` för att förhandsgranska och behålla utdata för funktionsomformningar före modellutbildning. Den här förbättringen ger dig en inblick i hur omformningsfunktioner (som kodning, tokenisering och vektorsammansättning) används i datauppsättningen.

Genom att materialisera omformade data till en fristående tabell kan du inspektera mellanliggande funktioner, validera bearbetningslogiken och säkerställa funktionskvaliteten innan du skapar en modell. Detta förbättrar genomskinligheten i maskininlärningen och stöder ett mer välgrundat beslutsfattande under modellutvecklingen.

#### Syntax {#syntax}

Använd `TRANSFORM`-satsen i en `CREATE TABLE` - eller `CREATE TEMP TABLE` -programsats enligt nedan:

```sql
CREATE TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

Eller:

```sql
CREATE TEMP TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

**Exempel**

Skapa en tabell med grundläggande omformningar:

```sql
CREATE TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review;
```

Skapa en temporär tabell med ytterligare funktionstekniska steg:

```sql
CREATE TEMP TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

Fråga sedan utdata:

```sql
SELECT * FROM ctas_transform_table LIMIT 1;
```

#### Viktiga överväganden {#considerations}

Den här funktionen förbättrar genomskinligheten och stöder funktionsvalidering, men det finns viktiga begränsningar att tänka på när du använder `TRANSFORM`-satsen utanför modellskapandet.

- **Vektorutdata**: Om omformningen genererar vektortyputdata konverteras de automatiskt till arrayer.
- **Begränsning för återanvändning av grupp**: Tabeller som skapats med `TRANSFORM` kan bara tillämpa omformningar när tabeller skapas. Nya grupper med data som infogats med `INSERT INTO` omformas **inte automatiskt**. Om du vill använda samma transformeringslogik för nya data måste du återskapa tabellen med en ny `CREATE TABLE AS SELECT`-sats (CTAS).
- **Begränsning för återanvändning av modell**: Tabeller som skapats med `TRANSFORM` kan inte användas direkt i `CREATE MODEL` -satser. Du måste definiera om logiken för `TRANSFORM` när modellen skapas. Transformeringar som producerar utdata av vektortyp stöds inte under modellutbildning. Mer information finns i [Utdatatyper för funktionsomformning](./feature-transformation.md#available-transformations).

>[!NOTE]
>
>Den här funktionen är avsedd för inspektion och validering. Det ersätter inte återanvändbar pipeline-logik. Alla omformningar som är avsedda för modellindata måste omdefinieras explicit i steget för att skapa modellen.

## Utvärdera modeller {#evaluate-model}

För att säkerställa tillförlitliga resultat bör du utvärdera modellens exakthet och effektivitet innan du distribuerar den för förutsägelser med nyckelordet `model_evaluate`. SQL-satsen nedan anger en testdatamängd, specifika kolumner och modellens version för att testa modellen genom att utvärdera dess prestanda.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test_dataset)
```

Funktionen `model_evaluate` tar `model-alias` som sitt första argument och en flexibel `SELECT`-sats som sitt andra argument. Frågetjänsten kör först programsatsen `SELECT` och mappar resultatet till den `model_evaluate` Adobe Defined Function (ADF). Systemet förväntar sig att kolumnnamnen och datatyperna i `SELECT`-satsens resultat matchar de som används i utbildningssteget. Dessa kolumnnamn och datatyper behandlas som testdata och etikettdata för utvärdering.

>[!IMPORTANT]
>
>Vid utvärdering av (`model_evaluate`) och prediktion (`model_predict`) används den (de) omvandling(ar) som utfördes vid kursen.

## Förutspå {#predict}

>[!IMPORTANT]
>
>Förbättrad kolumnmarkering och kantutjämning för `model_predict` styrs av en funktionsflagga. Som standard inkluderas inte mellanliggande fält som `probability` och `rawPrediction` i förutsägelseutdata.\
>Om du vill aktivera åtkomst till dessa mellanliggande fält kör du följande kommando innan du kör `model_predict`:
>
>`set advanced_statistics_show_hidden_fields=true;`

Använd nyckelordet `model_predict` för att tillämpa den angivna modellen och versionen på en datauppsättning och generera prognoser. Du kan markera alla utdatakolumner, välja specifika eller tilldela alias för att förbättra utdataskärpan.

Som standard returneras bara baskolumner och den slutliga förutsägelsen om inte funktionsflaggan är aktiverad.

```sql
SELECT * FROM model_predict(model-alias, version-number, SELECT col1, col2 FROM dataset);
```

### Välj specifika utdatafält {#select-specific-output-fields}

När funktionsflaggan är aktiverad kan du hämta en delmängd av fält från `model_predict`-utdata. Använd det här om du vill hämta mellanliggande resultat, t.ex. förutsägbarhetssannolikheter, poängvärden för råförutsägelse och baskolumner från indatafrågan.

**Fall 1: Returnera alla tillgängliga utdatafält**

```sql
SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Fall 2: Returnera markerade kolumner**

```sql
SELECT a, b, c, probability, predictionCol FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Fall 3: Returnera markerade kolumner med alias**

```sql
SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

I varje fall returneras de yttre `SELECT`-kontrollerna som resultatfälten returneras. Dessa innehåller basfält från indatafrågan tillsammans med förutsägelseutdata som `probability`, `rawPrediction` och `predictionCol`.

### Bevara förutsägelser med CREATE TABLE eller INSERT INTO

Du kan behålla förutsägelser med antingen &quot;CREATE TABLE AS SELECT&quot; eller &quot;INSERT INTO SELECT&quot;, inklusive förväntade utdata om så önskas.

**Exempel: Skapa tabell med alla förutsägelseutdatafält**

```sql
CREATE TABLE scored_data AS SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Exempel: Infoga markerade utdatafält med alias**

```sql
INSERT INTO scored_data SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

Detta ger flexibilitet att välja och behålla endast relevanta förutsägelseutdatafält och baskolumner för analys och rapportering i efterföljande led.

## Utvärdera och hantera dina modeller

Använd kommandot `SHOW MODELS` för att lista alla tillgängliga modeller som du har skapat. Använd det för att visa de modeller som har utbildats och är tillgängliga för utvärdering eller förutsägelse. När du tillfrågas hämtas informationen från modelldatabasen som uppdateras när modellen skapas. Följande information returneras: modell-ID, modellnamn, version, källdatauppsättning, algoritminformation, alternativ/parametrar, skapad/uppdaterad tid samt användaren som skapade modellen.

```sql
SHOW MODELS;
```

Resultaten visas i en tabell som liknar den som visas nedan:

| model-id | model-name | version | source-dataset | type | alternativ | omforma | fält | skapad | uppdaterad | skapat AV |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1,0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;name&quot;,&quot;kön&quot;\] | 2024-08-14 10:30 | 2024-08-14 11:00 | `JohnSnow@adobe.com` |

## Rensa och underhålla dina modeller

Använd kommandot `DROP MODELS` för att ta bort modeller som du har skapat från modellregistret. Du kan använda den för att ta bort gamla, oanvända eller oönskade modeller. Detta frigör resurser och säkerställer att endast relevanta modeller upprätthålls. Du kan även inkludera ett valfritt modellnamn för förbättrad specificitet. Detta utesluter bara modellen med den angivna modellversionen.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Nästa steg

När du har läst det här dokumentet förstår du nu den grundläggande SQL-syntax som krävs för att skapa, utbilda och hantera tillförlitliga modeller med Data Distiller. Utforska sedan dokumentet [Implementera avancerade statistiska modeller](./implement-models/implement-models.md) för att lära dig mer om de olika tillförlitliga modellerna som finns tillgängliga och hur du implementerar dem effektivt i dina SQL-arbetsflöden. Om du inte redan har gjort det bör du kontrollera att dina data är optimalt förberedda för modellutbildning genom att läsa dokumentet [Funktionskonstruktion](./feature-engineering.md) .
