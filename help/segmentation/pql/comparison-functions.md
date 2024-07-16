---
solution: Experience Platform
title: PQL jämförelsefunktioner
description: Jämförelsefunktioner används för att jämföra olika uttryck och värden och returnerar"true" eller"false" i enlighet med detta.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Jämförelsefunktioner

Jämförelsefunktioner används för att jämföra olika uttryck och värden, vilket returnerar `true` eller `false` utifrån detta. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Lika med

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

## Större än

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

## Större än eller lika med

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

## Mindre än

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

## Mindre än eller lika med

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

Nu när du har lärt dig mer om jämförelsefunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profile Query Language-översikten](./overview.md).
