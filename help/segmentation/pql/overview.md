---
keywords: Experience Platform;home;popular topics;PQL;pql;profile query language
solution: Experience Platform
title: Profilfrågespråk (PQL) - översikt
topic: developer guide
description: Den här guiden ger en allmän översikt över PQL, som beskriver riktlinjer för formatering och innehåller exempel på PQL-uttryck.
translation-type: tm+mt
source-git-commit: 5a10a31f4be5173af8b459b9ab8a53096348be1d
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---


# [!DNL Profile Query Language] (PQL) - översikt

[!DNL Profile Query Language] (PQL) är ett [!DNL Experience Data Model] (XDM)-kompatibelt frågespråk som har utformats för att stödja definition och körning av segmenteringsfrågor för [!DNL Real-time Customer Profile] data.

Den här guiden ger en allmän översikt över PQL, som beskriver riktlinjer för formatering och innehåller exempel på PQL-uttryck.

## PQL-frågeformatering

PQL-frågor har följande signatur:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Indataparametern kan vara enkel primitiv, till exempel ett booleskt värde eller en sträng, eller en mer komplex typ, till exempel ett objekt, en array eller en karta.

Det finns **tre** olika sätt att referera till indataparametrar i brödtexten för ett PQL-uttryck:

### Implicit referens till den första parametern

I exemplet nedan kan en egenskapsreferens (`homeAddress`) göras direkt till den första parametern eftersom den alltid är i kontexten.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Explicit referens till den första parametern

I exemplet nedan refererar `$1` till den första parametern. Detta resulterar i att `$2` refererar till den andra parametern osv.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Användning av namngivna variabler med lambda-notation

I exemplet nedan `Profile` är ett variabelnamn som frågeförfattaren kan välja.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL-litteraler

PQL har stöd för följande literaltyper:

| Literal | Definition | Exempel |
| ------- | ---------- | ------- |
| Sträng | En datatyp som består av tecken omgivna av dubbla citattecken. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Boolean | En datatyp som är antingen true eller false. | `true`, `false` |
| Heltal | En datatyp som representerar ett heltal. Den kan vara positiv, negativ eller noll. | `-201`, `0`, `412` |
| Dubbel | En datatyp som representerar ett reellt tal. Den kan vara positiv, negativ eller noll. | `-51.24`, `3.14`, `0.6942058` |
| Datum | En datatyp som kan användas för att skapa datum baserat på år, månad och dag som heltalsparametrar. Det är formaterat som `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | En datatyp som består av en grupp med andra literala värden. Här används hakparenteser för att gruppera och kommatecken för att avgränsa mellan olika värden. <br> **Obs!** Du kan inte komma åt egenskaper direkt för objekt i en array. Om du behöver få åtkomst till en egenskap i en array är metoden `select X from array where X.item = ...`som stöds. <br> PQL reserverar ordet `xEvent` för att referera till en array med upplevelsehändelser som är kopplade till en profil. | `[1, 4, 7]`, `["US", "CA"]` |
| Relativa tidsreferenser | Reserverade ord som kan användas för att skapa tidsstämplar och tidsintervallreferenser. <ul><li>idag, i går, imorgon</li><li>this, last, next</li><li>före, efter, från</li><li>millisekunder, sekund(er), minut(er), timme(ar), dag(ar), vecka(er), månad(er), år, årtionde, århundraden/århundraden, millennium/millennium</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL-funktioner

Följande tabell visar de olika kategorierna av PQL-funktioner som stöds, inklusive länkar till ytterligare dokumentation för mer information.

| Kategori | Definition |
| -------- | ---------- |
| Boolean | Används för att implementera booleskt algebra i PQL. Mer information om dessa funktioner finns i dokumentet [med](./boolean-functions.md)booleska funktioner. |
| Jämförelse | Används för att jämföra olika PQL-element. Mer information om dessa funktioner finns i [jämförelsefunktionsdokumentet](./comparison-functions.md). |
| Array, lista och uppsättning | Används för att interagera med arrayer, listor och uppsättningar. Mer information om dessa funktioner finns i [arrayen, listan och funktionsdokumentet](./array-functions.md). |
| Mappa | Används för att interagera med kartor. Mer information om dessa funktioner finns i [kartfunktionsdokumentet](./map-functions.md). |
| Sträng | Används för att interagera med strängar. Mer information om dessa funktioner finns i [strängfunktionsdokumentet](./string-functions.md). |
| Objekt | Används för att interagera med objekt. Mer information om de här funktionerna finns i [objektfunktionsdokumentet](./object-functions.md). |
| Aritmetisk | Används för att utföra grundläggande aritmetik på PQL-element. Mer information om dessa funktioner finns i dokumentet med [aritmetiska funktioner](./arithmetic-functions.md) |
| Aggregera | Används för att kombinera resultat från en array till ett enda resultat. Mer information om sammanställningsfunktioner finns i dokumentet [med](./aggregation-functions.md)sammanställningsfunktioner. |
| Datum och tid | Används tillsammans med datum-, tids- och datetime-objekt. Mer information om dessa funktioner finns i dokumentet [med](./datetime-functions.md)datum-/tidsfunktioner. |
| Filter | Används för att filtrera data inom arrayer. Mer information om dessa funktioner finns i [filterfunktionsdokumentet](./filter-functions.md). |
| Logiska kvantifierare | Används för att infoga villkor i en array. Mer information finns i dokumentet [med](./logical-quantifiers.md)logiska kvantifierare. |
| Diverse | Funktioner som inte passar i någon av ovanstående kategorier finns i dokumentet [med](./misc-functions.md)diverse funktioner. |

## Nästa steg

Nu när du har lärt dig att använda [!DNL Profile Query Language]kan du använda PQL när du skapar och ändrar segment. Mer information om segmentering finns i [segmenteringsöversikten](../home.md).