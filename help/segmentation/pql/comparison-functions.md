---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profile Query Language;jämförelsefunktioner;jämförelse;
solution: Experience Platform
title: PQL-jämförelsefunktioner
topic-legacy: developer guide
description: Jämförelsefunktioner används för att jämföra mellan olika uttryck och värden och returnerar"true" eller"false" i enlighet därmed.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 7%

---

# Jämförelsefunktioner

Jämförelsefunktioner används för att jämföra olika uttryck och värden, vilket returnerar `true` eller `false` därefter. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Är lika med

Funktionen `=` (lika med) kontrollerar om ett värde eller uttryck är lika med ett annat värde eller uttryck.

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Exempel**

Följande PQL-fråga kontrollerar om hemadresslandet är i Kanada.

```sql
homeAddress.countryISO = "CA"
```

## Inte lika med

Funktionen `!=` (inte lika med) kontrollerar om ett värde eller uttryck är **inte** lika med ett annat värde eller uttryck.

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**Exempel**

Följande PQL-fråga kontrollerar om hemadresslandet inte är i Kanada.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

Funktionen `>` (större än) används för att kontrollera om det första värdet är större än det andra värdet.

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Exempel**

Följande PQL-fråga definierar personer vars födelsedagar inte infaller i januari eller februari.

```sql
person.birthMonth > 2
```

## Greater than or equal to

Funktionen `>=` (större än eller lika med) används för att kontrollera om det första värdet är större än eller lika med det andra värdet.

**Format**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Exempel**

Följande PQL-fråga definierar personer vars födelsedagar inte infaller i januari eller februari.

```sql
person.birthMonth >= 3
```

## Less than

Jämförelsefunktionen `<` (mindre än) används för att kontrollera om det första värdet är mindre än det andra värdet.

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Exempel**

Följande PQL-fråga definierar personer vars födelsedag är i januari.

```sql
person.birthMonth < 2
```

## Less than or equal to

Jämförelsefunktionen `<=` (mindre än eller lika med) används för att kontrollera om det första värdet är mindre än eller lika med det andra värdet.

**Format**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Exempel**

Följande PQL-fråga definierar personer vars födelsedag är i januari eller februari.

```sql
person.birthMonth <= 2
```

## Nästa steg

Nu när du har lärt dig mer om jämförelsefunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).
