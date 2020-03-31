---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kartfunktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Kartfunktioner

PQL (Profile Query Language) har funktioner som underlättar interaktion med kartor. Mer information om andra PQL-funktioner finns i översikten [för](./overview.md)profilfrågespråk.

## Hämta

Funktionen används `get` för att hämta värdet för en karta för en given nyckel.

**Format**

```sql
{MAP}.get({STRING})
```

**Exempel**

Följande PQL-fråga hämtar värdet på identitetskartan för nyckeln `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Tangenter

Funktionen används `keys` för att hämta alla nycklar för en viss karta.

**Format**

```sql
{MAP}.keys()
```

**Exempel**

Följande PQL-fråga hämtar alla nycklar för kartan `identityMap`.

```sql
identityMap.keys()
```

## Värden

Funktionen används `values` för att hämta alla värden för en viss karta.

**Format**

```sql
{MAP}.values()
```

**Exempel**

Följande PQL-fråga hämtar alla värden för kartan `identityMap`.

```sql
identityMap.values()
```

## Nästa steg

Nu när du har lärt dig mer om kartfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.
