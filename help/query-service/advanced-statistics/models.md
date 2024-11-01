---
title: Models
description: Modelllivscykelhantering med Data Distiller SQL-tillägget. Lär dig skapa, utbilda och hantera avancerade statistiska modeller med SQL, inklusive nyckelprocesser som modellversionshantering, utvärdering och förutsägelse, för att få användbara insikter från era data.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---

# Models

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Data Distiller-tillägget. Kontakta din Adobe-representant om du vill veta mer.

Frågetjänsten har nu stöd för kärnprocesserna för att bygga och driftsätta en modell. Du kan använda SQL för att utbilda modellen med dina data, utvärdera dess exakthet och sedan använda en tågmodell för att göra prognoser om nya data. Du kan sedan använda modellen för att generera från tidigare data och fatta välgrundade beslut om verkliga scenarier.

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

## Uppdatera en modell {#update}

Lär dig hur du uppdaterar en befintlig maskininlärningsmodell genom att använda nya funktionskonverteringar och konfigureringsalternativ som algoritmtyp och etikettkolumn. I SQL nedan visas hur du ökar modellens versionsnummer med varje uppdatering och ser till att ändringarna spåras så att modellen kan återanvändas i framtida utvärderings- eller förutsägelsesteg.

```sql
UPDATE model <model_alias> transform( one_hot_encoder(NAME) ohe_name, string_indexer(gender) gendersi) options ( type = 'LogisticRegression', label = <label-COLUMN>, ) ASSELECT col1,
       col2,
       col3
FROM   training-dataset.
```

För att du enklare ska förstå hur du hanterar modellversioner och tillämpar omformningar effektivt, beskrivs de viktigaste komponenterna och alternativen i arbetsflödet för modelluppdatering i följande anteckningar.

- `UPDATE model <model_alias>`: Uppdateringskommandot hanterar versionshantering och ökar modellens versionsnummer vid varje uppdatering.
- `version`: Ett valfritt nyckelord används bara under uppdateringar för att skapa en ny version av modellen.

## Utvärdera modeller {#evaluate-model}

För att säkerställa tillförlitliga resultat bör du utvärdera modellens exakthet och effektivitet innan du distribuerar den för förutsägelser med nyckelordet `model_evaluate`. SQL-satsen nedan anger en testdatamängd, specifika kolumner och modellens version för att testa modellen genom att utvärdera dess prestanda.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

Funktionen `model_evaluate` tar `model-alias` som sitt första argument och en flexibel `SELECT`-sats som sitt andra argument. Frågetjänsten kör först programsatsen `SELECT` och mappar resultatet till ADF (Adobe Defined Function) i `model_evaluate`. Systemet förväntar sig att kolumnnamnen och datatyperna i `SELECT`-satsens resultat matchar de som används i utbildningssteget. Dessa kolumnnamn och datatyper behandlas som testdata och etikettdata för utvärdering.

>[!IMPORTANT]
>
>Vid utvärdering av (`model_evaluate`) och prediktion (`model_predict`) används den (de) omvandling(ar) som utfördes vid kursen.

## Förutspå {#predict}

Använd sedan nyckelordet `model_predict` för att tillämpa den angivna modellen och versionen på en datauppsättning och generera prognoser för de markerade kolumnerna. I SQL nedan visas den här processen, som visar hur du kan förutse utfall med hjälp av modellens alias och version.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` accepterar modellaliaset som det första argumentet och en flexibel `SELECT`-sats som det andra argumentet. Frågetjänsten kör först programsatsen `SELECT` och mappar resultatet till ADF:en `model_predict`. Systemet förväntar sig att kolumnnamnen och datatyperna i `SELECT`-satsens resultat matchar dem från utbildningssteget. Dessa data används sedan för att bedöma och generera prognoser.

>[!IMPORTANT]
>
>Vid utvärdering av (`model_evaluate`) och prediktion (`model_predict`) används den (de) omvandling(ar) som utfördes vid kursen.

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
