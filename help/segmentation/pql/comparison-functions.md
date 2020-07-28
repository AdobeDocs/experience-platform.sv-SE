---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Jämförelsefunktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 3%

---


# Jämförelsefunktioner

Jämförelsefunktioner används för att jämföra olika uttryck och värden, returnera `true` eller `false` därefter. Mer information om andra PQL-funktioner finns i översikten [för](./overview.md)profilfrågespråk.

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

Funktionen `!=` (inte lika med) kontrollerar om ett värde eller uttryck **inte** är lika med ett annat värde eller uttryck.

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

Nu när du har lärt dig mer om jämförelsefunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
