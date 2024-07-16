---
title: Hantera matriser och mappa datatyper med funktioner i högre ordning
description: Lär dig hur du hanterar matriser och mappar datatyper med funktioner för högre ordning i frågetjänsten. Praktiska exempel finns i vanliga användningsfall.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Hantera matriser och mappa datatyper med funktioner i högre ordning

Använd den här vägledningen när du vill lära dig hur funktioner i högre ordning kan bearbeta komplexa datatyper, som arrayer och kartor. Dessa funktioner tar bort behovet av att ta bort arrayen, utföra en funktion och sedan kombinera resultatet. Funktioner i högre ordning är särskilt användbara för att analysera eller bearbeta tidsseriedatauppsättningar och analyser, som ofta innehåller komplexa kapslade strukturer, arrayer, kartor och olika användningsfall.

Följande lista över användningsfall innehåller exempel på funktioner för arrayhantering i högre ordning och mappningsmanipulering.

## Använd omformning för att justera prissumman med n {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

Ovanstående kodutdrag använder en funktion för varje element i arrayen och returnerar en ny array med omformade element. Funktionen `transform` tar en array av typen T och konverterar varje element från typen T till typ U. Sedan returneras en array av typen U. De faktiska typerna T och U beror på den specifika användningen av omformningsfunktionen.

`transform(array<T>, function<T, Int, U>): array<U>`

Den här arrayomformningsfunktionen liknar det föregående exemplet, men det finns två argument för funktionen. Det andra argumentet i den här funktionen tar även emot indexvärdet för elementet i arrayen utöver att omformas.

**Exempel**

I SQL-exemplet nedan visas det här användningsexemplet. Frågan hämtar en begränsad uppsättning rader från den angivna tabellen och omformar `productListItems`-arrayen genom att multiplicera `priceTotal`-attributet för varje objekt med 73. Resultatet innehåller kolumnerna `_id`, `productListItems` och omformade `price_in_inr`. Markeringen baseras på ett specifikt tidsstämpelintervall.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## Det finns redan en funktion för att ta reda på om det finns en produkt med en specifik SKU {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

I fragmentet ovan tillämpas funktionen `exists` på alla element i arrayen och returnerar ett booleskt värde. Det booleska värdet anger om det finns ett eller flera element i arrayen som uppfyller ett angivet villkor. I det här fallet bekräftar den om det finns en produkt med en specifik SKU.

**Exempel**

I SQL-exemplet nedan hämtar frågan `productListItems` från tabellen `geometrixxx_999_xdm_pqs_1batch_10k_rows` och utvärderar om det finns ett element med en SKU som är lika med `123679` i arrayen `productListItems`. Sedan filtreras resultaten baserat på ett visst intervall med tidsstämplar och slutresultatet begränsas till tio rader.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## Använd filter för att hitta produkter där SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

Den här funktionen filtrerar en array med element baserat på ett givet villkor som utvärderar varje element som ett booleskt värde. Sedan returneras en ny array som bara innehåller element där villkoret returnerade ett true-värde.

**Exempel**

Frågan nedan markerar kolumnen `productListItems`, använder ett filter för att endast inkludera element med en SKU som är större än 10000 och begränsar resultatet som angetts till rader inom ett visst tidsstämpelintervall. Den filtrerade arrayen kantutjämnas sedan som `_filter` i utdata.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## Använd aggregat för att summera SKU:er för alla produktlisteobjekt som är kopplade till ett specifikt ID och fördubbla den resulterande totalen {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

Den här aggregeringsåtgärden använder en binär operator på ett initialt läge och alla element i arrayen. Det minskar också flera värden till ett enda läge. Efter den här reduceringen konverteras det slutliga läget sedan till det slutliga resultatet med en avslutningsfunktion. Slutfunktionen tar det senaste läget som erhålls när den binära operatorn har använts på alla arrayelement och gör något med den för att skapa det slutliga resultatet.

**Exempel**

Det här frågeexemplet beräknar det maximala SKU-värdet från arrayen `productListItems` inom det angivna tidsstämpelintervallet och dubblerar resultatet. Utdata innehåller den ursprungliga `productListItems`-arrayen och den beräknade `max_value`.

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## Använd zip_with för att tilldela ett sekvensnummer till alla objekt i produktlistan {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

Detta kodutdrag kombinerar elementen i två arrayer till en enda ny array. Åtgärden utförs oberoende av varje element i arrayen och genererar värdepar. Om en array är kortare läggs null-värden till för att matcha längden på den längre arrayen. Detta inträffar innan funktionen används.

**Exempel**

Följande fråga använder funktionen `zip_with` för att skapa värdepar från två arrayer. Det gör du genom att lägga till SKU-värdena från arrayen `productListItems` i en heltalssekvens, som genererades med funktionen `Sequence`. Resultatet markeras tillsammans med den ursprungliga kolumnen `productListItems` och begränsas baserat på ett tidsstämpelintervall.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## Använd map_from_entries för att tilldela ett sekvensnummer till varje objekt i produktlistan och få det slutliga resultatet som en karta {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

Detta kodutdrag konverterar en array med nyckelvärdepar till en karta. Det är användbart när du hanterar nyckelvärdepar som skulle kunna dra nytta av en mer strukturerad och effektiv struktur.

**Exempel**

Följande fråga skapar värdepar från en sekvens och arrayen productListItems, konverterar dessa par till en karta med map_from_entries och markerar sedan den ursprungliga kolumnen productListItems tillsammans med den nyligen skapade kolumnen map_from_entries. Resultatet filtreras och begränsas baserat på det angivna tidsstämpelintervallet.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Använd map_form_arrays för att tilldela sekvensnummer till objekt i produktlistan och returnera resultatet som en karta {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

Funktionen `map_form_arrays` skapar en karta med parade värden från två arrayer.

>[!IMPORTANT]
>
>Det ska inte finnas några null-element i nycklarna.

**Exempel**

SQL nedan skapar en karta där nycklarna är sekvensnummer som genereras med funktionen `Sequence` och värdena är element från arrayen `productListItems`. Frågan markerar kolumnen `productListItems` och använder funktionen `Map_from_arrays` för att skapa kartan baserat på den genererade nummersekvensen och elementen i arrayen. Resultatet begränsas till tio rader och filtreras baserat på ett tidsstämpelintervall.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Använd map_concat för att sammanfoga två kartor till en enda karta {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

Funktionen `map_concat` i fragmentet ovan tar flera kartor som argument och returnerar en ny karta som kombinerar alla nyckel/värde-par från indatamappningarna. Funktionen sammanfogar flera kartor till en enda karta, och den resulterande kartan innehåller alla nyckelvärdepar från indatamappningarna.

**Exempel**

SQL nedan skapar en karta där varje objekt i `productListItems` är associerat med ett sekvensnummer som sedan sammanfogas med en annan karta där nycklar genereras i ett visst sekvensintervall.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Använd element_at för att hämta ett värde som motsvarar AAID i identitetskartan för ytterligare beräkning {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

För arrayer returnerar fragmentet elementet vid ett angivet (1-baserat) index eller det värde som är associerat med en nyckel i en karta. Om indexvärdet är &lt; 0 får det åtkomst till element från det sista till det första och returnerar null om indexvärdet överskrider arrayens längd.

För kartor returnerar den antingen ett värde för den angivna nyckeln eller null om nyckeln inte finns på kartan.

**Exempel**

Frågan markerar kolumnen `identitymap` från tabellen `geometrixxx_999_xdm_pqs_1batch_10k_rows` och extraherar värdet som är associerat med nyckeln `AAID` för varje rad. Resultatet begränsas till rader som ligger inom det angivna tidsstämpelintervallet och frågan begränsar utdata till tio rader.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## Använd kardinalitet för att hitta antalet identiteter i identitetskartan {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

Det här fragmentet returnerar storleken på en viss array eller karta och ger ett alias. Den returnerar -1 om värdet är null.

**Exempel**

Frågan nedan hämtar kolumnen `identitymap` och funktionen `Cardinality` beräknar antalet element i varje karta i `identitymap`. Resultaten begränsas till tio rader och filtreras baserat på ett angivet tidsstämpelintervall.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## Använd array_distincför att hitta distinkta element i productListItems {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

Ovanstående kodutdrag tar bort dubblettvärden från den angivna arrayen.

**Exempel**

Frågan nedan markerar kolumnen `productListItems`, tar bort dubblettobjekt från arrayerna och begränsar utdata till tio rader baserat på ett angivet tidsstämpelintervall.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultat**

Resultaten för denna SQL skulle se ut ungefär som de nedan.

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### Ytterligare funktioner för högre ordning {#additional-higher-order-functions}

Följande exempel på funktioner i högre ordning förklaras som en del av hämtningen av liknande poster använder skiftläget. Ett exempel och en förklaring till hur de olika funktionerna används finns i respektive avsnitt i dokumentet.

Funktionsexemplet [`transform` ](../use-cases/retrieve-similar-records.md#length-adjustment) beskriver tokeniseringen för en produktlista.

Funktionsexemplet [`filter` ](../use-cases/retrieve-similar-records.md#filter-results) visar en mer detaljerad extrahering av relevant information från textdata.

[`reduce`-funktionen ](../use-cases/retrieve-similar-records.md#higher-order-function-solutions) erbjuder ett sätt att härleda kumulativa värden eller aggregat, som kan vara avgörande i olika analys- och planeringsprocesser.
