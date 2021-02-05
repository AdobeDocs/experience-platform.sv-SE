---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;pql;PQL;Profilfrågespråk;objektfunktioner;objekt;
solution: Experience Platform
title: PQL-objektfunktioner
topic: developer guide
description: PQL (Profile Query Language) har funktioner som underlättar interaktion med objekt.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# Objektfunktioner

[!DNL Profile Query Language] (PQL) har funktioner som underlättar interaktion med objekt. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Är null

Funktionen `isNull` avgör om en objektreferens inte finns.

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

Funktionen `isNotNull` avgör om det finns en objektreferens.

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

Nu när du har lärt dig om objektfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i [översikten över profilfrågespråk](./overview.md).