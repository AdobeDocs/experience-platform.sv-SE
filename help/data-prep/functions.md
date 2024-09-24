---
keywords: Experience Platform;hem;populära ämnen;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mappning;mappningsfält;mappningsfunktioner;
solution: Experience Platform
title: Mappningsfunktioner för dataförinställningar
description: I det här dokumentet introduceras de mappningsfunktioner som används med Data Prep.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 1e06fa2f8a5685cf5debcc3b5279d7efab9af0c8
workflow-type: tm+mt
source-wordcount: '6024'
ht-degree: 0%

---

# Funktioner för datapersonmappning

Dataprep-funktioner kan användas för att beräkna och beräkna värden baserat på vad som anges i källfält.

## Fält

Ett fältnamn kan vara vilken giltig identifierare som helst - en sekvens med obegränsad längd av Unicode-bokstäver och siffror som börjar med en bokstav, dollartecknet (`$`) eller understrecket (`_`). Variabelnamn är också skiftlägeskänsliga.

Om ett fältnamn inte följer den här regeln måste fältnamnet kapslas in med `${}`. Om fältnamnet till exempel är &quot;Förnamn&quot; eller &quot;Förnamn&quot; måste namnet radbrytas som `${First Name}` respektive `${First\.Name}`.

>[!TIP]
>
>Om ett underordnat attribut har en punkt (`.`) vid interaktion med hierarkier måste du använda ett omvänt snedstreck (`\`) för att undvika specialtecken. Mer information finns i handboken om [att kringgå specialtecken](home.md#escape-special-characters).

Om ett fältnamn är **något** av följande reserverade nyckelord måste det kapslas med `${}{}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

Dessutom innehåller reserverade nyckelord alla mappningsfunktioner som listas på den här sidan.

Du kan komma åt data i underfält genom att använda punktnotation. Om det till exempel finns ett `name`-objekt använder du `name.firstName` för att komma åt fältet `firstName`.

## Lista över funktioner

I följande tabeller visas alla mappningsfunktioner som stöds, inklusive exempeluttryck och deras resulterande utdata.

### Strängfunktioner {#string}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Sammanfogar de angivna strängarna. | <ul><li>STRING: Strängarna som ska sammanfogas.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explodera | Delar strängen baserat på en regex och returnerar en array med delar. Kan även inkludera regex för att dela upp strängen. Som standard tolkas delningen som &quot;,&quot;. Följande avgränsare **måste** föregås av `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Om du inkluderar flera tecken som avgränsare behandlas avgränsaren som en avgränsare med flera tecken. | <ul><li>STRING: **Required** Strängen som måste delas.</li><li>REGEX: *Valfritt* Det reguljära uttryck som kan användas för att dela strängen.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hej, där!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Returnerar platsen/indexvärdet för en delsträng. | <ul><li>INPUT: **Required** Strängen som söks igenom.</li><li>SUBSTRING: **Required** Den delsträng som söks efter i strängen.</li><li>START_POSITION: *Valfritt* Platsen där sökningen ska börja i strängen.</li><li>FÖREKOMST: *Valfritt* Den n förekomsten att söka efter från startpositionen. Som standard är det 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacester | Ersätter söksträngen om den finns i den ursprungliga strängen. | <ul><li>INPUT: **Required** Indatasträngen.</li><li>TO_FIND: **Required** Strängen som ska slås upp i indata.</li><li>TO_REPLACE: **Required** Strängen som ska ersätta värdet i TO_FIND.</li></ul> | replacester(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;This is a string replace test&quot; |
| substr | Returnerar en delsträng med en viss längd. | <ul><li>INPUT: **Required** Indatasträngen.</li><li>START_INDEX: **Required** Indexvärdet för den indatasträng där delsträngen börjar.</li><li>LENGTH: **Required** Längden på delsträngen.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Konverterar en sträng till gemener. | <ul><li>INPUT: **Required** Strängen som ska konverteras till gemener.</li></ul> | lower(INPUT) | lower(&quot;HanLo&quot;)<br>lcase(&quot;HanLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Konverterar en sträng till versaler. | <ul><li>INPUT: **Required** Strängen som ska konverteras till versaler.</li></ul> | upper(INPUT) | upper(&quot;HanLo&quot;)<br>ucase(&quot;HanLo&quot;) | &quot;HELLO&quot; |
| dela | Delar en indatasträng på en avgränsare. Följande avgränsare **måste** föregås av `\`: `\`. Om du inkluderar flera avgränsare delas strängen upp på **valfri** av avgränsarna som finns i strängen. **Obs!** Den här funktionen returnerar bara index som inte är null från strängen, oavsett om avgränsaren finns. Om alla index, inklusive null, krävs i den resulterande arrayen använder du funktionen &quot;explode&quot; i stället. | <ul><li>INPUT: **Required** Den indatasträng som ska delas.</li><li>SEPARATOR: **Required** Strängen som används för att dela indata.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Sammanfogar en lista med objekt med hjälp av avgränsaren. | <ul><li>SEPARATOR: **Required** Strängen som ska användas för att förena objekten.</li><li>OBJEKT: **Obligatoriskt** En matris med strängar som ska kopplas.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Placerar den vänstra sidan av en sträng med den andra angivna strängen. | <ul><li>INPUT: **Required** Strängen som ska utfyllas. Strängen kan vara null.</li><li>ANTAL: **Obligatoriskt** Strängstorleken som ska utfyllas.</li><li>PADDING: **Required** Strängen som indata ska fyllas med. Om värdet är null eller tomt behandlas det som ett enda mellanslag.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | Placerar höger sida av en sträng med den andra angivna strängen. | <ul><li>INPUT: **Required** Strängen som ska utfyllas. Strängen kan vara null.</li><li>ANTAL: **Obligatoriskt** Strängstorleken som ska utfyllas.</li><li>PADDING: **Required** Strängen som indata ska fyllas med. Om värdet är null eller tomt behandlas det som ett enda mellanslag.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| vänster | Hämtar de första n-tecknen i den angivna strängen. | <ul><li>STRING: **Required** Strängen som du hämtar de första n-tecknen för.</li><li>ANTAL: **Obligatoriskt** De n-tecken som du vill hämta från strängen.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| höger | Hämtar de sista n-tecknen i den angivna strängen. | <ul><li>STRING: **Required** Strängen du hämtar de sista n-tecknen för.</li><li>ANTAL: **Obligatoriskt** De n-tecken som du vill hämta från strängen.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Tar bort mellanrummet från början av strängen. | <ul><li>STRING: **Required** Strängen som du vill ta bort mellanrummet från.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Tar bort mellanrummet från strängens slut. | <ul><li>STRING: **Required** Strängen som du vill ta bort mellanrummet från.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Tar bort mellanrummet från början och slutet av strängen. | <ul><li>STRING: **Required** Strängen som du vill ta bort mellanrummet från.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| är lika med | Jämför två strängar för att bekräfta om de är lika. Den här funktionen är skiftlägeskänslig. | <ul><li>STRING1: **Required** Den första strängen som du vill jämföra.</li><li>STRING2: **Required** Den andra strängen som du vill jämföra.</li></ul> | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Jämför två strängar för att bekräfta om de är lika. Den här funktionen är **inte** skiftlägeskänslig. | <ul><li>STRING1: **Required** Den första strängen som du vill jämföra.</li><li>STRING2: **Required** Den andra strängen som du vill jämföra.</li></ul> | STRING1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### Funktioner för reguljära uttryck

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extraherar grupper från indatasträngen baserat på ett reguljärt uttryck. | <ul><li>STRING: **Required** Strängen som du extraherar grupperna från.</li><li>REGEX: **Obligatoriskt** Det reguljära uttryck som du vill att gruppen ska matcha.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Kontrollerar om strängen matchar det inmatade reguljära uttrycket. | <ul><li>STRING: **Required** Strängen som du kontrollerar matchar det reguljära uttrycket.</li><li>REGEX: **Obligatoriskt** Det reguljära uttryck som du jämför med.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style="table-layout:auto"}

### Hash-funktioner {#hashing}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Tar en inmatning och skapar ett hash-värde med SHA-1 (Secure Hash Algorithm 1). | <ul><li>INMATNING: **Krävs** Den oformaterade text som ska hashas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;min text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Tar en inmatning och skapar ett hash-värde med Secure Hash Algorithm 256 (SHA-256). | <ul><li>INMATNING: **Krävs** Den oformaterade text som ska hashas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;min text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Tar en inmatning och skapar ett hash-värde med hjälp av den säkra hash-algoritmen 512 (SHA-512). | <ul><li>INMATNING: **Krävs** Den oformaterade text som ska hashas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;min text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Tar en inmatning och skapar ett hash-värde med MD5. | <ul><li>INMATNING: **Krävs** Den oformaterade text som ska hashas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;min text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Tar en inmatning använder en algoritm för cyklisk redundanskontroll (CRC) för att skapa en 32-bitars cyklisk kod. | <ul><li>INMATNING: **Krävs** Den oformaterade text som ska hashas.</li><li>CHARSET: *Valfritt* Namnet på teckenuppsättningen. Möjliga värden är UTF-8, UTF-16, ISO-8859-1 och US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;min text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### URL-funktioner {#url}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Returnerar protokollet från angiven URL. Om indata är ogiltiga returneras null. | <ul><li>URL: **Obligatoriskt** Den URL som protokollet måste extraheras från.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Returnerar värddatorn för angiven URL. Om indata är ogiltiga returneras null. | <ul><li>URL: **Obligatoriskt** Den URL som värden måste extraheras från.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Returnerar porten för angiven URL. Om indata är ogiltiga returneras null. | <ul><li>URL: **Obligatoriskt** Den URL som porten måste extraheras från.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Returnerar sökvägen till angiven URL. Som standard returneras den fullständiga sökvägen. | <ul><li>URL: **Obligatoriskt** URL:en som sökvägen måste extraheras från.</li><li>FULL_PATH: *Valfritt* Ett booleskt värde som avgör om den fullständiga sökvägen returneras. Om värdet är false returneras bara slutet av sökvägen.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | Returnerar frågesträngen för en angiven URL som en mappning av frågesträngsnamnet och frågesträngsvärdet. | <ul><li>URL: **Obligatoriskt** Den URL som du försöker hämta frågesträngen från.</li><li>ANCHOR: **Required** Avgör vad som ska göras med ankaret i frågesträngen. Kan vara ett av tre värden: &quot;keep&quot;, &quot;remove&quot; eller &quot;append&quot;.<br><br>Om värdet är &quot;behåll&quot; kopplas ankarpunkten till det returnerade värdet.<br>Om värdet är &quot;remove&quot; tas ankarpunkten bort från det returnerade värdet.<br>Om värdet är &quot;append&quot; returneras ankarpunkten som ett separat värde.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/here?name= &#x200B; ferret#nos&quot;, &quot;keep&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/here?name= &#x200B; ferret#nos&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.comågor:8042/over/where?name=illret#nos&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Den här funktionen tar en URL som indata och ersätter eller kodar specialtecknen med ASCII-tecken. Mer information om specialtecken finns i [listan över specialtecken](#special-characters) i bilagan till det här dokumentet. | <ul><li>URL: **Obligatoriskt** Indata-URL:en med specialtecken som du vill ersätta eller koda med ASCII-tecken.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | Den här funktionen tar en URL som indata och avkodar ASCII-tecken till specialtecken.  Mer information om specialtecken finns i [listan över specialtecken](#special-characters) i bilagan till det här dokumentet. | <ul><li>URL: **Obligatoriskt** Indata-URL:en med ASCII-tecken som du vill avkoda till specialtecken.</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | /example.com/partneralliance_asia-pacific_2022</span> |

{style="table-layout:auto"}

### Datum- och tidsfunktioner {#date-and-time}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen. Mer information om funktionen `date` finns i datumavsnittet i [hanteringsguiden för dataformat](./data-handling.md#dates).

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Hämtar aktuell tid. | | now() | now() | `2021-10-26T10:10:24Z` |
| tidsstämpel | Hämtar aktuell Unix-tid. | | timestamp() | timestamp() | 1571850624571 |
| format | Formaterar indatadatum enligt ett angivet format. | <ul><li>DATE: **Required** Indatadatum, som ett ZonedDateTime-objekt, som du vill formatera.</li><li>FORMAT: **Obligatoriskt** Formatet som du vill ändra datumet till.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | Konverterar en tidsstämpel till en datumsträng enligt ett angivet format. | <ul><li>TIDSSTÄMPEL: **Krävs** Tidsstämpeln som du vill formatera. Detta skrivs i millisekunder.</li><li>FORMAT: **Obligatoriskt** Det format som du vill att tidsstämpeln ska bli.</li></ul> | dformat(TIMESTAMP, FORMAT) | format(1571829875000, &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | <ul><li>DATE: **Required** Strängen som representerar datumet.</li><li>FORMAT: **Obligatoriskt** Strängen som representerar formatet för källdatumet.**Obs!** Detta representerar **inte** formatet som du vill konvertera datumsträngen till. </li><li>DEFAULT_DATE: **Required** Standarddatumet returnerades om det angivna datumet är null.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | <ul><li>DATE: **Required** Strängen som representerar datumet.</li><li>FORMAT: **Obligatoriskt** Strängen som representerar formatet för källdatumet.**Obs!** Detta representerar **inte** formatet som du vill konvertera datumsträngen till. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| datum | Konverterar en datumsträng till ett ZonedDateTime-objekt (ISO 8601-format). | <ul><li>DATE: **Required** Strängen som representerar datumet.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Hämtar datumets delar. Följande komponentvärden stöds: <br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarters&quot; <br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day of year&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;{1 <br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;vecka&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;veckodag&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot; <br>&quot;hh24&quot;<br> &quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;SSS&quot; | <ul><li>KOMPONENT: **Obligatorisk** En sträng som representerar datumdelen. </li><li>DATUM: **Obligatoriskt** Datumet i standardformat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Ersätter en komponent vid ett visst datum. Följande komponenter accepteras: <br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br> &quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>KOMPONENT: **Obligatorisk** En sträng som representerar datumdelen. </li><li>VÄRDE: **Obligatoriskt** Värdet som ska anges för komponenten för ett visst datum.</li><li>DATUM: **Obligatoriskt** Datumet i standardformat.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Skapar ett datum från delar. Den här funktionen kan också induceras med make_timestamp. | <ul><li>ÅR: **Obligatoriskt** Året, skrivet med fyra siffror.</li><li>MÅNAD: **Krävs** Månad. Tillåtna värden är 1 till 12.</li><li>DAG: **Krävs** Dagen. Tillåtna värden är 1 till 31.</li><li>TIMME: **Krävs** Timmen. De tillåtna värdena är 0 till 23.</li><li>MINUT: **Krävs** minuten. De tillåtna värdena är 0 till 59.</li><li>NANOSECOND: **Required** The nanosecond values. De tillåtna värdena är 0 till 999999999.</li><li>TIMEZONE: **Required** Tidszonen för datumet och tiden.</li></ul> | make_date_time &#x200B;(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Konverterar ett datum i en tidszon till ett datum i UTC. | <ul><li>DATUM: **Obligatoriskt** Det datum som du försöker konvertera.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Konverterar ett datum från en tidszon till en annan tidszon. | <ul><li>DATUM: **Obligatoriskt** Det datum som du försöker konvertera.</li><li>ZON: **Obligatoriskt** Tidszonen som du försöker konvertera datumet till.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Hierarkier - objekt {#objects}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Kontrollerar om ett objekt är tomt eller inte. | <ul><li>INMATNING: **Nödvändigt** Objektet som du försöker kontrollera är tomt.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrayer_to_object | Skapar en lista med objekt. | <ul><li>INMATNING: **Obligatoriskt** En gruppering av nyckel- och matrispar.</li></ul> | arrayer_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Skapar ett objekt baserat på de platta nyckel-/värdepar som anges. | <ul><li>INMATNING: **Krävs** En platt lista över nyckel-/värdepar.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Skapar ett objekt från indatasträngen. | <ul><li>STRING: **Required** Strängen som tolkas för att skapa ett objekt.</li><li>VALUE_DELIMITER: *Valfritt* Avgränsaren som skiljer ett fält från värdet. Standardavgränsaren är `:`.</li><li>FIELD_DELIMITER: *Valfritt* Avgränsaren som avgränsar fältvärdepar. Standardavgränsaren är `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Obs!**: Du kan använda funktionen `get()` tillsammans med `str_to_object()` för att hämta värden för nycklarna i strängen. | <ul><li>Exempel 1: str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>Exempel 2: str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>Exempel 1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Exempel 2: &quot;John&quot;</li></ul> |
| contains_key | Kontrollerar om objektet finns i källdata. **Obs!** Den här funktionen ersätter den inaktuella `is_set()`-funktionen. | <ul><li>INMATNING: **Nödvändig** Sökvägen som ska kontrolleras om den finns i källdata.</li></ul> | contains_key(INPUT) | contains_key(&quot;evar.evar.field1&quot;) | true |
| null | Anger värdet för attributet till `null`. Detta bör användas när du inte vill kopiera fältet till målschemat. | | nullify() | nullify() | `null` |
| get_keys | Tolkar nyckel/värde-paren och returnerar alla nycklar. | <ul><li>OBJEKT: **Obligatoriskt** Det objekt som nycklarna ska extraheras från.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Pride and Prekurce&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Tolkar nyckel/värde-paren och returnerar värdet för strängen baserat på den angivna nyckeln. | <ul><li>STRING: **Required** Strängen som du vill tolka.</li><li>KEY: **Required** Nyckeln som värdet ska extraheras för.</li><li>VALUE_DELIMITER: **Required** Avgränsaren som avgränsar fältet och värdet. Om antingen `null` eller en tom sträng anges är det här värdet `:`.</li><li>FIELD_DELIMITER: *Valfritt* Avgränsaren som avgränsar fält- och värdepar. Om antingen `null` eller en tom sträng anges är det här värdet `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John, lastName - Cena, phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | Tar en karta och tangentindata. Om indata är en enskild tangent returnerar funktionen det värde som är associerat med den tangenten. Om indata är en strängarray returnerar funktionen alla värden som motsvarar de angivna nycklarna. Om den inkommande kartan innehåller dubblettnycklar måste returvärdet avduplicera nycklarna och returnera unika värden. | <ul><li>MAP: **Obligatoriskt** Indatamappningsdata.</li><li>KEY: **Required** Nyckeln kan vara en sträng eller en strängmatris. Om någon annan primitiv typ (data/tal) anges behandlas den som en sträng.</li></ul> | get_values(MAP, KEY) | Ett kodexempel finns i [bilagan](#map_get_values). | |
| map_has_keys | Om en eller flera indatanycklar anges returnerar funktionen true. Om en strängarray anges som indata returnerar funktionen true för den första nyckeln som hittas. | <ul><li>MAP: **Obligatoriskt** Indatamappningsdata</li><li>KEY: **Required** Nyckeln kan vara en sträng eller en strängmatris. Om någon annan primitiv typ (data/tal) anges behandlas den som en sträng.</li></ul> | map_has_keys(MAP, KEY) | Ett kodexempel finns i [bilagan](#map_has_keys). | |
| add_to_map | Accepterar minst två indata. Ett valfritt antal kartor kan anges som indata. Data Prep returnerar en enda karta som innehåller alla nyckelvärdepar från alla indata. Om en eller flera nycklar upprepas (på samma karta eller tvärs över kartor) deduplicerar Data Prep nycklarna så att det första nyckel/värde-paret kvarstår i den ordning som de skickades i indata. | MAP: **Obligatoriskt** Indatamappningsdata. | add_to_map(MAP 1, MAP 2, MAP 3, ...) | Ett kodexempel finns i [bilagan](#add_to_map). | |
| object_to_map (Syntax 1) | Använd den här funktionen om du vill skapa datatyperna för kartan. | <ul><li>KEY: **Obligatoriska**-nycklar måste vara en sträng. Om det finns andra primitiva värden, till exempel heltal eller datum, konverteras de automatiskt till strängar och behandlas som strängar.</li><li>ANY_TYPE: **Required** Avser alla XDM-datatyper som stöds, förutom Maps.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, ...) | Ett kodexempel finns i [bilagan](#object_to_map). | |
| object_to_map (Syntax 2) | Använd den här funktionen om du vill skapa datatyperna för kartan. | <ul><li>OBJECT: **Required** Du kan ange en inkommande objekt- eller objektmatris och peka på ett attribut inuti objektet som nyckel.</li></ul> | object_to_map(OBJECT) | Ett kodexempel finns i [bilagan](#object_to_map). |
| object_to_map (Syntax 3) | Använd den här funktionen om du vill skapa datatyperna för kartan. | <ul><li>OBJECT: **Required** Du kan ange en inkommande objekt- eller objektmatris och peka på ett attribut inuti objektet som nyckel.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Ett kodexempel finns i [bilagan](#object_to_map). |

{style="table-layout:auto"}

Mer information om objektkopieringsfunktionen finns i avsnittet [nedan](#object-copy).

### Hierarkier - matriser {#arrays}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Returnerar det första icke-null-objektet i en given array. | <ul><li>INPUT: **Required** Arrayen som du vill hitta det första icke-null-objektet för.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| först | Hämtar det första elementet i den angivna arrayen. | <ul><li>INPUT: **Required** Arrayen som du vill hitta det första elementet i.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| sista | Hämtar det sista elementet i den angivna arrayen. | <ul><li>INPUT: **Required** Arrayen som du vill hitta det sista elementet i.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Lägger till element i slutet av arrayen. | <ul><li>ARRAY: **Required** Arrayen som du lägger till element i.</li><li>VÄRDEN: De element som du vill lägga till i arrayen.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Kombinerar arrayerna med varandra. | <ul><li>ARRAY: **Required** Arrayen som du lägger till element i.</li><li>VÄRDEN: Den eller de matriser som du vill lägga till i den överordnade matrisen.</li></ul> | join_arrays &#x200B;(ARRAY, VALUES) | join_arrays &#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Tar en lista med indata och konverterar den till en array. | <ul><li>INCLUDE_NULLS: **Required** Ett booleskt värde som anger om null-värden ska tas med i svarsarrayen eller inte.</li><li>VÄRDEN: **Obligatoriskt** De element som ska konverteras till en array.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Returnerar storleken på indata. | <ul><li>INPUT: **Obligatoriskt** Det objekt som du försöker hitta storleken på.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Den här funktionen används för att lägga till alla element i hela inmatningsarrayen i slutet av arrayen i profilen. Den här funktionen är **endast** tillämplig under uppdateringar. Om den används i infogningskontexten returneras indata i befintligt skick. | <ul><li>ARRAY: **Required** Arrayen som ska läggas till i arrayen i profilen.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | Den här funktionen används för att ersätta element i en array. Den här funktionen är **endast** tillämplig under uppdateringar. Om den används i infogningskontexten returneras indata i befintligt skick. | <ul><li>ARRAY: **Required** Arrayen som ska ersätta arrayen i profilen.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |
| [!BADGE Beta]{type=Informative} array_to_string | Sammanfogar strängrepresentationerna för elementen i en array med den angivna avgränsaren. Om arrayen är flerdimensionell förenklas den innan den förenas. **Obs!** Den här funktionen används i mål. Mer information finns i [dokumentationen](../destinations/ui/export-arrays-calculated-fields.md). | <ul><li>SEPARATOR: **Required** Avgränsaren som används för att förena elementen i arrayen.</li><li>ARRAY: **Required** Arrayen som ska förenas (efter förenkling).</li></ul> | array_to_string(SEPARATOR, ARRAY) | `array_to_string(";", ["Hello", "world"])` | &quot;Hello;world&quot; |
| [!BADGE Beta]{type=Informative} filterArray* | Filtrerar den angivna arrayen baserat på ett predikat. **Obs!** Den här funktionen används i mål. Mer information finns i [dokumentationen](../destinations/ui/export-arrays-calculated-fields.md). | <ul><li>ARRAY: **Obligatorisk** Matrisen som ska filtreras</li><li>PREDICATE: **Required** Predikatet som ska användas för varje element i den angivna arrayen. | filterArray(ARRAY, PREDICATE) | `filterArray([5, -6, 0, 7], x -> x > 0)` | [5, 7] |
| [!BADGE Beta]{type=Informative} transformArray* | Omformar den angivna arrayen baserat på ett predikat. **Obs!** Den här funktionen används i mål. Mer information finns i [dokumentationen](../destinations/ui/export-arrays-calculated-fields.md). | <ul><li>ARRAY: **Required** Arrayen som ska omformas.</li><li>PREDICATE: **Required** Predikatet som ska användas för varje element i den angivna arrayen. | transformArray(ARRAY, PREDICATE) | ` transformArray([5, 6, 7], x -> x + 1)` | [6, 7, 8] |
| [!BADGE Beta]{type=Informative} flattenArray* | Förenklar den angivna (flerdimensionella) arrayen till en endimensionell array. **Obs!** Den här funktionen används i mål. Mer information finns i [dokumentationen](../destinations/ui/export-arrays-calculated-fields.md). | <ul><li>ARRAY: **Obligatorisk** Matrisen som ska förenklas.</li></ul> | flattenArray(ARRAY) | flattenArray([[&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;, &#39;d&#39;]], [[&#39;e&#39;], [&#39;f&#39;]])) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;, &#39;f&#39;] |

{style="table-layout:auto"}

### Hierarkier - karta {#map}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Den här funktionen tar en objektarray och en nyckel som indata och returnerar en karta över nyckelfältet med värdet key och arrayelementet som value. | <ul><li>INPUT: **Required** Objektarrayen som du vill hitta det första icke-null-objektet för.</li><li>KEY: **Required** Nyckeln måste vara ett fältnamn i objektarrayen och objektet som värde.</li></ul> | array_to_map(OBJECT[] INPUTS, KEY) | I [bilagan](#object_to_map) finns ett kodexempel. |
| object_to_map | Den här funktionen tar ett objekt som argument och returnerar en karta över nyckelvärdepar. | <ul><li>INPUT: **Required** Objektarrayen som du vill hitta det första icke-null-objektet för.</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address) där input är &quot; + &quot;address: {line1 : \&quot;345 park ave\&quot;,line2: \&quot;bldg 2\&quot;,City : \&quot;san jose\&quot;,State : \&quot;CA\&quot;,type: \&quot;office\&quot;}&quot; | Returnerar en karta med angivet fältnamn och värde-par eller null om indata är null. Till exempel: `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Den här funktionen tar en lista över par med nyckelvärden och returnerar en karta med par med nyckelvärden. | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;, \&quot;John\&quot;, \&quot;lastName\&quot;, \&quot;Doe\&quot;)&quot; | Returnerar en karta med angivet fältnamn och värde-par eller null om indata är null. Till exempel: `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Logiska operatorer {#logical-operators}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Om en nyckel och en lista med nyckelvärdepar förenklas som en array, returnerar funktionen värdet om nyckeln hittas eller returnerar ett standardvärde om det finns i arrayen. | <ul><li>NYCKEL: **Krävs** Nyckeln som ska matchas.</li><li>OPTIONS: **Obligatorisk** En förenklad matris med nyckel/värde-par. Ett standardvärde kan också placeras i slutet.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Om given stateCode är &quot;ca&quot;, &quot;California&quot;.<br>Om angiven stateCode är &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Om stateCode inte matchar följande, &quot;N/A&quot;. |
| iif | Utvärderar ett givet booleskt uttryck och returnerar det angivna värdet baserat på resultatet. | <ul><li>UTTRYCK: **Obligatoriskt** Det booleska uttryck som utvärderas.</li><li>TRUE_VALUE: **Required** Värdet som returneras om uttrycket utvärderas till true.</li><li>FALSE_VALUE: **Required** Värdet som returneras om uttrycket utvärderas till false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Sant&quot; |

{style="table-layout:auto"}

### Aggregering {#aggregation}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Returnerar det minsta av de angivna argumenten. Använder naturlig beställning. | <ul><li>OPTIONS: **Obligatoriskt** Ett eller flera objekt som kan jämföras med varandra.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Returnerar det maximala antalet angivna argument. Använder naturlig beställning. | <ul><li>OPTIONS: **Obligatoriskt** Ett eller flera objekt som kan jämföras med varandra.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Typkonverteringar {#type-conversions}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Konverterar en sträng till ett BigInteger. | <ul><li>STRING: **Required** Strängen som ska konverteras till ett BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;100000.34&quot;) | 1000000,34 |
| to_decimal | Konverterar en sträng till en dubbel sträng. | <ul><li>STRING: **Required** Strängen som ska konverteras till Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Konverterar en sträng till en flyttal. | <ul><li>STRING: **Required** Strängen som ska konverteras till ett flyttal.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Konverterar en sträng till ett heltal. | <ul><li>STRING: **Required** Strängen som ska konverteras till ett heltal.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON-funktioner {#json}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserialisera JSON-innehåll från angiven sträng. | <ul><li>STRING: **Required** JSON-strängen som ska avserialiseras.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}}) | Ett objekt som representerar JSON. |

{style="table-layout:auto"}

### Särskilda åtgärder {#special-operations}

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Skapar ett pseudoslumpmässigt ID. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |
| `fpid_to_ecid ` | Den här funktionen tar en FPID-sträng och konverterar den till ett ECID som ska användas i Adobe Experience Platform- och Adobe Experience Cloud-program. | <ul><li>STRING: **Required** Den FPID-sträng som ska konverteras till ECID.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Användaragentfunktioner {#user-agent}

Alla användaragentfunktioner i tabellen nedan kan returnera något av följande värden:

* Telefon - En mobil enhet med liten skärm (vanligen &lt; 7 tum)
* Mobil - En mobil enhet som ännu inte har identifierats. Den här mobila enheten kan vara en eReader, en surfplatta, en telefon, en klocka osv.

Mer information om enhetsfältvärden finns i [listan över enhetsfältvärden](#device-field-values) i bilagan till det här dokumentet.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extraherar operativsystemets namn från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extraherar operativsystemets huvudversion från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Hämtar operativsystemets version från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Hämtar operativsystemets namn och version från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Hämtar agentversionen från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Hämtar agentnamnet och huvudversionen från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Hämtar agentnamnet från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Hämtar enhetsklassen från användaragentsträngen. | <ul><li>USER_AGENT: **Required** Användaragentsträngen.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefon |

{style="table-layout:auto"}

### Analysfunktioner {#analytics}

>[!NOTE]
>
>Du får bara använda följande analysfunktioner för WebSDK- och Adobe Analytics-flöden.

| Funktion | Beskrivning | Parametrar | Syntax | Uttryck | Exempelutdata |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extraherar händelse-ID:t från en Analytics-händelsesträng. | <ul><li>EVENT_STRING: **Required** Den kommaavgränsade händelsesträngen Analytics.</li><li>EVENT_NAME: **Required** Händelsenamnet att extrahera och ID från.</li></ul> | aa_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 123456 |
| aa_get_event_value | Extraherar händelsevärdet från en Analytics-händelsesträng. Om händelsevärdet inte anges returneras 1. | <ul><li>EVENT_STRING: **Required** Den kommaavgränsade händelsesträngen Analytics.</li><li>EVENT_NAME: **Required** Händelsenamnet som ett värde ska extraheras från.</li></ul> | aa_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 5 |
| aa_get_product_categories | Extraherar produktkategorin från en analysproduktsträng. | <ul><li>PRODUCTS_STRING: **Required** Produktsträngen Analytics.</li></ul> | a_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories(&quot;;Exempel product 1;1;3.50,Exempelkategori 2;Exempelprodukt 2;1;5.99&quot;) | [null,&quot;Exempelkategori 2&quot;] |
| aa_get_product_names | Extraherar produktnamnet från en analysproduktsträng. | <ul><li>PRODUCTS_STRING: **Required** Produktsträngen Analytics.</li></ul> | a_get_product_names(PRODUCTS_STRING) | a_get_product_names(&quot;;Exempel: produkt 1;1;3.50,Exempelkategori 2;Exempelprodukt 2;1;5.99&quot;) | [&quot;Exempelprodukt 1&quot;,&quot;Exempelprodukt 2&quot;] |
| aa_get_product_quantity | Extraherar kvantiteterna från en Analytics-produktsträng. | <ul><li>PRODUCTS_STRING: **Required** Produktsträngen Analytics.</li></ul> | a_get_product_quantity(PRODUCTS_STRING) | a_get_product_quantity(&quot;;Exempel: produkt 1;1;3.50,Exempelkategori 2;Exempelprodukt 2&quot;) | [&quot;1&quot;, null] |
| a_get_product_prices | Extraherar priset från en analysproduktsträng. | <ul><li>PRODUCTS_STRING: **Required** Produktsträngen Analytics.</li></ul> | a_get_product_prices(PRODUCTS_STRING) | a_get_product_prices(&quot;;Exempelprodukt 1;1;3.50,Exempelkategori 2;Exempelprodukt 2&quot;) | [&quot;3.50&quot;, null] |
| aa_get_product_event_values | Extraherar värden för den namngivna händelsen från produktsträngen som en array med strängar. | <ul><li>PRODUCTS_STRING: **Required** Produktsträngen Analytics.</li><li>EVENT_NAME: **Required** Händelsenamnet som värden ska extraheras från.</li></ul> | a_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | a_get_product_event_values(&quot;;Exempel: product 1;1;4.20;event1=2.3\|event2=5:1,;Exempel: product 2;1;4.20;event1=3\|event2=2:2&quot;, &quot;event1&quot;) | [&quot;2.3&quot;, &quot;3&quot;] |
| aa_get_product_vars | Extraherar evar-värdena för den namngivna händelsen från produktsträngen som en array med strängar. | <ul><li>PRODUCTS_STRING: **Required** Produktsträngen Analytics.</li><li>EVAR_NAME: **Required** eVarnas namn som ska extraheras.</li></ul> | a_get_product_vars(PRODUCTS_STRING, EVENT_NAME) | a_get_product_vars(&quot;;Exempelprodukt;1;6.69;;eVar1=Merchandising value&quot;, &quot;eVar1&quot;) | [&quot;Merchandising value&quot;] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Objektkopia {#object-copy}

>[!TIP]
>
>Objektkopieringsfunktionen används automatiskt när ett objekt i källan mappas till ett objekt i XDM. Ingen ytterligare åtgärd krävs från användarna.

Du kan använda objektkopieringsfunktionen för att automatiskt kopiera attribut till ett objekt utan att göra ändringar i mappningen. Om källdata till exempel har strukturen:

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

och en XDM-struktur på

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

Därefter blir mappningen:

```json
address -> addr
address.line1 -> addr.addrLine1
```

I exemplet ovan kapslas även attributen `city` och `state` automatiskt vid körning eftersom objektet `address` mappas till `addr`. Om du skulle skapa ett `line2`-attribut i XDM-strukturen och dina indata även innehåller en `line2` i `address` -objektet, kommer det också att kapslas in automatiskt utan att mappningen behöver ändras manuellt.

För att automatisk mappning ska fungera måste följande krav vara uppfyllda:

* Objekt på överordnad nivå bör mappas.
* Nya attribut måste ha skapats i XDM-schemat;
* Nya attribut ska ha matchande namn i källschemat och XDM-schemat.

Om något av villkoren inte uppfylls måste du manuellt mappa källschemat till XDM-schemat med hjälp av dataprep.

## Bilaga

Nedan finns ytterligare information om hur du använder funktioner för dataprep

### Specialtecken {#special-characters}

Tabellen nedan visar en lista med reserverade tecken och motsvarande kodade tecken.

| Reserverat tecken | Kodat tecken |
| --- | --- |
| space | %20 |
| ! | %21 |
| &quot; | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
| ; | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Värden för enhetsfält {#device-field-values}

Tabellen nedan visar en lista med enhetsfältvärden och motsvarande beskrivningar.

| Enhet | Beskrivning |
| --- | --- |
| Skrivbord | En stationär eller bärbar typ av enhet. |
| Anonymiserad | En anonym enhet. I vissa fall är det `useragents` som har ändrats av en anonymiseringsprogramvara. |
| Okänd | En okänd enhet. Dessa är vanligtvis `useragents` som inte innehåller någon information om enheten. |
| Mobil | En mobil enhet som ännu inte har identifierats. Den här mobila enheten kan vara en eReader, en surfplatta, en telefon, en klocka osv. |
| Tablet | En mobil enhet med stor skärm (vanligtvis > 7 tum). |
| Telefon | En mobil enhet med liten skärm (vanligen &lt; 7 tum). |
| Titta | En mobil enhet med en liten skärm (vanligen &lt; 2 tum). Dessa enheter fungerar normalt som en extra skärm för en typ av telefon/surfplatta. |
| Förstärkt verklighet | En mobil enhet med AR-funktioner. |
| Virtuell verklighet | En mobil enhet med VR-funktioner. |
| eReader | En enhet som liknar en surfplatta, men vanligtvis med en [!DNL eInk]-skärm. |
| Rutan Ange överkant | En ansluten enhet som tillåter interaktion via en skärm i tv-storlek. |
| TV | En enhet som liknar digitalboxen, men är inbyggd i tv:n. |
| Hemutrustning | En (vanligtvis stor) hemutrustning, som ett kylskåp. |
| Spelkonsol | Ett fast spelsystem som [!DNL Playstation] eller [!DNL XBox]. |
| Handdatorspelskonsol | Ett mobilt spelsystem som [!DNL Nintendo Switch]. |
| Voice | En röststyrd enhet som [!DNL Amazon Alexa] eller [!DNL Google Home]. |
| Bil | En fordonsbaserad webbläsare. |
| Robot | Robotar som besöker en webbplats. |
| Robot Mobile | Robotar som besöker en webbplats men som anger att de vill bli synliga som mobilbesökare. |
| Robot Imitator | Robotar som besöker en webbplats, låtsas vara robotar som [!DNL Google], men de gör det inte. **Obs!**: I de flesta fall är Robot Imitators robotar. |
| Cloud | Ett molnbaserat program. Detta är varken robotar eller hackare, men är program som måste anslutas. Detta inkluderar [!DNL Mastodon] servrar. |
| Hacker | Det här enhetsvärdet används om skript upptäcks i strängen `useragent`. |

{style="table-layout:auto"}

### Kodexempel {#code-samples}

#### map_get_values {#map-get-values}

+++Markera för att visa exempel

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++Markera för att visa exempel

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++Markera för att visa exempel

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**Syntax 1**

+++Markera för att visa exempel

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**Syntax 2**

+++Markera för att visa exempel

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**Syntax 3**

+++Markera för att visa exempel

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++Markera för att visa exempel

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

