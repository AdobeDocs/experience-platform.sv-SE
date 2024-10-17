---
solution: Experience Platform
title: PQL Map-funktioner
description: Profile Query Language (PQL) har funktioner som underlättar interaktion med kartor.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Kartfunktioner

[!DNL Profile Query Language] (PQL) erbjuder funktioner som underlättar interaktion med kartor. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Hämta

Funktionen `get` används för att hämta värdet för en karta för en given nyckel som ett objekt.

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

Funktionen `keys` används för att hämta alla nycklar för en given karta som en matris eller lista.

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

Funktionen `values` används för att hämta alla värden för en given karta som en matris eller lista.

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

Nu när du har lärt dig mer om kartfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profile Query Language-översikten](./overview.md).
