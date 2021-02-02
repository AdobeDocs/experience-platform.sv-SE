---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Query Service;spark sql;Spark sql;spark;spark sql functions;functions;
solution: Experience Platform
title: Spark SQL-funktioner
topic: spark sql functions
description: Den här dokumentationen innehåller information om Spark SQL-funktioner som utökar SQL-funktioner.
translation-type: tm+mt
source-git-commit: 019de34c5e4ac53d38887752e893733f843dd22f
workflow-type: tm+mt
source-wordcount: '3890'
ht-degree: 0%

---


# [!DNL Spark] SQL-funktioner

Adobe Experience Platform Query Service innehåller flera inbyggda Spark SQL-funktioner som utökar SQL-funktionerna. I det här dokumentet visas Spark SQL-funktioner som stöds av Query Service.

Mer detaljerad information om funktionerna, inklusive syntax, användning och exempel, finns i [Spark SQL function documentation](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Alla funktioner i den externa dokumentationen stöds inte.

## Kategorier

- [Matematik- och statistikoperatorer och -funktioner](#math)
- [Logiska operatorer](#logical-operators)
- [Datum-/tidsfunktioner](#datetime-functions)
- [Arrayer](#arrays)
- [Datatypsdatatypsbytefunktioner](#datatype-casting)
- [Konverterings- och formateringsfunktioner](#conversion)
- [Utvärdering av data](#data-evaluation)
- [Aktuell information](#current-information)
- [Funktioner för högre ordning](#higher-order)

## Matematik- och statistikoperatorer och -funktioner {#math}

| Operator/funktion | Beskrivning |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_2) | Returnerar resten av de två talen |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_4) | Multiplicerar de två talen |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Lägger till de två talen |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Subtraherar de två talen |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Dividerar de två talen |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Returnerar indatans absoluta värde |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Returnerar det inverterade cosinusvärdet |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Returnerar beräknad kardinalitet av HyperLog++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Returnerar det ungefärliga percentilvärdet vid den angivna procentandelen |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Returnerar det inverterade sinusvärdet |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Returnerar det inverterade tangentvärdet |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Returnerar vinkeln mellan det positiva x-axelplanet och de punkter som anges av koordinaterna |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Returnerar det genomsnittliga värdet |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Returnerar kubroten |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) eller  [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Returnerar det minsta heltalet som inte är större än det inmatade värdet |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Konvertera från en bas till en annan |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Returnerar Pearson-koefficienten mellan talen |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Returnerar cosinusvärdet |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Returnerar det hyperboliska cosinusvärdet |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Returnerar cotangent-värdet |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Returnerar rangordningen för ett värde i en grupp med värden |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Returnerar Eulers tal |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Returnerar e upphöjt till värdet |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Returnerar e upphöjt till värdet minus 1 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Returnerar värdets fakultet |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Returnerar det största heltalet som inte är mindre än värdet |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Returnerar det största värdet för alla parametrar |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Returnerar hypotensionen för de två angivna värdena |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Returnerar kurtosvärdet från gruppen |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Returnerar det minsta värdet för alla parametrar |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Returnerar den naturliga logaritmen för värdet |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Returnerar värdets logaritm |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Returnerar logaritmen av värdet i bas 10 |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Returnerar logaritmen för värdet plus 1 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Returnerar logaritmen av värdet i bas 2 |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Returnerar det maximala värdet för uttrycket |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Returnerar medelvärdet som beräknats från värdena |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Returnerar det minsta värdet för uttrycket |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Returnerar monotont ökande ID:n |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Returnerar det negerade värdet |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Returnerar procentrangordningen för ett värde |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Returnerar den exakta percentilen vid en angiven procentandel |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Returnerar den ungefärliga percentilen vid en given procentandel |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Returnerar pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Returnerar den positiva modulon mellan två värden |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Returnerar det positiva värdet |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Returnerar det första värdet till det andra värdets potens |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Konverterar värdet till radianer |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Returnerar ett slumpmässigt tal mellan 0 och 1 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Returnerar ett slumpmässigt värde |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Returnerar det närmaste dubbla värdet |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Returnerar det närmaste avrundade värdet |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign),  [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Returnerar talets tecken |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Returnerar sinus för värdet |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Returnerar hyperbolisk sinus för värdet |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Returnerar kvadratroten av värdet |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Returnerar standardavvikelsen för värdet |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Returnerar populationens standardavvikelse för värdet |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Returnerar exempelstandardavvikelsen för värdet |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Returnerar summan av värdena |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Returnerar värdets tangent |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Returnerar hyperbolisk tangens för värdet |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Returnerar den beräknade populationsvariationen |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp),  [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Returnerar den beräknade samplingsavvikelsen |

### Logiska operatorer och funktioner {#logical-operators}

| Operator/funktion | Beskrivning |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) eller  [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Logiskt inte |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Less than |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Less than or equal to |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_10) | Equal to |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Greater than |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Greater than or equal to |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Bitvis exklusiv eller |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Större än eller lika med |
| [`|`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Bitvis eller |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitvis inte |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Returnerar de gemensamma elementen |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Kontrollerar om uttrycket är sant |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Om uttrycket utvärderas till true returnerar du det andra uttrycket. Annars returnerar du det tredje uttrycket. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Om uttrycket är null returneras det andra uttrycket. Annars returneras det första uttrycket. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Returnerar true om det första uttrycket finns i något av de efterföljande uttrycken. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Returnerar true om värdet inte är ett tal |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Returnerar true om värdet inte är null |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Returnerar true om värdet är null |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Returnerar det första uttrycket om det inte är ett tal, returnerar annars det andra uttrycket |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Logiskt eller |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | När kan användas för att skapa förgreningsvillkor för jämförelse |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Returnerar true om XPath-uttrycket utvärderas till true eller om en matchande nod hittas |

### Datum-/tidsfunktioner {#datetime-functions}

|  -funktion | Beskrivning |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Lägg till månader till datum |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Lägg till dagar till datum |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Ändra datumformat |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Ta bort dagar från datum |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Returnerar det datum som trunkeras till den angivna enheten |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Returnerar skillnaden mellan datum i dagar |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day),  [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Returnerar dagen i månaden |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Returnerar veckodag (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Returnerar dag på året |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Returnerar datum i Unix-tid |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Returnerar datum i UTC-tid |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Returnerar timmen för indata |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Returnerar den sista dagen i månaden som datumet tillhör |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Returnerar minuten för indata |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Returnerar månaden för indata |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Antal månader mellan |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Returnerar den första dagen senare än indata |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Returnerar inmatningens fjärdedel |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Returnerar den andra delen av strängen |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Konverterar strängen till ett datum |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Konverterar strängen till en tidsstämpel |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Konverterar strängen till en Unix-tidsstämpel |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Konverterar strängen till en UTC-tidsstämpel |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Trunkerar datumet |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Returnerar Unix-tidsstämpeln |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Veckodag (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Returnerar veckan på året för ett givet datum |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Returnerar året för strängen |

### Matriser {#arrays}

|  -funktion | Beskrivning |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Skapar en array med de angivna elementen |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Kontrollerar om arrayen innehåller värdet |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Tar bort dubblettvärden från arrayen |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Returnerar en array med elementen i den första arrayen, men inte den andra |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Returnerar skärningspunkten för de två arrayerna |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Sammanfogar två arrayer |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Returnerar det maximala värdet för arrayen |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Returnerar det minsta värdet för arrayen |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Returnerar elementets 1-baserade position |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Tar bort alla element som är lika med elementet |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Skapar en array som innehåller det värde som räknas gånger |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Sorterar arrayen |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Sammanfogar arrayen utan några dubbletter |
| [`array_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Postnummer |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Returnera arrayens storlek |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Returnera elementet vid positionen |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Separera element i en array i flera rader, exklusive null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Separera element i en array i flera rader, inklusive null |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Returnerar arrayens 1-baserade position |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Förenklar en array med arrayer |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Separat array med strukturer i en tabell, exklusive null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Separat array med strukturer i en tabell, inklusive null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Separera element i en array i flera rader med positioner, exklusive null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Separera element i en array i flera rader med positioner, inklusive null |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Invertera elementen i arrayen |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Returnera en slumpmässig permutation av arrayen |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Delar en array |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Sortera en array, ange en ordning |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Sammanfogar de två arrayerna till en enda array innan en funktion används |

### Datatypsdatatypsbytesfunktioner {#datatype-casting}

|  -funktion | Beskrivning |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Ändra datatypen till bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Ändra datatypen till binär |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Ändra datatypen till boolesk |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Ändra datatypen till den angivna typen |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Ändra datatypen till datum |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Ändra datatypen till decimal |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Ändra datatypen till dubbel |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Ändra datatypen till flyttal |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Ändra datatypen till int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Ändra datatypen till small |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Skapa en karta från en sträng |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Ändra datatypen till sträng |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Skapa en struktur |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Ändra datatypen till tinyint |

### Konverterings- och formateringsfunktioner {#conversion}

|  -funktion | Beskrivning |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Returnera det numeriska värdet (ASCII) |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Ändra argumentet till en base64-sträng |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Ändra argumentet till ett binärt värde |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Returnera bitlängden |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char),  [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Returnera ASCII-tecknet |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length),  [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Returnera stränglängden |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Returnerar det cykliska värdet för redundanskontrollen |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Konvertera radianer till grader |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Ändra talets format |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json),  [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Hämta data från JSON |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Returnera hash-värdet |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Konvertera argumentet till ett hexadecimalt värde |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Ändrar strängen så att den får ett namnslut |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase),  [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Ändrar strängen till gemener |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Knuffar den vänstra sidan av en sträng |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Skapa en karta |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Skapa en karta från en array |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Skapa en karta från en array med strukturer |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Returnera md5-värdet |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Placerar höger sida i en sträng |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Tar bort avslutande blanksteg |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha),  [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | Returnera SHA1-värdet |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | Returnera SHA2-värdet |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Returnera ljudindexkoden |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Dela upp värden i rader |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr),  [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Returnera delsträngen |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Returnerar en JSON-sträng |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Ersätt värden i sträng |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Ta bort inledande och avslutande tecken |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase),  [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Ändra strängen till versaler |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Konvertera base64-strängen till binär |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Konvertera det hexadecimala till binära |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Returnera ett UUID |

### Datautvärdering {#data-evaluation}

|  -funktion | Beskrivning |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Returnera det första icke-null-argumentet |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Returnera en lista med icke-unika element |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Returnera en uppsättning unika element |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Sammanfogning |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Sammanfogning med avgränsare |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Returnerar det totala antalet rader |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Avkoda med en teckenuppsättning |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Returnera [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)th input |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Koda med en teckenuppsättning |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first),  [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Returnerar det första värdet |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Anger om en kolumn är grupperad |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Returnerar grupperingsnivån |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Returnerar ett 1-baserat index för teckenförekomst |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Returnerar en tuppel från en JSON-inmatning |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag),  [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Returnerar värdet före förskjutningen |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last),  [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Returnerar det sista värdet |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Returnerar de första [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) tecknen |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Returnerar strängens längd |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Returnerar Levenshetin-avståndet mellan strängar |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate),  [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Returnerar positionen för den första förekomsten av en delsträng |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Sammanfoga en karta |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Returnera knapparna för en karta |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Returnera värden för en karta |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Dela upp rader i partitioner |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Returnerar null om true |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Returnerar värdet om null |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Returnerar värdet om det inte är null |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extraherar en del av en URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Beräknar rangordningen för ett värde |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extraherar något som matchar regex |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Ersätter något som matchar regex |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Returnerar en sträng som upprepas |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Ersätta alla förekomster av en sträng |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Skapa en flerdimensionell sammanslagning |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Tilldelar ett unikt radnummer |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Returnerar schemat för JSON |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Delar upp strängen i en array med ord |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Genererar en array med element |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Signerat bitvis skift åt vänster |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Signerat bitvis skift åt höger |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Bitflyttning utan tecken höger |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Returnera arrayens storlek |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Returnera en sträng med [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) blanksteg |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Delad sträng |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Returnera index för delsträng |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Fönster |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Tolka XML-noder |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double),  [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Tolka XML-noder för dubbla |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Tolka XML-noder för flytande |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Tolka XML-noder för heltal |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Tolka XML-noder för lång tid |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | Tolka XML-noder för kort heltal |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Tolka XML-noder för sträng |

### Aktuell information {#current-information}

|  -funktion | Beskrivning |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Returnerar aktuell databas |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Returnerar aktuellt datum |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp),  [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Returnerar aktuell tidsstämpel |

### Funktioner för högre ordning {#higher-order}

|  -funktion | Beskrivning |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Omforma element i en array |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Kontrollera om elementet finns |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtrera inmatningsarrayen |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Använda en binär operator för alla element |