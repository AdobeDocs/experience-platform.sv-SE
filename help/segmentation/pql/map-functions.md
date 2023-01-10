---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profilfrågespråk;kartfunktioner;karta;
solution: Experience Platform
title: PQL-kartfunktioner
description: PQL (Profile Query Language) har funktioner som underlättar interaktion med kartor.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# Kartfunktioner

[!DNL Profile Query Language] (PQL) har funktioner som underlättar interaktion med kartor. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikt](./overview.md).

## Hämta

The `get` används för att hämta värdet för en karta för en viss nyckel.

**Format**

```sql
{MAP}.get({STRING})
```

**Exempel**

Följande PQL-fråga hämtar värdet för identitetskartan för nyckeln `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Tangenter

The `keys` används för att hämta alla nycklar för en viss karta.

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

The `values` används för att hämta alla värden för en viss karta.

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

Nu när du har lärt dig mer om kartfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profilfrågespråk - översikt](./overview.md).
