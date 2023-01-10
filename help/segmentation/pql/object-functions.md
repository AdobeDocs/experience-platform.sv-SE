---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profilfrågespråk;objektfunktioner;objekt;
solution: Experience Platform
title: PQL-objektfunktioner
description: PQL (Profile Query Language) har funktioner som underlättar interaktion med objekt.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---

# Objektfunktioner

[!DNL Profile Query Language] (PQL) har funktioner som underlättar interaktion med objekt. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikt](./overview.md).

## Är null

The `isNull` funktionen avgör om en objektreferens inte finns.

**Format**

```sql
{OBJECT}.isNull()
```

**Exempel**

Följande PQL-fråga kontrollerar om personens hemadress inte finns.

```sql
person.homeAddress.isNull()
```

## Är inte null

The `isNotNull` funktionen avgör om det finns en objektreferens.

**Format**

```sql
{OBJECT}.isNotNull()
```

**Exempel**

Följande PQL-fråga kontrollerar om personens hemadress finns.

```sql
person.homeAddress.isNotNull()
```

## Nästa steg

Nu när du har lärt dig om objektfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [Profilfrågespråk - översikt](./overview.md).
