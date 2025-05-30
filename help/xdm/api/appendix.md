---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;Experience data model;Experience data model;data model;data model;data model;schema register;schema Registry;compatibility;compatibility;compatibility mode;Compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: API-handbok för schematabell
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med API:t för schemaregister.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---

# API-guide för schematabell

Det här dokumentet innehåller ytterligare information om hur du arbetar med API:t [!DNL Schema Registry].

## Använda frågeparametrar {#query}

[!DNL Schema Registry] har stöd för användning av frågeparametrar för att filtrera resultat och sidor när resurser listas.

>[!NOTE]
>
>När flera frågeparametrar kombineras måste de avgränsas med et-tecken (`&`).

### Sidindelning {#paging}

De vanligaste frågeparametrarna för sidindelning är:

| Parameter | Beskrivning |
| --- | --- |
| `orderby` | Sortera resultat efter en specifik egenskap. Exempel: `orderby=title` sorterar resultaten efter titel i stigande ordning (A-Z). Om du lägger till `-` före parametervärdet (`orderby=-title`) sorteras objekt efter rubrik i fallande ordning (Z-A). |
| `limit` | När den används tillsammans med en `orderby`-parameter begränsar `limit` det maximala antalet objekt som ska returneras för en viss begäran. Den här parametern kan inte användas utan en `orderby`-parameter.<br><br>Parametern `limit` anger ett positivt heltal (mellan `0` och `500`) som ett *tips* om det maximala antalet objekt som ska returneras. `limit=5` returnerar till exempel bara fem resurser i listan. Detta värde respekteras dock inte. Den faktiska svarsstorleken kan vara mindre eller större, vilket begränsas av behovet att tillhandahålla den tillförlitliga funktionen för parametern `start`, om en sådan anges. |
| `start` | När den används tillsammans med en `orderby`-parameter anger `start` var den deluppsatta listan med objekt ska börja. Den här parametern kan inte användas utan en `orderby`-parameter. Det här värdet kan hämtas från attributet `_page.next` för ett listsvar och användas för att komma åt nästa resultatsida. Om värdet `_page.next` är null finns det ingen ytterligare sida tillgänglig.<br><br>Normalt utelämnas den här parametern för att få fram den första resultatsidan. Därefter ska `start` anges till det maximala värdet för den primära sorteringsegenskapen för fältet `orderby` som togs emot på föregående sida. API-svaret returnerar sedan poster som börjar med de som har en primär sorteringsegenskap från `orderby` som är strikt större än (för stigande) eller strikt mindre än (för fallande) det angivna värdet.<br><br>Om parametern `orderby` till exempel är inställd på `orderby=name,firstname` innehåller parametern `start` ett värde för egenskapen `name`. Om du i det här fallet vill visa de nästa 20 posterna för en resurs omedelbart efter namnet &quot;Miller&quot;, använder du: `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filtrering {#filtering}

Du kan filtrera resultat med parametern `property` som används för att tillämpa en viss operator på en viss JSON-egenskap i de hämtade resurserna. Operatorer som stöds är:

| Operatör | Beskrivning | Exempel |
| --- | --- | --- |
| `==` | Filtrerar efter om egenskapen är lika med det angivna värdet. | `property=title==test` |
| `!=` | Filtrerar efter om egenskapen inte är lika med det angivna värdet. | `property=title!=test` |
| `<` | Filtrerar efter om egenskapen är mindre än det angivna värdet. | `property=version<5` |
| `>` | Filtrerar efter om egenskapen är större än det angivna värdet. | `property=version>5` |
| `<=` | Filtrerar efter om egenskapen är mindre än eller lika med det angivna värdet. | `property=version<=5` |
| `>=` | Filtrerar efter om egenskapen är större än eller lika med det angivna värdet. | `property=version>=5` |
| (Ingen) | Om du bara anger egenskapsnamnet returneras bara poster där egenskapen finns. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>Du kan använda parametern `property` för att filtrera schemafältgrupper efter deras kompatibla klass. `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` returnerar till exempel bara fältgrupper som är kompatibla med klassen [!DNL XDM Individual Profile].

## Kompatibilitetsläge {#compatibility}

[!DNL Experience Data Model] (XDM) är en öppet dokumenterad specifikation som drivs av Adobe för att förbättra interoperabiliteten, uttrycksfullheten och kraften i digitala upplevelser. Adobe underhåller källkoden och formella XDM-definitioner i ett [öppen källkodsprojekt på GitHub](https://github.com/adobe/xdm/). Dessa definitioner är skrivna i XDM Standard Notation, där JSON-LD (JavaScript Object Notation for Linked Data) och JSON Schema används som grammatik för att definiera XDM-scheman.

När du tittar på formella XDM-definitioner i den offentliga databasen ser du att standard-XDM skiljer sig från det du ser i Adobe Experience Platform. Det du ser i [!DNL Experience Platform] kallas Kompatibilitetsläge och ger en enkel mappning mellan standard-XDM och hur det används i [!DNL Experience Platform].

### Så här fungerar kompatibilitetsläget

Kompatibilitetsläge gör att XDM JSON-LD-modellen kan arbeta med befintlig datainfrastruktur genom att ändra värden inom standard-XDM samtidigt som semantiken förblir densamma. Den använder en kapslad JSON-struktur och visar scheman i ett trädliknande format.

Den största skillnaden mellan standard-XDM och kompatibilitetsläge är borttagningen av &quot;xdm:&quot;-prefixet för fältnamn.

Följande är en jämförelse sida vid sida som visar födelsedagsrelaterade fält (där attributen &quot;description&quot; har tagits bort) i både standard-XDM och kompatibilitetsläge. Observera att fälten för kompatibilitetsläge innehåller en referens till XDM-fältet och dess datatyp i attributen &quot;meta:xdmField&quot; och &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>Standard XDM</th>
  <th>Kompatibilitetsläge</th>
  <tr>
  <td>
  <pre class=" language-json">
&lbrace;
  "xdm:bornDate": &lbrace;
    "title": "Birth Date",
    "type": "string",
    "format": "date"
  &rbrace;,
  "xdm:bornDayAndMonth": &lbrace;
    "title": "Birth Date",
    "type": "string",
    "mönster": "[0-1][0-9]-[0-9][0-9]"
  &rbrace;,
  "xdm:bornYear": &lbrace;
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "maximum": 32767
  &rbrace;
&rbrace;
  </pre>
  </td>
  <td>
  <pre class=" language-json">
&lbrace;
  "bornDate": &lbrace;
    "title": "Birth Date",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:bornDate",
    "meta:xdmType": "date"
  &rbrace;,
  "bornDayAndMonth": &lbrace;
    "title": "Birth Date",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]",
    "meta:xdmField": "xdm:bornDayAndMonth",
    "meta:xdmType": "string"
  &rbrace;,
  "bornYear": &lbrace;
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "maximum": 32767,
    "meta:xdmField": "xdm:bornYear",
    "meta:xdmType": "short"
  &rbrace;
&rbrace;
      </pre>
  </td>
  </tr>
</table>

### Varför krävs kompatibilitetsläge?

Adobe Experience Platform är utformat för att fungera tillsammans med flera lösningar och tjänster, var och en med sina egna tekniska utmaningar och begränsningar (till exempel hur vissa tekniker hanterar specialtecken). Kompatibilitetsläge har utvecklats för att övervinna dessa begränsningar.

De flesta [!DNL Experience Platform]-tjänster, inklusive [!DNL Catalog], [!DNL Data Lake] och [!DNL Real-Time Customer Profile] använder [!DNL Compatibility Mode] i stället för standard-XDM. API:t [!DNL Schema Registry] använder också [!DNL Compatibility Mode], och exemplen i det här dokumentet visas alla med [!DNL Compatibility Mode].

Det är värt att veta att en mappning görs mellan standard-XDM och sättet den används i [!DNL Experience Platform], men det bör inte påverka din användning av [!DNL Experience Platform]-tjänster.

Du har tillgång till projektet med öppen källkod, men när det gäller att interagera med resurser via [!DNL Schema Registry] innehåller API-exemplen i det här dokumentet de bästa metoder du bör känna till och följa.
