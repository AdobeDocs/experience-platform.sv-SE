---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Spark SQL-funktioner
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a23ee02a9e801531a38b5ff70ef07497aa21b174

---


# Spark SQL-funktioner

Spark SQL-hjälparna har inbyggda Spark SQL-funktioner som utökar SQL-funktionerna.

Referens: Dokumentation för [Spark SQL-funktionen](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE] Alla funktioner i den externa dokumentationen stöds inte.

## Kategorier

- [Matematik- och statistikoperatorer och -funktioner](#math-and-statistical-operators-and-functions)
- [Logiska operatorer](#logical-operators)
- [Datum-/tidsfunktioner](#date/time-functions)
- [Sammanställningsfunktioner](#aggregate-functions)
- [Arrayer](#arrays)
- [Datatypsdatatypsbytefunktioner](#datatype-casting-functions)
- [Konverterings- och formateringsfunktioner](#conversion-and-formatting-functions)
- [Utvärdering av data](#data-evaluation)
- [Aktuell information](#current-information)

### Matematik- och statistikoperatorer och -funktioner

#### Modulo

`expr1 % expr2`: Returnerar resten efter `expr1`/`expr2`.

Exempel:

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Multiplicera

`expr1 * expr2`: Returnerar `expr1`*`expr2`.

Exempel:

```
> SELECT 2 * 3;
 6
```

#### Lägg till

`expr1 + expr2`: Returnerar `expr1`+`expr2`.

Exempel:

```
> SELECT 1 + 2;
 3
```

#### Subtrahera

`expr1 - expr2`: Returer `expr1`-`expr2`.

Exempel:

```
> SELECT 2 - 1;
 1
```

#### Dela

`expr1 / expr2`: Returnerar `expr1`/`expr2`. Den utför alltid flyttalsdivision.

Exempel:

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`: Returnerar det absoluta värdet av det numeriska värdet.

Exempel:

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`: Returnerar den inverterade cosinus (kallas även arc cosinus) för `expr`, som om den beräknas av `java.lang.Math.acos`.

Exempel:

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### ca_percentil

`approx_percentile(col, percentage [, accuracy])`: Returnerar det ungefärliga percentilvärdet för en numerisk kolumn `col` vid den angivna procentandelen. Procentvärdet måste vara mellan 0,0 och 1,0. Parametern `accuracy` (standard: 10000) är en positiv numerisk litteral som kontrollerar ungefärlig noggrannhet till minneskostnad. Ett högre värde för `accuracy` ger bättre noggrannhet, `1.0/accuracy` är det relativa felet för approximationen. När `percentage` är en array måste varje värde i den procentuella arrayen vara mellan 0,0 och 1,0. I det här fallet returneras den ungefärliga percentilmatrisen för kolumnen `col` vid den angivna procentarrayen.

Exempel:

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`: Returnerar den inverterade sinus (kallas även arcussinus), bågsinus för `expr`, som om den beräknats av `java.lang.Math.asin`.

Exempel:

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`: Returnerar den inverterade tangenten (kallas även arc tangent) för `expr`, som om den beräknas av `java.lang.Math.atan`

Exempel:

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: Returnerar vinkeln i radianer mellan den positiva x-axeln i ett plan och den punkt som anges av koordinaterna (`exprX`, `exprY`), som om den beräknats av `java.lang.Math.atan2`.

Argument:

`exprY`: Koordinat på y-axel`exprX`: Koordinera på x-axel

Exempel:

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: Returnerar medelvärdet som beräknas från värden i en grupp.

#### kardinalitet

`cardinality(expr)`: Returnerar storleken på en array eller karta. Funktionen returnerar -1 om dess indata är null och `spark.sql.legacy.sizeOfNull` är inställd på true (standard). Om värdet `spark.sql.legacy.sizeOfNull` är false returneras null för null-indata.

Exempel:

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`: Returnerar kubroten för `expr`.

Exempel:

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: Returnerar det minsta heltalet som inte är mindre än `expr`.

Exempel:

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### tak

`ceiling(expr)`: Returnerar det minsta heltalet som inte är mindre än `expr`.

Exempel:

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`: Konvertera `num` från `from_base` till `to_base`

Exempel:

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### korr

`corr(expr1, expr2)`: Returnerar Pearson-korrelationskoefficienten mellan en uppsättning sifferpar.

#### cos

`cos(expr)`: Returnerar cosinus för `expr`, som om det beräknats av `java.lang.Math.cos`.

Exempel:

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`: Returnerar hyperbolisk cosinus för `expr`, som om den beräknas av `java.lang.Math.cosh`.

Argument:
- `expr`: Hyperbolisk vinkel

Exempel:

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)`: Returnerar cotangens för `expr`, som om den beräknas av `1/java.lang.Math.cot`.

Argument:
- `expr`: Vinkel i radianer

Exempel:

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`: Beräknar rangordningen för ett värde i en grupp med värden. Resultatet är ett plus det tidigare tilldelade rangvärdet. Till skillnad från funktionen `rank`skapar `dense_rank` inte mellanrum i rangordningssekvensen.

#### e

`e()`: Returnerar Eulers tal, e.

Exempel:

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: Returnerar e till styrkan hos `expr`.

Exempel:

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: Returnerar exp(`expr`) - 1.

Exempel:

```
> SELECT expm1(0);
 0.0
```

#### faktoriell

`factorial(expr)`: Returnerar fakulteten för `expr`. `expr` är [0..20]. Annars null.

Exempel:

```
> SELECT factorial(5);
 120
```

#### floor

`floor(expr)`: Returnerar det största heltalet som inte är större än `expr`.

Exempel:

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### störst

`greatest(expr, ...)`: Returnerar det största värdet av alla parametrar, och hoppar över null-värden.

Exempel:

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypotek

`hypot(expr1, expr2)`: Returnerar sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>).

Exempel:

```
> SELECT hypot(3, 4);
 5.0
```

#### kurtosis

`kurtosis(expr)`: Returnerar kurtosvärdet som beräknas utifrån värden för en grupp.


#### minst

`least(expr, ...)`: Returnerar det minsta värdet för alla parametrar, och hoppar över null-värden.

Exempel:

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)`: Returnerar Levenshetin-avståndet mellan de två givna strängarna.

Exempel:

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: Returnerar den naturliga logaritmen (bas e) för `expr`.

Exempel:

```
> SELECT ln(1);
 0.0
```

#### logg

`log(base, expr)`: Returnerar logaritmen för `expr` med `base`.

Exempel:

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: Returnerar logaritmen för `expr` med basen 10.

Exempel:

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Returnerar `log(1 + expr)`.

Exempel:

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: Returnerar logaritmen för `expr` med bas 2.

Exempel:

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: Returnerar det högsta värdet för `expr`.

#### medelvärde

`mean(expr)`: Returnerar medelvärdet som beräknas från värden i en grupp.

#### min

`min(expr)`: Returnerar det minsta värdet för `expr`.

#### monotonically_increase_id

`monotonically_increasing_id()`: Returnerar monotont ökande 64-bitars heltal. Det genererade ID:t kommer garanterat att öka monotont och vara unikt, men inte i följd. Den aktuella implementeringen placerar partitions-ID i de övre 31 bitarna och de nedre 33 bitarna representerar postnumret i varje partition. Antagandet är att dataramen har mindre än 1 miljard partitioner och att varje partition har mindre än 8 miljarder poster. Funktionen är icke-deterministisk eftersom dess resultat är beroende av partitions-ID:n.

#### negativ

`negative(expr)`: Returnerar det negativa värdet för `expr`.

Exempel:

```
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`: Beräknar den procentuella rangordningen av ett värde i en grupp med värden.

#### percentil

`percentile(col, percentage [, frequency])`: Returnerar det exakta percentilvärdet för den numeriska kolumnen `col` vid den angivna procentandelen. Värdet för `percentage` måste vara mellan 0,0 och 1,0. Värdet för `frequency` ska vara en positiv integral.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: Returnerar den exakta percentilvärdesarrayen för en numerisk kolumn `col` vid de angivna procentsatserna. Varje värde i procentarrayen måste vara mellan 0,0 och 1,0. Värdet för `frequency` ska vara en positiv integral.

#### percentil_ca

`percentile_approx(col, percentage [, accuracy])`: Returnerar det ungefärliga percentilvärdet för en numerisk kolumn `col` vid den angivna procentandelen. Värdet för `percentage` måste vara mellan 0,0 och 1,0. Parametern `accuracy` (standard: 10000) är en positiv numerisk litteral som kontrollerar ungefärlig noggrannhet till minneskostnad. Ett högre värde för `accuracy` ger bättre noggrannhet, `1.0/accuracy` är det relativa felet för approximationen. När `percentage` är en array måste varje värde i den procentuella arrayen vara mellan 0,0 och 1,0. I det här fallet returneras den ungefärliga percentilmatrisen för kolumnen `col` vid den angivna procentmatrisen.

Exempel:

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`: Returnerar pi.

Exempel:

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`: Returnerar det positiva värdet för `expr1` mod `expr2`.

Exempel:

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positiv

`positive(expr)`: Returnerar det positiva värdet för `expr`

#### pow

`pow(expr1, expr2)`: Startar `expr1` till `expr2`.

Exempel:

```
> SELECT pow(2, 3);
 8.0
```

#### effekt

`power(expr1, expr2)`: Startar `expr1` till `expr2`.

Exempel:

```
> SELECT power(2, 3);
 8.0
```

#### radianer

`radians(expr)`: Konverterar grader till radianer.

Argument:

- `expr`: Vinkel i grader

Exempel:

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`: Returnerar ett slumpmässigt värde med oberoende och identiskt fördelade (i.i.d.) värden som är jämnt fördelade i (0, 1).

Exempel:

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE] Den här funktionen är i allmänhet icke-deterministisk.

#### slumpmässig

`randn([seed])`: Returnerar ett slumpmässigt värde med oberoende och identiskt fördelade (i.d.) värden som hämtats från standardnormalfördelningen.

Exempel:

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE] Den här funktionen är i allmänhet icke-deterministisk.

#### utskrift

`rint(expr)`: Returnerar det dubbla värdet som är närmast argumentet och är lika med ett matematiskt heltal.

Exempel:

```
> SELECT rint(12.3456);
 12.0
```

#### rund

`round(expr, d)`: Returnerar `expr` avrundat till `d` decimaler med avrundningsläget HALF_UP.

Exempel:

```
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)`: Returnerar -1,0, 0,0 eller 1,0 eftersom `expr` är negativt, 0 eller positivt.

Exempel:

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`: Returnerar -1,0, 0,0 eller 1,0 eftersom `expr` är negativt, 0 eller positivt.

Exempel:

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`: Returnerar sinus för `expr`, som om det beräknats av `java.lang.Math.sin`.

Argument:

- `expr`: Vinkel i radianer

Exempel:

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`: Returnerar hyperbolisk sinus för `expr`, som om den beräknats av `java.lang.Math.sinh`.

Argument:

- `expr`: Hyperbolisk vinkel

Exempel:

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: Returnerar kvadratroten av `expr`.

Exempel:

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: Returnerar den exempelstandardavvikelse som beräknas från värden i en grupp.

#### stddev_pop

`sttdev_pop(expr)`: Returnerar den populationsstandardavvikelse som beräknas från värden för en grupp.

#### stddev_samp

`stddev_samp(expr)`: Returnerar den exempelstandardavvikelse som beräknas från värden i en grupp.

#### summa

`sum(expr)`: Returnerar summan som beräknas från värden i en grupp.

#### tan

`tan(expr)`: Returnerar tangenten för `expr`, som om den beräknats av `java.lang.Math.tan`.

Argument:

- `expr`: Vinkel i radianer

Exempel:

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`: Returnerar hyperbolisk tangens för `expr`, som om den beräknas av `java.lang.Math.tanh`.

Argument:

- `expr`: Hyperbolisk vinkel

Exempel:

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`: Returnerar populationsvariationen beräknad utifrån värden för en grupp.

#### Var_samp

`var_samp(expr)`: Returnerar samplingsvariansen som beräknas från värden i en grupp.

#### avvikelse

`variance(expr)`: Returnerar samplingsvariansen som beräknas från värden i en grupp.

### Logiska operatorer

#### Logiskt inte

`! expr`: Logiskt inte.

#### Mindre än

`expr1 < expr2`: Returnerar true om `expr1` är mindre än `expr2`.

Argument:

- `expr1, expr2`: De två uttrycken måste vara av samma typ eller så kan de bytas ut mot en gemensam typ och måste vara en typ som kan ordnas. Mappningstypen kan till exempel inte ordnas, så den stöds inte. För komplexa typer som matris/struktur måste datatyperna för fält vara sorterbara.

Exempel:

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### Mindre än eller lika med

`expr1 <= expr2`: Returnerar true om `expr1` är mindre än eller lika med `expr2`.

Argument:

- `expr1, expr2`: De två uttrycken måste vara av samma typ eller kan bytas ut mot en gemensam typ och måste vara en typ som kan ordnas. Mappningstypen kan till exempel inte ordnas, så den stöds inte. För komplexa typer som matris/struktur måste datatyperna för fälten vara sorterbara.

Exempel:

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### Lika med

`expr1 = expr2`: Returnerar true om `expr1` är lika med `expr2`eller false i annat fall.

Argument:

- `expr1, expr2`: De två uttrycken måste vara av samma typ eller så kan de bytas ut mot en gemensam typ, och de måste vara en typ som kan användas vid likhetsjämförelse. Karttypen stöds inte. För komplexa typer som matris/struktur måste datatyperna för fält vara sorterbara.

Exempel:

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### Större än

`expr1 > expr2`: Returnerar true om `expr1` är större än `expr2`.

Argument:

- `expr1, expr2`: De två uttrycken måste vara av samma typ eller så kan de bytas ut mot en gemensam typ och måste vara en typ som kan ordnas. Mappningstypen kan till exempel inte ordnas, så den stöds inte. För komplexa typer som matris/struktur måste datatyperna för fält vara sorterbara.

Exempel:

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### Större än eller lika med

`expr1 >= expr2`: Returnerar true om `expr1` är större än eller lika med `expr2`.

Argument:

- `expr1, expr2`: De två uttrycken måste vara av samma typ eller så kan de bytas ut mot en gemensam typ och måste vara en typ som kan ordnas. Mappningstypen kan till exempel inte ordnas, så den stöds inte. För komplexa typer som matris/struktur måste datatyperna för fält vara sorterbara.

Exempel:

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Bitvis exklusiv eller

`expr1 ^ expr2`: Returnerar resultatet av OR i bitform exklusivt för `expr1` och `expr2`.

Exempel:

```
> SELECT 3 ^ 5;
 2
```

#### och

`expr1 and expr2`: Logiskt AND.

#### arrayer_overlap

`arrays_overlap(a1, a2)`: Returnerar true om a1 innehåller minst ett element som inte är null och som också finns i a2. Om arrayerna inte har något gemensamt element och båda är icke-tomma och någon av dem innehåller ett null-element, returneras null. Annars returneras false.

Exempel:

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Sedan: 2.4.0

#### assert_true

`assert_true(expr)`: Utlöser ett undantag om `expr` inte är true.

Exempel:

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`: Om `expr1` utvärderas till true returneras `expr2`; annars returneras `expr3`.

Exempel:

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`: Returnerar `expr2` om `expr1` är null eller `expr1` inte.

Exempel:

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: Returnerar true om `expr` är lika med valfritt valN.

Argument:
- `expr1, expr2, expr3, ...`: Argumenten måste vara av samma typ.

Exempel:

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`: Returnerar true om `expr` är NaN eller false i annat fall.

Exempel:

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isNotnull

`isnotnull(expr)`: Returnerar true om `expr` inte är null eller false i annat fall.

Exempel:

```
> SELECT isnotnull(1);
 true
```

#### är null

`isnull(expr)`: Returnerar true om `expr` är null eller false i annat fall.

Exempel:

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`: Returnerar `expr1` om det inte är NaN, eller `expr2` inte.

Exempel:

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`: Logiskt inte.

#### eller

`expr1 or expr2`: Logiskt eller.

#### xpath_boolean

`xpath_boolean(xml, xpath)`: Returnerar true om XPath-uttrycket utvärderas till true eller om en matchande nod hittas.

Exempel:

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Datum-/tidsfunktioner

#### add_month

`add_months(start_date, num_months)`: Returnerar datumet som infaller `num_months` efter `start_date`.

Exempel:

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Sedan: 1.5.0

#### date_add

`date_add(start_date, num_days)`: Returnerar datumet som infaller `num_days` efter `start_date`.

Exempel:

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Sedan: 1.5.0

#### date_format

`date_format(timestamp, fmt)`: Konverterar `timestamp` till ett strängvärde i det format som anges av datumformatet `fmt`.

Exempel:

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Sedan: 1.5.0

#### date_sub

`date_sub(start_date, num_days)`: Returnerar datumet som infaller `num_days` före `start_date`.

Exempel:

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Sedan: 1.5.0

#### date_trunc

`date_trunc(fmt, ts)`: Returnerar tidsstämplar som trunkerats till den enhet som anges av formatmodellen `fmt`. `fmt` ska vara något av [&quot;YEAR&quot;, &quot;YYYY&quot;, &quot;YY&quot;, &quot;MON&quot;, &quot;MONTH&quot;, &quot;MM&quot;, &quot;DAY&quot;, &quot;DD&quot;, &quot;HOUR&quot;, &quot;MINUTE&quot;, &quot;SECOND&quot;, &quot;WEEK&quot;, &quot;QUARTER&quot;]

Exempel:

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

Sedan: 2.3.0

#### datediff

`datediff(endDate, startDate)`: Returnerar antalet dagar från `startDate` till `endDate`.

Exempel:

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Sedan: 1.5.0

#### dag

`day(date)`: Returnerar dag i månaden för datum/tidsstämpel.

Exempel:

```
> SELECT day('2009-07-30');
 30
```

Sedan: 1.5.0

#### dag i månad

`dayofmonth(date)`: Returnerar dag i månaden för datum/tidsstämpel.

Exempel:

```
> SELECT dayofmonth('2009-07-30');
 30
```

Sedan: 1.5.0

#### veckodag

`dayofweek(date)`: Returnerar veckodag för datum/tidsstämpel (1 = söndag, 2 = måndag, ..., 7 = lördag).

Exempel:

```
> SELECT dayofweek('2009-07-30');
 5
```

Sedan: 2.3.0

#### dagÅr

`dayofyear(date)`: Returnerar dag på året för datum/tidsstämpel.

Exempel:

```
> SELECT dayofyear('2016-04-09');
 100
```

Sedan: 1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`: Returnerar `unix_time` i det angivna `format`värdet.

Exempel:

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Sedan: 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: Tolkar en tidsstämpel som &quot;2017-07-14 02:40:00.0&quot; som en tid i UTC, och återger den tiden som en tidsstämpel i den givna tidszonen. GMT+1 skulle till exempel ge 2017-07-14 03:40:00.0.

Exempel:

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Sedan: 1.5.0

#### timme

`hour(timestamp)`: Returnerar timkomponenten för strängen/tidsstämpeln.

Exempel:

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

Sedan: 1.5.0

#### last_day

`last_day(date):` Returnerar den sista dagen i månaden som datumet tillhör.

Exempel:

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

Sedan: 1.5.0

#### minut

`minute(timestamp)`: Returnerar minutkomponenten för strängen/tidsstämpeln.

Exempel:

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Sedan: 1.5.0

#### månad

`month(date)` Returnerar månadskomponenten för datum/tidsstämpel.

Exempel:

```
> SELECT month('2016-07-30');
 7
```

Sedan: 1.5.0

#### månad_mellan

`months_between(timestamp1, timestamp2[, roundOff])`: Om `timestamp1` är senare än `timestamp2`är resultatet positivt. Om `timestamp1` och `timestamp2` finns på samma dag i månaden, eller båda är den sista dagen i månaden, ignoreras tiden på dagen. I annat fall beräknas skillnaden på 31 dagar per månad och avrundas till 8 siffror om inte `roundOff=false`.

Exempel:

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Sedan: 1.5.0

#### next_day

`next_day(start_date, day_of_week)`: Returnerar det första datumet som infaller senare än `start_date` och namnges som angivet.

Exempel:

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Sedan: 1.5.0

#### kvartal

`quarter(date)`: Returnerar årets kvartal för datum, i intervallet 1 till 4.

Exempel:

```
> SELECT quarter('2016-08-31');
 3
```

Sedan: 1.5.0

#### sekund

`second(timestamp)`: Returnerar den andra komponenten i strängen/tidsstämpeln.

Exempel:

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Sedan: 1.5.0

#### to_date

`to_date(date_str[, fmt])`: Tolkar `date_str` uttrycket med `fmt` uttrycket till ett datum. Returnerar null med ogiltiga indata. Som standard följer datatypsbytet till ett datum om det `fmt` utelämnas.

Exempel:

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Sedan: 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: Tolkar `timestamp` uttrycket med `fmt` uttrycket till en tidsstämpel. Returnerar null med ogiltiga indata. Som standard följer dataregler till en tidsstämpel om den `fmt` utelämnas.

Exempel:

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Sedan: 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`: Returnerar UNIX-tidsstämpeln för den angivna tiden.

Exempel:

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Sedan: 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`: Tolkar en tidsstämpel som &quot;2017-07-14 02:40:00.0&quot; som en tid i den givna tidszonen och återger den tiden som en tidsstämpel i UTC. GMT+1 skulle till exempel ge 2017-07-14 01:40:00.0.

Exempel:

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Sedan: 1.5.0

#### trunc

`trunc(date, fmt)`: Returnerar datum med tidsdelen av dagen trunkerad till den enhet som anges av formatmodellen `fmt`. `fmt` är ett av [&quot;year&quot;,&quot;yyyy&quot;,&quot;yy&quot;,&quot;mon&quot;,&quot;month&quot;, &quot;mm&quot;]

Exempel:

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Sedan: 1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`: Returnerar UNIX-tidsstämpeln för aktuell eller angiven tid.

Exempel:

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Sedan: 1.5.0

#### veckodag

`weekday(date)`: Returnerar veckodag för datum/tidsstämpel (0 = måndag, 1 = tisdag, ..., 6 = söndag).

Exempel:

```
> SELECT weekday('2009-07-30');
 3
```

Sedan: 2.4.0

#### vecka_på_år

`weekofyear(date)`: Returnerar veckan på året för det angivna datumet. En vecka anses börja på en måndag och vecka 1 är den första veckan med >3 dagar.

Exempel:

```
> SELECT weekofyear('2008-02-20');
 8
```

Sedan: 1.5.0

#### när

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: När `expr1` = true returneras `expr2`; else when `expr3` = true, returnerar `expr4`; else returnerar `expr5`.

Argument:

- `expr1`, `expr3`: Förgreningsvillkorsuttrycken ska alla vara av boolesk typ.
- `expr2`, `expr4`, `expr5`: Förgreningsvärdeuttrycken och else-värdeuttrycket ska alla vara av samma typ eller vara bindande för en gemensam typ.

Exempel:

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### år

`year(date)`: Returnerar årskomponenten för datum/tidsstämpel.

Exempel:

```
> SELECT year('2016-07-30');
 2016
```

Sedan: 1.5.0

### Sammanställningsfunktioner

#### ca_count_distinkt

`approx_count_distinct(expr[, relativeSD])`: Returnerar den beräknade kardinaliteten av HyperLogLog++. `relativeSD` definierar det maximalt tillåtna beräkningsfelet.

### Arrayer

#### array

`array(expr, ...)`: Returnerar en array med de angivna elementen.

Exempel:

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: Returnerar true om arrayen innehåller värdet.

Exempel:

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_distinc

`array_distinct(array)`: Tar bort dubblettvärden från arrayen.

Exempel:

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Sedan: 2.4.0

#### array_except

`array_except(array1, array2)`: Returnerar en array med elementen i `array1` men inte i `array2`, utan dubbletter.

Exempel:

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Sedan: 2.4.0

#### array_intersect

`array_intersect(array1, array2)`: Returnerar en array med elementen i skärningspunkten för `array1` och `array2`, utan dubbletter.

Exempel:

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Sedan: 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`: Sammanfogar elementen i den angivna arrayen med avgränsaren och en valfri sträng som ersätter null-värden. Om inget värde anges för `nullReplacement`filtreras alla null-värden.

Exempel:

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Sedan: 2.4.0

#### array_max

`array_max(array)`: Returnerar det högsta värdet i arrayen. Null-element ignoreras.

Exempel:

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Sedan: 2.4.0

#### array_min

`array_min(array)`: Returnerar det minsta värdet i arrayen. Null-element ignoreras.

Exempel:

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Sedan: 2.4.0

#### array_position

`array_position(array, element)`: Returnerar det (1-baserade) indexvärdet för arrayens första element som långt.

Exempel:

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Sedan: 2.4.0

#### array_remove

`array_remove(array, element)`: Ta bort alla element som är lika med element från arrayen.

Exempel:

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Sedan: 2.4.0

#### array_repeat

`array_repeat(element, count)`: Returnerar arrayen med elementräkningstider.

Exempel:

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Sedan: 2.4.0

#### array_sort

`array_sort(array)`: Sorterar indatarrayen i stigande ordning. Elementen i inmatningsarrayen måste kunna ordnas. Null-element placeras i slutet av den returnerade arrayen.

Exempel:

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Sedan: 2.4.0

#### array_union

`array_union(array1, array2)`: Returnerar en array med elementen i union av `array1` och `array2`, utan dubbletter.

Exempel:

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Sedan: 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`: Returnerar en sammanfogad array med strukturer där den n:e strukturen innehåller alla N:e värden för indatarrayer.

Exempel:

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Sedan: 2.4.0

#### element_at

`element_at(array, index)`: Returnerar elementet i en array vid givet (1-baserat) index. Om `index < 0`används kommer åt element från det sista till det första. Returnerar NULL om indexvärdet överskrider matrislängden.

`element_at(map, key)`: Returnerar värdet för den angivna nyckeln eller NULL om nyckeln inte finns på kartan

Exempel:

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Sedan: 2.4.0

#### explodera

`explode(expr)`: Delar upp arrayelementen `expr` i flera rader, eller elementen i kartan `expr` i flera rader och kolumner.

Exempel:

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)`: Delar upp arrayelementen `expr` i flera rader, eller elementen i kartan `expr` i flera rader och kolumner.

Exempel:

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`: Returnerar indexvärdet (1-baserat) för den angivna strängen (`str`) i den kommaavgränsade listan (`str_array`). Returnerar 0, om strängen inte hittades eller om den angivna strängen (`str`) innehåller ett komma.

Exempel:

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### lägga

`flatten(arrayOfArrays)`: Omvandlar en array med arrayer till en enda array.

Exempel:

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Sedan: 2.4.0

#### inline

`inline(expr)`: Bryter ned en array med strukturer i en tabell.

Exempel:

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_outer

`inline_outer(expr)`: Bryter ned en array med strukturer i en tabell.

Exempel:

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### posexplodera

`posexplode(expr)`: Delar elementen i arrayen `expr` i flera rader med positioner, eller elementen i kartan `expr` i flera rader och kolumner med positioner.

Exempel:

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)`: Delar elementen i arrayen `expr` i flera rader med positioner, eller elementen i kartan `expr` i flera rader och kolumner med positioner.

Exempel:

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### reversera

`reverse(array)`: Returnerar en omvänd sträng eller en array med omvänd ordning för element.

Exempel:

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Sedan: 1.5.0
>[!NOTE] RSS-logik för arrayer är tillgänglig sedan 2.4.0.

#### blanda

`shuffle(array)`: Returnerar en slumpmässig permutation av den angivna arrayen.

Exempel:

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Sedan: 2.4.0
>[!NOTE] funktionen är icke-deterministisk.

#### segment

`slice(x, start, length)`: Delar matrisen x med början från indexstarten (eller med början från slutet om startvärdet är negativt) med den angivna längden.

Exempel:

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Sedan: 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`: Sorterar indatarrayen i stigande eller fallande ordning enligt arrayelementens naturliga ordning. Null-element placeras i början av den returnerade arrayen i stigande ordning eller i slutet av den returnerade arrayen i fallande ordning.

Exempel:

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: Sammanfogar de två angivna arrayerna, elementvis, till en enda array med hjälp av funktionen. Om en array är kortare läggs null-värden till i slutet för att matcha längden på den längre arrayen innan funktionen används.

Exempel:

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Sedan: 2.4.0

### Datatypsdatatypsbytefunktioner

#### bigint

`bigint(expr)`: Ändrar värdet `expr` till måldatatypen `bigint`.

#### binary

`binary(expr)`: Ändrar värdet `expr` till måldatatypen `binary`.

#### boolesk

`boolean(expr)`: Ändrar värdet `expr` till måldatatypen `boolean`.

#### cast

`cast(expr AS type)`: Ändrar värdet `expr` till måldatatypen `type`.

Exempel:

```
> SELECT cast('10' as int);
 10
```

#### datum

`date(expr)`: Ändrar värdet `expr` till måldatatypen `date`.

#### decimal

`decimal(expr)`: Ändrar värdet `expr` till måldatatypen `decimal`.

#### double

`double(expr)`: Ändrar värdet `expr` till måldatatypen `double`.

#### float

`float(expr)`: Ändrar värdet `expr` till måldatatypen `float`.

#### int

`int(expr)`: Ändrar värdet `expr` till måldatatypen `int`.

#### map

`map(key0, value0, key1, value1, ...)`: Skapar en karta med angivna nyckel/värde-par.

Exempel:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### smallint

`smallint(expr)`: Ändrar värdet `expr` till måldatatypen `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: Skapar en karta när texten har delats upp i nyckel-/värdepar med hjälp av avgränsare. Standardavgränsare är &#39;,&#39; för `pairDelim` och &#39;:&#39; för `keyValueDelim`.

Exempel:

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### string

`string(expr)`: Ändrar värdet `expr` till måldatatypen `string`.

#### strukturell

`struct(col1, col2, col3, ...)`: Skapar en struktur med de angivna fältvärdena.

#### tinyint

`tinyint(expr)`: Ändrar värdet `expr` till måldatatypen `tinyint`.

### Konverterings- och formateringsfunktioner

#### ascii

`ascii(str)`: Returnerar det numeriska värdet för det första tecknet i `str`.

Exempel:

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: Konverterar argumentet från en binär sträng `bin` till en base 64-sträng.

Exempel:

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`: Returnerar strängbeteckningen för det långa värdet `expr` som representeras i binärfilen.

Exempel:

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`: Returnerar bitlängden för strängdata eller antalet bitar för binära data.

Exempel:

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: Returnerar ASCII-tecknet som har den binära motsvarigheten till `expr`. Om n är större än 256 är resultatet lika med `chr(n % 256)`.

Exempel:

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: Returnerar teckenlängden för strängdata eller antalet byte för binära data. Längden på strängdata inkluderar efterföljande blanksteg. Längden på binära data inkluderar binära nollor.

Exempel:

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`: Returnerar teckenlängden för strängdata eller antalet byte för binära data. Längden på strängdata inkluderar efterföljande blanksteg. Längden på binära data inkluderar binära nollor.

Exempel:

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`: Returnerar ASCII-tecknet som har den binära motsvarigheten till expr. Om n är större än 256 är resultatet lika med `chr(n % 256)`

Exempel:

```
> SELECT chr(65);
 A
```

#### grader

`degrees(expr)`: Konverterar radianer till grader.

Argument:
- `expr`: Vinkel i radianer

Exempel:

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: Formaterar talet `expr1` som &#39;#,###,###.##&#39;, avrundat till `expr2` decimaler. Om `expr2` är 0 har resultatet inget decimaltecken eller bråkdel. `expr2` accepterar även ett användardefinierat format. Den här funktionen fungerar som MySQL:s `FORMAT`.

Exempel:

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: Returnerar ett strukturvärde med angivet `jsonStr` och `schema`.

Exempel:

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Sedan: 2.2.0

#### hash

`hash(expr1, expr2, ...)`: Returnerar ett hash-värde för argumenten.

Exempel:

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hex

`hex(expr)`: Konverterar `expr` till hexadecimal.

Exempel:

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: Returnerar `str` med den första bokstaven i varje ord med versaler. Alla andra bokstäver är i gemener. Ord avgränsas av blanktecken.

Exempel:

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`: Returneras `str` med alla tecken ändrade till gemener.

Exempel:

```
> SELECT lcase('SparkSql');
 sparksql
```

#### nedre

`lower(str)`: Returneras `str` med alla tecken ändrade till gemener.

Exempel:

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: Returnerar `str`, vänster utfyllnad med `pad` en längd av `len`. Om `str` är längre än `len`så förkortas returvärdet till `len` tecken.

Exempel:

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)`: Skapar en karta med angivna nyckel/värde-par.

Exempel:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`: Skapar en karta med ett par av de angivna nyckel-/värdesarrayerna. Element i nycklar kan inte vara null.

Exempel:

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Sedan: 2.4.0

#### map_from_entries

`map_from_entries(arrayOfEntries)`: Returnerar en karta som skapats från den angivna matrisen med poster.

Exempel:

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Sedan: 2.4.0

#### md5

`md5(expr)`: Returnerar en 128-bitars MD5-kontrollsumma som en hexsträng av `expr`.

Exempel:

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`: Returnerar `str`, högerutfyllnad med `pad` en längd av `len`. Om `str` är längre än `len`så förkortas returvärdet till `len` tecken.

Exempel:

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rensa

`rtrim(str)`: Tar bort de avslutande blankstegstecknen från `str`.

`rtrim(trimStr, str)`: Tar bort den avslutande strängen, som innehåller tecknen från trimningssträngen från `str`.

Argument:
- `str`: Ett stränguttryck
- `trimStr`: Trimma strängtecken som ska trimmas. Standardvärdet är ett blanksteg

Exempel:

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: Returnerar ett `sha1` hash-värde som en hexsträng av `expr`.

Exempel:

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: Returnerar ett `sha1` hash-värde som en hexsträng av `expr`.

Exempel:

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: Returnerar en kontrollsumma av SHA-2-familjen som en hexsträng av `expr`. SHA-224, SHA-256, SHA-384 och SHA-512 stöds. Bitlängden 0 motsvarar 256.

Exempel:

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: Returnerar indexkoden för strängen.

Exempel:

```
> SELECT soundex('Miller');
 M460
```

#### hög

`stack(n, expr1, ..., exprk)`: Separerar `expr1`, ..., `exprk` i `n` rader.

Exempel:

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: Returnerar delsträngen för `str` som börjar vid `pos` och är lång `len`eller segmentet i bytearrayen som börjar vid `pos` och är av längden `len`.

Exempel:

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### delsträng

`substring(str, pos[, len])`: Returnerar delsträngen för `str` som börjar vid `pos` och är lång `len`eller segmentet i bytearrayen som börjar vid `pos` och är av längden `len`.

Exempel:

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`: Returnerar en JSON-sträng med ett givet strukturvärde.

Exempel:

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Sedan: 2.2.0

#### translate

`translate(input, from, to)`: Översätter `input` strängen genom att ersätta tecknen i `from` strängen med motsvarande tecken i `to` strängen.

Exempel:

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trimma

`trim(str)`: Tar bort inledande och avslutande blankstegstecken från `str`.

`trim(BOTH trimStr FROM str)`: Ta bort inledande och avslutande `trimStr` tecken från `str`.

`trim(LEADING trimStr FROM str)`: Ta bort de inledande `trimStr` tecknen från `str`.

`trim(TRAILING trimStr FROM str)`: Ta bort efterföljande `trimStr` tecken från `str`.

Argument:
- `str`: Ett stränguttryck
- `trimStr`: Trimma strängtecken som ska trimmas. Standardvärdet är ett blanksteg
- `BOTH`, `FROM`: Det här är nyckelord som anger trimningssträngtecken från strängens båda ändar
- `LEADING`, `FROM`: Det här är nyckelord för att ange trimningssträngtecken från den vänstra änden av strängen
- `TRAILING`, `FROM`: Det här är nyckelord för att ange trimningssträngtecken från den högra änden av strängen

Exempel:

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### ucase

`ucase(str)`: Returneras `str` med alla tecken ändrade till versaler.

Exempel:

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: Konverterar argumentet från en base 64-sträng `str` till en binär sträng.

Exempel:

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`: Konverterar hexadecimal `expr` till binär.

Exempel:

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`: Returneras `str` med alla tecken ändrade till versaler.

Exempel:

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`: Returnerar en UUID-sträng (Universal Unique Identifier). Värdet returneras som en kanonisk UUID-sträng med 36 tecken.

Exempel:

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE] Funktionen är icke-deterministisk.

### Utvärdering av data

#### coalesce

`coalesce(expr1, expr2, ...)`: Returnerar det första icke-null-argumentet om det finns. Annars null.

Exempel:

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_list

`collect_list(expr)`: Samlar in och returnerar en lista med icke-unika element.

#### collect_set

`collect_set(expr)`: Samlar in och returnerar en uppsättning unika element.

#### concat

`concat(col1, col2, ..., colN)`: Returnerar sammanfogningen av col1, col2, ..., colN.

Exempel:

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE] Det finns `concat` logik för arrayer sedan 2.4.0.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: Returnerar sammanfogningen av strängarna avgränsade med `sep`.

Exempel:

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### antal

`count(*)`: Returnerar det totala antalet hämtade rader, inklusive rader som innehåller null.

`count(expr[, expr...])`: Returnerar antalet rader för vilka de angivna uttrycken inte är null.

`count(DISTINCT expr[, expr...])`: Returnerar antalet rader för vilka de angivna uttrycken är unika och inte null.

#### crc32

`crc32(expr)`: Returnerar ett cykliskt redundanskontrollvärde för `expr` som en bigint.

Exempel:

```
> SELECT crc32('Spark');
 1557323817
```

#### decode

`decode(bin, charset)`: Avkodar det första argumentet med den andra argumentteckenuppsättningen.

Exempel:

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`: Returnerar den `n`:e inmatningen, t.ex. returnerar `input2` när `n` är 2.

Exempel:

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### koda

`encode(str, charset)`: Kodar det första argumentet med den andra argumentteckenuppsättningen.

Exempel:

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### först

`first(expr[, isIgnoreNull])`: Returnerar det första värdet för `expr` en grupp med rader. Om `isIgnoreNull` är true returneras endast värden som inte är null.

#### first_value

`first_value(expr[, isIgnoreNull])`: Returnerar det första värdet för `expr` en grupp med rader. Om `isIgnoreNull` är true returneras endast värden som inte är null.

#### get_json_object

`get_json_object(json_txt, path)`: Extraherar ett json-objekt från `path`.

Exempel:

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### gruppera

<!-- was blank --->

#### grouping_id

<!-- was blank --->

#### instr

`instr(str, substr)`: Returnerar det (1-baserade) indexvärdet för den första förekomsten av `substr` i `str`.

Exempel:

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: Returnerar en tuppel som funktionen, `get_json_object`men den tar flera namn. Alla indataparametrar och utdatakolumntyper är strängar.

Exempel:

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### lag

`lag(input[, offset[, default]])`: Returnerar värdet för `input` på `offset`den rad som finns före den aktuella raden i fönstret. Standardvärdet för `offset` är 1 och standardvärdet för `default` är null. Om värdet för `input` vid `offset`raden är null returneras null. Om det inte finns någon sådan förskjutningsrad (om förskjutningen till exempel är 1 har den första raden i fönstret ingen föregående rad) och `default` returneras.

#### sista

`last(expr[, isIgnoreNull])`: Returnerar det sista värdet för `expr` en grupp rader. Om `isIgnoreNull` är true returneras endast värden som inte är null.

#### last_value

`last_value(expr[, isIgnoreNull])`: Returnerar det sista värdet för `expr` en grupp rader. Om `isIgnoreNull` är true returneras endast värden som inte är null.

#### lead

`lead(input[, offset[, default]])`: Returnerar värdet för `input` på `offset`raden efter den aktuella raden i fönstret. Standardvärdet för `offset` är 1 och standardvärdet för `default` är null. Om värdet för `input` vid `offset`raden är null returneras null. Om det inte finns någon sådan förskjutningsrad (t.ex. om förskjutningen är 1, har den sista raden i fönstret ingen efterföljande rad) och `default` returneras.


#### vänster

`left(str, len)`: Returnerar tecknen längst till vänster `len` (`len` kan vara strängtyp) från strängen `str`. Om `len` är mindre än eller lika med 0 är resultatet en tom sträng.

Exempel:

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: Returnerar teckenlängden för strängdata eller antalet byte för binära data. Längden på strängdata inkluderar efterföljande blanksteg. Längden på binära data inkluderar binära nollor.

Exempel:

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### leta

`locate(substr, str[, pos])`: Returnerar positionen för den första förekomsten av `substr` i `str` efter position `pos`. Angivet `pos` och returvärdet är 1-baserade.

Exempel:

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`: Returnerar unionen för alla angivna kartor.

Exempel:

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Sedan: 2.4.0

#### map_keys

`map_keys(map)`: Returnerar en osorterad array som innehåller kartans nycklar.

Exempel:

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: Returnerar en osorterad array som innehåller mappningens värden.

Exempel:

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`: Delar upp raderna för varje fönsterpartition i `n` intervall från 1 till högst `n`.

#### null om

`nullif(expr1, expr2)`: Returnerar null om `expr1` är lika med `expr2`, eller `expr1` inte.

Exempel:

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: Returnerar `expr2` om `expr1` är null eller `expr1` inte.

Exempel:

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: Returnerar `expr2` om `expr1` inte är null eller `expr3` inte.

Exempel:

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`: Extraherar en del från en URL.

Exempel:

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`: Returnerar positionen för den första förekomsten av `substr` i `str` efter position `pos`. Angivet `pos` och returvärdet är 1-baserade.

Exempel:

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### rankning

`rank()`: Beräknar rangordningen för ett värde i en grupp med värden. Resultatet är ett plus antalet rader som är före eller lika med den aktuella raden i partitionsordningen. Värdena skapar luckor i sekvensen.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: Extraherar en grupp som matchar `regexp`.

Exempel:

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: Ersätter alla delsträngar i `str` som matchar `regexp` med `rep`.

Exempel:

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### upprepa

`repeat(str, n)`: Returnerar strängen som upprepar det angivna strängvärdet n gånger.

Exempel:

```
> SELECT repeat('123', 2);
 123123
```

#### ersätt

`replace(str, search[, replace])`: Ersätter alla förekomster av `search` med `replace`.

Argument:
- `str`: Ett stränguttryck
- `search`: Ett stränguttryck. Om `search` inte hittas i `str`returneras `str` oförändrat.
- `replace`: Ett stränguttryck. Om `replace` inte anges eller är en tom sträng ersätter ingenting den sträng som tas bort från `str`.

Exempel:

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### sammanslagning

<!-- was blank -->

#### radnummer

`row_number()`: Tilldelar varje rad ett unikt sekventiellt nummer, med början på en rad, enligt ordningen för rader i fönsterpartitionen.

#### schema_of_json

`schema_of_json(json[, options])`: Returnerar schema i DDL-format för JSON-sträng.

Exempel:

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Sedan: 2.4.0

#### meningar

`sentences(str[, lang, country])`: Delar `str` i en array med ord.

Exempel:

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### sekvens

`sequence(start, stop, step)`: Genererar en array med element från början till slut (inklusive), med stegvis ökning. Typen för de returnerade elementen är densamma som typen för argumentuttryck.

Typer som stöds är: byte, short, integer, long, date, timestamp.

Uttrycken `start` och `stop` måste kunna evalueras till samma typ. Om `start` och `stop` uttryck matchar typen &#39;date&#39; eller &#39;timestamp&#39; måste `step` uttrycket kunna evalueras till typen &#39;interval&#39;. I annat fall tolkas det till samma typ som `start` och `stop` uttryck.

Argument:
- `start`: Ett uttryck. Intervallets början.
- `stop`: Ett uttryck. Slutet av intervallet (inklusive).
- `step`: Ett valfritt uttryck. Intervallets steg. Som standard `step` är 1 om `start` är mindre än eller lika med `stop`, i annat fall -1. För de tidsmässiga sekvenserna är det 1 dag respektive -1 dag. Om `start` är större än `stop`måste `step` värdet vara negativt och vice versa.

Exempel:

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Sedan: 2.4.0

#### shiftleft

`shiftleft(base, expr)`: Bitvis vänsterskift.

Exempel:

```
> SELECT shiftleft(2, 1);
 4
```

#### shiftright

`shiftright(base, expr)`: Bitvis (signerad) högerskift.

Exempel:

```
> SELECT shiftright(4, 1);
 2
```

#### shiftRightTunsigned

`shiftrightunsigned(base, expr)`: Bitvis osignerad högerskift.

Exempel:

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### size

`size(expr)`: Returnerar storleken på en array eller karta. Funktionen returnerar -1 om dess indata är null och `spark.sql.legacy.sizeOfNull` är inställd på true. Om värdet `spark.sql.legacy.sizeOfNull` är false returneras null för null-indata. Som standard är parametern `spark.sql.legacy.sizeOfNull` inställd på true.

Exempel:

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### space

`space(n)`: Returnerar en sträng som består av `n` blanksteg.

Exempel:

```
> SELECT concat(space(2), '1');
   1
```

#### dela

`split(str, regex)`: Delar `str` runt förekomster som matchar `regex`.

Exempel:

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`: Returnerar delsträngen från `str` före `count` förekomster av avgränsaren `delim`. Om `count` är positivt returneras allt till vänster om den sista avgränsaren (från vänster). Om `count` är negativt returneras allt till höger om den sista avgränsaren (från höger). Funktionen `substring_index` utför en skiftlägeskänslig matchning vid sökning efter `delim`.

Exempel:

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### window

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: Returnerar en strängmatris med värden i noderna i xml som matchar XPath-uttrycket.

Exempel:

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_double

`xpath_double(xml, xpath)`: Returnerar ett dubbelvärde, värdet noll om ingen matchning hittas eller NaN om en matchning hittas men värdet är icke-numeriskt.

Exempel:

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: Returnerar ett flyttal, värdet noll om ingen matchning hittas eller NaN om en matchning hittas men värdet är icke-numeriskt.

Exempel:

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: Returnerar ett heltalsvärde, eller värdet noll om ingen matchning hittas, eller om en matchning hittas men värdet är icke-numeriskt.

Exempel:

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: Returnerar ett långt heltalsvärde, eller värdet noll om ingen matchning hittas, eller om en matchning hittas men värdet är icke-numeriskt.

Exempel:

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: Returnerar ett dubbelvärde, värdet noll om ingen matchning hittas eller NaN om en matchning hittas men värdet är icke-numeriskt.

Exempel:

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: Returnerar ett kort heltalsvärde, eller värdet noll om ingen matchning hittas, eller om en matchning hittas men värdet är icke-numeriskt.

Exempel:

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: Returnerar textinnehållet i den första xml-noden som matchar XPath-uttrycket.

Exempel:

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Aktuell information

#### current_database

`current_database()`: Returnerar den aktuella databasen.

Exempel:

```
> SELECT current_database();
 default
```

#### aktuellt_datum

`current_date()`: Returnerar aktuellt datum vid början av frågeutvärderingen.

Sedan: 1.5.0

#### current_timestamp

`current_timestamp()`: Returnerar den aktuella tidsstämpeln i början av frågeutvärderingen.

Sedan: 1.5.0

#### nu

`now()`: Returnerar den aktuella tidsstämpeln i början av frågeutvärderingen.

Sedan: 1.5.0
