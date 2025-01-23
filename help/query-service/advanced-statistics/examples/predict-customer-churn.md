---
title: Förutspå kundomsättning med SQL-baserad Logistisk regression
description: Lär dig förutse kundbortfall med hjälp av SQL-baserad logistisk regression. Den här guiden täcker hela processen från att skapa modeller till utvärdering och förutsägelse. Få användbara insikter från kundernas beteenden när det gäller att implementera förebyggande strategier och optimera affärsbeslut.
source-git-commit: 95c7ad3f8eb86cacd42077008824eea9e25b4db0
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Förutspå kundomsättning med SQL-baserad Logistisk regression

Genom att förutse kundbortfall kan företag behålla kunder, optimera resurser och öka lönsamheten genom att förbättra nöjdheten och lojaliteten med hjälp av åtgärdbara insikter.

Upptäck hur du använder SQL-baserad logistikregression för att förutsäga kundbortfall. Använd den här omfattande SQL-guiden för att omvandla rådata från e-handel till meningsfulla kundinsikter baserat på viktiga beteendemått (som inköpsfrekvens, genomsnittligt ordervärde och senaste köp). Dokumentet täcker hela processen, från dataförberedelse och funktionsframtagning till modellframtagning, utvärdering och förutsägelse.

Använd den här guiden för att skapa en kraftfull modell för att förutsäga förändringar som identifierar riskkunder, förfinar strategier för kundlojalitet och driver bättre affärsbeslut. Den innehåller stegvisa instruktioner, SQL-frågor och detaljerade förklaringar som hjälper dig att använda maskininlärningstekniker i din datamiljö.

## Komma igång

Innan du skapar en omsättningsmodell är det viktigt att du utforskar viktiga kundfunktioner och datakrav. I följande avsnitt beskrivs viktiga kundattribut och obligatoriska datafält för korrekt modellutbildning.

### Definiera kundfunktioner {#define-customer-features}

Modellen analyserar köpvanor och trender för att kunna klassificera kurvor korrekt. Tabellen nedan visar de viktigaste funktionerna för kundbeteende som används i modellen:

| Funktion | Beskrivning |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | Det totala antalet inköp som gjorts av kunden. |
| `total_revenue` | Den totala intäkten från kundinköp. |
| `avg_order_value` | Det genomsnittliga värdet av en kunds inköp. |
| `customer_lifetime` | Antalet dagar mellan kundens första och sista köp. |
| `days_since_last_purchase` | Antalet dagar sedan kundens senaste köp. |
| `purchase_frequency` | Antalet distinkta månader då kunden gjorde inköp. |

### Antaganden och obligatoriska fält {#assumptions-required-fields}

Modellen är beroende av nyckelfält i tabellen `webevents` som samlar in information om kundtransaktioner för att generera kundbortfallsprognoser. Datauppsättningen måste innehålla följande fält:

| Fält | Beskrivning |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | En unik identifierare som används för att spåra kunder mellan sessioner. |
| `productListItems.priceTotal[0]` | Den totala kostnaden för inköpta artiklar per transaktion. |
| `productListItems.quantity[0]` | Det totala antalet artiklar i ett inköp. |
| `timestamp` | Exakt datum och tid för varje köphändelse. |
| `commerce.order.purchaseID` | Ett obligatoriskt värde som bekräftar ett slutfört köp. |

Datauppsättningen måste innehålla strukturerade historiska kundtransaktionsposter, där varje rad representerar en köphändelse. Varje händelse måste innehålla tidsstämplar i ett lämpligt datum- och tidsformat som är kompatibelt med SQL `DATEDIFF`-funktionen (till exempel YYY-MM-DD HH:MI:SS). Dessutom måste varje post innehålla ett giltigt Experience Cloud-ID (`ECID`) i fältet `identityMap` för att unikt identifiera kunder.

>[!TIP]
>
>Bearbetning av stora datauppsättningar med miljontals poster kan påverka prestandan avsevärt. Om du vill optimera frågekörningen partitionerar du upplevelsedatauppsättningen med tidsstämpel, utför inkrementell bearbetning med ögonblicksbilder och tillämpar effektiva aggregeringsfunktioner efter behov. Filtrera data före aggregering för att minska bearbetningskostnaderna.

## Skapa en modell {#create-a-model}

För att förutsäga kundbortfall måste ni skapa en SQL-baserad logistisk regressionsmodell som analyserar kundens inköpshistorik och beteendemått. Modellen klassificerar kunder som `churned` eller `not churned` genom att fastställa om de har gjort ett köp de senaste 90 dagarna.

### Använd SQL för att skapa kurvförutsägelsemodellen {#sql-create-model}

Den SQL-baserade modellen bearbetar `webevents`-data genom att samla nyckelmått och tilldela churn-etiketter baserat på en 90-dagars inaktivitetsregel. Denna metod skiljer aktiva kunder från riskkunder. SQL-frågan utför även funktionskonstruktion för att förbättra modellernas exakthet och förbättra bortfallsklassificeringen. Dessa insikter ger er möjlighet att implementera riktade strategier för kundlojalitet, minska bortfallet och maximera kundlivstidsvärdet.

>[!NOTE]
>
>I modellen för bortfallsförutsägelse används ett standardtröskelvärde på 90 dagar för att klassificera kunder som bortskurna. Om du vill justera det här tröskelvärdet så att det överensstämmer med dina affärsmål och strategier för kvarhållande ändrar du villkoret `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` i SQL-frågorna.

Använd följande SQL-sats för att skapa modellen `retention_model_logistic_reg` med de angivna funktionerna och etiketterna:

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### Modellutdata {#model-output}

Utdatadatauppsättningen innehåller kundrelaterade mått och deras bortfallsstatus. Varje rad representerar en kund, deras funktionsvärden och deras bortfallsstatus. Ni kan använda dessa utdata för att analysera kundbeteenden, träna prediktiva modeller och utveckla målinriktade strategier för att behålla riskfyllda kunder. En exempeltabell visas nedan:

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| Kolumn | Beskrivning |
|-----------|------------------------------------------------------------------------------------|
| `churned` | Värdet anger om kunden har gjort ett köp inom de senaste 90 dagarna (0 = inte nedringad, 1 = nedtryckt). |

## Använd SQL för att utvärdera modellen {#model-evaluation}

Utvärdera sedan modellen för omsättningsförutsägelse för att avgöra hur effektiv den är när det gäller att identifiera riskkunder. Utvärdera modellens prestanda med viktiga mätvärden som mäter precision och tillförlitlighet.

Använd funktionen `model_evaluate` för att mäta noggrannheten hos modellen `retention_model_logistic_reg` när det gäller att förutsäga kundbortfall. I följande SQL-exempel utvärderas modellen med en datauppsättning som är strukturerad som utbildningsdata:

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### Utdata för modellutvärdering

Utvärderingsresultatet innehåller nyckeltal för prestanda, som AUC-ROC, precision, precision och återkallande. Dessa mätvärden ger insikter i modellens effektivitet som ni kan använda för att förfina strategier för kvarhållning och fatta datadrivna beslut.

>[!NOTE]
>
>Prestandavärdena varierar mellan 0 och 1, där 1.0 representerar perfekta prestanda.

```console
 auc_roc | accuracy | precision | recall 
---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| Mått | Beskrivning |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | Denna mätmetod visar modellens förmåga att skilja mellan kunder som är bortskurna och kunder som inte är bortskurna. Ett värde närmare 1 innebär bättre prestanda. |
| `accuracy` | Precisionsmåttet representerar andelen korrekta prognoser, som utgör ett övergripande mått på modellens prestanda. |
| `precision` | Precision visar andelen korrekt identifierade kunder och anger tillförlitligheten i bortfallsförutsägelser. Ett högt värde innebär färre falskt positiva värden. |
| `recall` | Återkallande mäter modellens förmåga att identifiera alla faktiska kunder som har blivit bortskurna. Ett högt återkallningsvärde innebär att färre kunder missat att vinna. |

>[!NOTE]
>
>De nästan perfekta poängen i det här exemplet är avsedda som exempel. I praktiken kan verkliga data ge lägre värden på grund av brus och variabilitet.

## Modellförutsägelse {#model-prediction}

När modellen har utvärderats använder du `model_predict` för att tillämpa den på en ny datamängd och prognostisera kundomsättning. Ni kan använda dessa prognoser för att identifiera riskkunder och implementera riktade strategier för kundlojalitet.

### Använd SQL för att generera bortfallsprognoser {#sql-model-predict}

I SQL-frågan nedan används modellen `retention_model_logistic_reg` för att förutsäga kundbortfall med en datauppsättning som är strukturerad som utbildningsdata:

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### Utdata för modellförutsägelse {#prediction-output}

Datauppsättningen för utdata innehåller viktiga kundfunktioner och deras förväntade bortfallsstatus, vilket anger om det är troligt att en kund kommer att försvinna. Använd dessa insikter för att implementera proaktiva strategier för kundlojalitet och minska bortfallet från kunderna.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| Kolumn | Beskrivning |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | Kundens förväntade kurvstatus baserat på modellen (0 = inte kurvad, 1 = kurvad). |

## Nästa steg

Du har nu lärt dig att skapa, utvärdera och använda en SQL-baserad modell för att förutsäga kundbortfall. Med denna grund kan ni analysera kundbeteenden, identifiera riskkunder och implementera förebyggande strategier för att behålla kunderna. Om du vill förbättra och tillämpa din modell för bortfallsförutsägelse ytterligare ska du göra följande:

- Automatisera processen: Integrera modellen i en dataledning för kontinuerlig övervakning och realtidsinsikter. [Utforska hur du verifierar och bearbetar datauppsättningar med SQL](../../../dashboards/query.md).
- Övervaka modellens prestanda: Utvärdera modellen kontinuerligt med nya data för att bibehålla noggrannheten och relevansen.  Använd [AI Assistant](../../../ai-assistant/landing.md) i Adobe Experience Platform-gränssnittet för att övervaka viktiga prestandaändringar och [prognostisera målgruppstrender](../../../ai-assistant/new-features/audience-forecasting.md).
