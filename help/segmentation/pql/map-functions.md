---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profilfrågespråk;kartfunktioner;karta;
solution: Experience Platform
title: PQL-kartfunktioner
topic: developer guide
description: PQL (Profile Query Language) har funktioner som underlättar interaktion med kartor.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---


# Kartfunktioner

[!DNL Profile Query Language] (PQL) har funktioner som underlättar interaktion med kartor. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Hämta

Funktionen `get` används för att hämta värdet för en karta för en given nyckel.

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

Funktionen `keys` används för att hämta alla nycklar för en given karta.

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

Funktionen `values` används för att hämta alla värden för en given karta.

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

Nu när du har lärt dig mer om kartfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).
