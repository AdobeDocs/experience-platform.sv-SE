---
keywords: Experience Platform;hem;populära ämnen;mappa csv;mappa csv-fil;mappa csv-fil till xdm;mappa csv till xdm;ui guide;mappa;mappa;mappningsfält;mappningsfunktioner;
solution: Experience Platform
title: Förinställningsfunktioner för data
topic: overview
description: I det här dokumentet introduceras de mappningsfunktioner som används med Data Prep.
translation-type: tm+mt
source-git-commit: bfcb1924e40b67c0af41dc789b5ff0bf8e8366e1
workflow-type: tm+mt
source-wordcount: '3597'
ht-degree: 2%

---


# Förinställningsfunktioner för data

Dataprep-funktioner kan användas för att beräkna och beräkna värden baserat på vad som anges i källfält.

## Fält

Ett fältnamn kan vara vilken giltig identifierare som helst - en sekvens med obegränsad längd av Unicode-bokstäver och siffror, med början med en bokstav, dollartecknet (`$`) eller understrecket (`_`). Variabelnamn är också skiftlägeskänsliga.

Om ett fältnamn inte följer den här regeln måste fältnamnet omslutas med `${}`. Om fältnamnet till exempel är &quot;Förnamn&quot; eller &quot;Förnamn&quot; måste namnet omslutas till `${First Name}` eller `${First.Name}`.

Dessutom är fältnamn **alla** av följande reserverade nyckelord. De måste omslutas med `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Du kan komma åt data i underfält genom att använda punktnotation. Om det till exempel finns ett `name`-objekt använder du `name.firstName` för att komma åt fältet `firstName`.

## Lista över funktioner

I följande tabeller visas alla mappningsfunktioner som stöds, inklusive exempeluttryck och deras resulterande utdata.

### Strängfunktioner

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Sammanfogar de angivna strängarna. | <ul><li>STRING: Strängarna som ska sammanfogas.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explodera | Delar strängen baserat på en regex och returnerar en array med delar. Kan även inkludera regex för att dela upp strängen. Som standard tolkas delningen som &quot;,&quot;. Följande avgränsare **måste** föregås av `\`: `+, ?, ^, |, ., [, (, {, ), *, $, \` | <ul><li>STRING: **Obligatorisk** Strängen som måste delas.</li><li>REGEX: *Valfritt* Det reguljära uttryck som kan användas för att dela strängen.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hej, där!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Returnerar platsen/indexvärdet för en delsträng. | <ul><li>INMATNING: **Obligatorisk** Strängen som söks igenom.</li><li>SUBSTRING: **Obligatorisk** Den delsträng som söks efter i strängen.</li><li>START_POSITION: *Valfritt* Platsen där sökningen ska börja i strängen.</li><li>FÖREKOMST: *Valfritt* Den n förekomsten att söka efter från startpositionen. Som standard är det 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe`<span>`.com&quot;, &quot;com&quot;) | 6 |
| replacester | Ersätter söksträngen om den finns i den ursprungliga strängen. | <ul><li>INMATNING: **Obligatorisk** Indatasträngen.</li><li>TO_FIND: **Obligatorisk** Strängen som ska slås upp i indata.</li><li>TO_REPLACE: **Obligatoriskt** Strängen som ska ersätta värdet i TO_FIND.</li></ul> | replacester(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;This is a string replace test&quot; |
| substr | Returnerar en delsträng med en viss längd. | <ul><li>INMATNING: **Obligatorisk** Indatasträngen.</li><li>START_INDEX: **Obligatoriskt** indexvärdet för den indatasträng där delsträngen börjar.</li><li>LÄNGD: **Obligatoriskt** Längden på delsträngen.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>case | Konverterar en sträng till gemener. | <ul><li>INMATNING: **Obligatorisk** Strängen som ska konverteras till gemener.</li></ul> | lower(INPUT) | lower(&quot;HanLo&quot;)<br>lcase(&quot;HanLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Konverterar en sträng till versaler. | <ul><li>INMATNING: **Obligatorisk** Strängen som ska konverteras till versaler.</li></ul> | upper(INPUT) | upper(&quot;HanLo&quot;)<br>ucase(&quot;HanLo&quot;) | &quot;HELLO&quot; |
| split | Delar en indatasträng på en avgränsare. Följande avgränsare **måste** föregås av `\`: `\`. | <ul><li>INMATNING: **Nödvändig** Den indatasträng som ska delas.</li><li>AVGRÄNSARE: **Obligatorisk** Strängen som används för att dela indata.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Sammanfogar en lista med objekt med hjälp av avgränsaren. | <ul><li>AVGRÄNSARE: **Obligatorisk** Strängen som ska användas för att förena objekten.</li><li>OBJEKT: **Nödvändig** En matris med strängar som ska kopplas.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Placerar den vänstra sidan av en sträng med den andra angivna strängen. | <ul><li>INMATNING: **Nödvändig** Strängen som ska utfyllas. Strängen kan vara null.</li><li>ANTAL: **Nödvändig** Storleken på strängen som ska skrivas ut.</li><li>PADDING: **Obligatorisk** Strängen som indata ska fyllas med. Om värdet är null eller tomt behandlas det som ett enda mellanslag.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | Placerar höger sida av en sträng med den andra angivna strängen. | <ul><li>INMATNING: **Nödvändig** Strängen som ska utfyllas. Strängen kan vara null.</li><li>ANTAL: **Nödvändig** Storleken på strängen som ska skrivas ut.</li><li>PADDING: **Obligatorisk** Strängen som indata ska fyllas med. Om värdet är null eller tomt behandlas det som ett enda mellanslag.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| vänster | Hämtar de första n-tecknen i den angivna strängen. | <ul><li>STRING: **Obligatoriskt** Strängen som du hämtar de första n-tecknen för.</li><li>ANTAL: **Obligatoriskt** De n-tecken som du vill hämta från strängen.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| höger | Hämtar de sista n-tecknen i den angivna strängen. | <ul><li>STRING: **Obligatoriskt** Strängen som du hämtar de sista n-tecknen för.</li><li>ANTAL: **Obligatoriskt** De n-tecken som du vill hämta från strängen.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Tar bort mellanrummet från början av strängen. | <ul><li>STRING: **Obligatoriskt** Strängen som du vill ta bort mellanrummet från.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rensa | Tar bort mellanrummet från strängens slut. | <ul><li>STRING: **Obligatoriskt** Strängen som du vill ta bort mellanrummet från.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trimma | Tar bort mellanrummet från början och slutet av strängen. | <ul><li>STRING: **Obligatoriskt** Strängen som du vill ta bort mellanrummet från.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| är lika med | Jämför två strängar för att bekräfta om de är lika. Den här funktionen är skiftlägeskänslig. | <ul><li>STRING1: **Obligatorisk** Den första strängen som du vill jämföra.</li><li>STRING2: **Obligatorisk** Den andra strängen som du vill jämföra.</li></ul> | STRING1.equals(STRING2) | &quot;string1&quot;.equals(&quot;STRING1) | falskt |
| equalsIgnoreCase | Jämför två strängar för att bekräfta om de är lika. Den här funktionen är **inte** skiftlägeskänslig. | <ul><li>STRING1: **Obligatorisk** Den första strängen som du vill jämföra.</li><li>STRING2: **Obligatorisk** Den andra strängen som du vill jämföra.</li></ul> | STRING1.equalsIgnoreCase(STRING2) | &quot;string1&quot;.equalsIgnoreCase(&quot;STRING1&quot;) | sant |
| extract_regex | Extraherar grupper från indatasträngen baserat på ett reguljärt uttryck. | <ul><li>STRING: **Obligatoriskt** Strängen som du extraherar grupperna från.</li><li>REGEX: **Obligatoriskt** Det reguljära uttryck som du vill att gruppen ska matcha.</li></ul> | extract_regex(STRING, REGEX) | extract_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Kontrollerar om strängen matchar det inmatade reguljära uttrycket. | <ul><li>STRING: **Obligatoriskt** Strängen som du kontrollerar matchar det reguljära uttrycket.</li><li>REGEX: **Obligatoriskt** Det reguljära uttryck som du jämför med.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | sant |

### Hash-funktioner

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Tar en inmatning och skapar ett hash-värde med SHA-1 (Secure Hash Algorithm 1). | <ul><li>INMATNING: **Obligatorisk** Den oformaterade text som ska hash-kodas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;min text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Tar en inmatning och skapar ett hash-värde med hjälp av den säkra hash-algoritmen 256 (SHA-256). | <ul><li>INMATNING: **Obligatorisk** Den oformaterade text som ska hash-kodas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;min text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Tar en inmatning och skapar ett hash-värde med hjälp av den säkra hash-algoritmen 512 (SHA-512). | <ul><li>INMATNING: **Obligatorisk** Den oformaterade text som ska hash-kodas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;min text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Tar en inmatning och skapar ett hash-värde med MD5. | <ul><li>INMATNING: **Obligatorisk** Den oformaterade text som ska hash-kodas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;min text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Tar en inmatning använder en algoritm för cyklisk redundanskontroll (CRC) för att skapa en 32-bitars cyklisk kod. | <ul><li>INMATNING: **Obligatorisk** Den oformaterade text som ska hash-kodas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;min text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### URL-funktioner

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | Returnerar protokollet från angiven URL. Om indata är ogiltiga returneras null. | <ul><li>URL: **Nödvändig** Den URL som protokollet måste extraheras från.</li></ul> | get_url_protocol(URL) | get_url_protocol(&quot;https://platform.adobe.com/home&quot;) | https |
| get_url_host | Returnerar värddatorn för angiven URL. Om indata är ogiltiga returneras null. | <ul><li>URL: **Nödvändig** Den URL som värden måste extraheras från.</li></ul> | get_url_host(URL) | get_url_host(&quot;https://platform.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Returnerar porten för angiven URL. Om indata är ogiltiga returneras null. | <ul><li>URL: **Nödvändig** Den URL som porten måste extraheras från.</li></ul> | get_url_port(URL) | get_url_port(&quot;sftp://example.com//home/joe/employee.csv&quot;) | 22 |
| get_url_path | Returnerar sökvägen till angiven URL. Som standard returneras den fullständiga sökvägen. | <ul><li>URL: **Nödvändig** Den URL som sökvägen måste extraheras från.</li><li>FULL_PATH: *Valfritt* Ett booleskt värde som avgör om den fullständiga sökvägen returneras. Om värdet är false returneras bara slutet av sökvägen.</li></ul> | get_url_path(URL, FULL_PATH) | get_url_path(&quot;sftp://example.com//home/joe/employee.csv&quot;) | &quot;//home/joe/employee.csv&quot; |
| get_url_query_str | Returnerar frågesträngen för en angiven URL. | <ul><li>URL: **Nödvändig** Den URL som du försöker hämta frågesträngen från.</li><li>ANKARE: **Obligatoriskt** Anger vad som ska göras med ankaret i frågesträngen. Kan vara ett av tre värden: &quot;keep&quot;, &quot;remove&quot; eller &quot;append&quot;.<br><br>Om värdet är &quot;behåll&quot; kopplas ankarpunkten till det returnerade värdet.<br>Om värdet är &quot;remove&quot; tas ankarpunkten bort från det returnerade värdet.<br>Om värdet är &quot;append&quot; returneras ankarpunkten som ett separat värde.</li></ul> | get_url_query_str(URL, ANCHOR) | get_url_query_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;behåll&quot;)<br>get_url_query_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Datum- och tidsfunktioner

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| nu | Hämtar aktuell tid. |  | nu() | nu() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| tidsstämpel | Hämtar aktuell Unix-tid. |  | tidsstämpel() | tidsstämpel() | 1571850624571 |
| format | Formaterar indatadatum enligt ett angivet format. | <ul><li>DATUM: **Obligatoriskt** Indatadatum, som ett ZonedDateTime-objekt, som du vill formatera.</li><li>FORMAT: **Nödvändigt** Formatet som du vill att datumet ska ändras till.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Konverterar en tidsstämpel till en datumsträng enligt ett angivet format. | <ul><li>TIDSSTÄMPEL: **Obligatorisk** Tidsstämpeln som du vill formatera. Detta skrivs i millisekunder.</li><li>FORMAT: **Nödvändigt** Det format som du vill att tidsstämpeln ska ändras till.</li></ul> | dformat(TIMESTAMP, FORMAT) | format(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-Oct-2019 11:24&quot; |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | <ul><li>DATUM: **Obligatorisk** Strängen som representerar datumet.</li><li>FORMAT: **Obligatorisk** Strängen som representerar datumformatet.</li><li>DEFAULT_DATE: **Obligatoriskt** Standarddatumet som returneras om det angivna datumet är null.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | <ul><li>DATUM: **Obligatorisk** Strängen som representerar datumet.</li><li>FORMAT: **Obligatorisk** Strängen som representerar datumformatet.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | <ul><li>DATUM: **Obligatorisk** Strängen som representerar datumet.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Hämtar datumets delar. Följande komponentvärden stöds: <br><br>&quot;år&quot;<br>&quot;åååå&quot;<br>&quot;yy&quot;<br><br>&quot;kvartal&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;månad&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dag på året&quot;<br>&quot;dag&quot;&lt;a 11/>&quot;y&quot;<br><br>&quot;dag&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;vecka&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;veckodag&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n a28/>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot;<br><br><br> | <ul><li>KOMPONENT: **Obligatorisk** En sträng som representerar datumdelen. </li><li>DATUM: **Obligatoriskt** Datumet i standardformat.</li></ul> | date_part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Ersätter en komponent ett visst datum. Följande komponenter godkänns: <br><br>&quot;år&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;månad&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dag&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;timme&quot;<br>&quot;hh&quot;&lt;a1 1/>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br> | <ul><li>KOMPONENT: **Obligatorisk** En sträng som representerar datumdelen. </li><li>VÄRDE: **Obligatoriskt** Värdet som ska anges för komponenten för ett visst datum.</li><li>DATUM: **Obligatoriskt** Datumet i standardformat.</li></ul> | set_date_part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Skapar ett datum från delar. Den här funktionen kan också induceras med make_timestamp. | <ul><li>ÅR: **Obligatoriskt** År, skrivet med fyra siffror.</li><li>MÅNAD: **Obligatorisk** Månad. Tillåtna värden är 1 till 12.</li><li>DAG: **Obligatorisk** Dag. Tillåtna värden är 1 till 31.</li><li>TIMME: **Nödvändig** Timmen. De tillåtna värdena är 0 till 23.</li><li>MINUT: **Nödvändig** Minut. De tillåtna värdena är 0 till 59.</li><li>NANOSECOND: **Obligatoriskt** nanosekundsvärdena. De tillåtna värdena är 0 till 999999999.</li><li>TIMEZON: **Obligatoriskt** Tidszonen för datum/tid.</li></ul> | make_date_time(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Konverterar ett datum i en tidszon till ett datum i UTC. | <ul><li>DATUM: **Obligatoriskt** Det datum som du försöker konvertera.</li></ul> | zone_date_to_utc(DATE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Konverterar ett datum från en tidszon till en annan tidszon. | <ul><li>DATUM: **Obligatoriskt** Det datum som du försöker konvertera.</li><li>ZON: **Obligatoriskt** Tidszonen som du försöker konvertera datumet till.</li></ul> | zone_date_to_zone(DATE, ZONE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

### Hierarkier - objekt

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Returnerar storleken på indata. | <ul><li>INMATNING: **Obligatoriskt** Det objekt som du försöker hitta storleken på.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Kontrollerar om ett objekt är tomt eller inte. | <ul><li>INMATNING: **Obligatoriskt** Det objekt som du försöker kontrollera är tomt.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | falskt |
| arrayer_to_object | Skapar en lista med objekt. | <ul><li>INMATNING: **Obligatoriskt** En gruppering av nyckel- och matrispar.</li></ul> | arrayer_to_object(INPUT) | need sample | need sample |
| to_object | Skapar ett objekt baserat på de platta nyckel-/värdepar som anges. | <ul><li>INMATNING: **Obligatoriskt** En platt lista med nyckel/värde-par.</li></ul> | to_object(INPUT) | to_object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Skapar ett objekt från indatasträngen. | <ul><li>STRING: **Obligatorisk** Strängen som tolkas för att skapa ett objekt.</li><li>VALUE_DELIMITER: *Valfritt* Avgränsaren som skiljer ett fält från värdet. Standardavgränsaren är `:`.</li><li>FIELD_DELIMITER: *Valfritt* Avgränsaren som avgränsar fältvärdepar. Standardavgränsaren är `,`.</li></ul> | str_to_object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | telefon - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Kontrollerar om objektet finns i källdata. | <ul><li>INMATNING: **Obligatorisk** Sökvägen som ska kontrolleras om den finns i källdata.</li></ul> | is_set(INPUT) | is_set(&quot;evar.evar.field1&quot;) | sant |
| null | Anger värdet för attributet till `null`. Detta bör användas när du inte vill kopiera fältet till målschemat. |  | nullify() | nullify() | `null` |

### Hierarkier - matriser

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| coalesce | Returnerar det första icke-null-objektet i en given array. | <ul><li>INMATNING: **Obligatoriskt** Den array som du vill hitta det första icke-null-objektet för.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| först | Hämtar det första elementet i den angivna arrayen. | <ul><li>INMATNING: **Nödvändig** Arrayen som du vill hitta det första elementet i.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| sista | Hämtar det sista elementet i den angivna arrayen. | <ul><li>INMATNING: **Nödvändig** Arrayen som du vill hitta det sista elementet i.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Tar en lista med indata och konverterar den till en array. | <ul><li>INCLUDE_NULLS: **Obligatoriskt** Ett booleskt värde som anger om null-värden ska tas med i svarsarrayen eller inte.</li><li>VÄRDEN: **Obligatoriskt** De element som ska konverteras till en array.</li></ul> | to_array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Logiska operatorer

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decode | Om en nyckel och en lista med nyckelvärdepar förenklas som en array, returnerar funktionen värdet om nyckeln hittas eller returnerar ett standardvärde om det finns i arrayen. | <ul><li>NYCKEL: **Nödvändig** Nyckeln som ska matchas.</li><li>OPTIONS: **Nödvändig** En förenklad array med nyckel/värde-par. Ett standardvärde kan också placeras i slutet.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Om given stateCode är &quot;ca&quot;, &quot;California&quot;.<br>Om den angivna statskoden är &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Om stateCode inte matchar följande, &quot;N/A&quot;. |
| iif | Utvärderar ett givet booleskt uttryck och returnerar det angivna värdet baserat på resultatet. | <ul><li>BOOLEAN_EXPRESSION: **Obligatoriskt** Det booleska uttryck som utvärderas.</li><li>TRUE_VALUE: **Obligatoriskt** Värdet som returneras om uttrycket utvärderas till true.</li><li>FALSE_VALUE: **Obligatoriskt** Värdet som returneras om uttrycket utvärderas till false.</li></ul> | iif(BOOLEAN_EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Sant&quot; |

### Aggregera

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Returnerar det minsta av de angivna argumenten. Använder naturlig beställning. | <ul><li>OPTIONS: **Obligatoriskt** Ett eller flera objekt som kan jämföras med varandra.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Returnerar det maximala antalet angivna argument. Använder naturlig beställning. | <ul><li>OPTIONS: **Obligatoriskt** Ett eller flera objekt som kan jämföras med varandra.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Typkonverteringar

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Konverterar en sträng till ett BigInteger. | <ul><li>STRING: **Obligatorisk** Strängen som ska konverteras till ett BigInteger.</li></ul> | to_bigint(STRING) | to_bigint(&quot;100000.34&quot;) | 1000000,34 |
| to_decimal | Konverterar en sträng till en dubbel sträng. | <ul><li>STRING: **Obligatorisk** Strängen som ska konverteras till Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | Konverterar en sträng till en flyttal. | <ul><li>STRING: **Obligatorisk** Strängen som ska konverteras till ett flyttal.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | Konverterar en sträng till ett heltal. | <ul><li>STRING: **Obligatorisk** Strängen som ska konverteras till ett heltal.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### JSON-funktioner

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Deserialisera JSON-innehåll från den angivna strängen. | <ul><li>STRING: **Nödvändig** JSON-strängen som ska avserialiseras.</li></ul> | json_to_object(STRING) | json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}) | Ett objekt som representerar JSON. |

### Särskilda åtgärder

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Skapar ett pseudoslumpmässigt ID. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |

### Användaragentfunktioner

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

|  -funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Extraherar operativsystemets namn från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_os_name(USER_AGENT) | ua_os_name(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extraherar operativsystemets huvudversion från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_os_version_major(USER_AGENT) | ua_os_version_major(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extraherar operativsystemets version från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_os_version(USER_AGENT) | ua_os_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extraherar operativsystemets namn och version från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_os_name_version(USER_AGENT) | ua_os_name_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extraherar agentversionen från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_agent_version(USER_AGENT) | ua_agent_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extraherar agentnamnet och huvudversionen från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_agent_version_major(USER_AGENT) | ua_agent_version_major(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extraherar agentnamnet från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_agent_name(USER_AGENT) | ua_agent_name(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extraherar enhetsklassen från användaragentsträngen. | <ul><li>USER_AGENT: **Nödvändig** Användaragentsträngen.</li></ul> | ua_device_class(USER_AGENT) | ua_device_class(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 som Mac OS X) AppleWebKit/534.46 (KHTML, t.ex. Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefon |