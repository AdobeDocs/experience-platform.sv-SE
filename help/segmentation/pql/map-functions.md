---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;map functions;map;
solution: Experience Platform
title: Kartfunktioner
topic: developer guide
description: PQL (Profile Query Language) har funktioner som underlättar interaktion med kartor.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 3%

---


# Kartfunktioner

[!DNL Profile Query Language] (PQL) har funktioner som underlättar interaktion med kartor. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

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
