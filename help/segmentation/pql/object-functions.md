---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objektfunktioner
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Objektfunktioner

[!DNL Profile Query Language] (PQL) har funktioner som underlättar interaktion med objekt. Mer information om andra PQL-funktioner finns i [[!DNL Profile Query Language] översikten](./overview.md).

## Är null

Funktionen avgör `isNull` om en objektreferens inte finns.

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

Funktionen avgör `isNotNull` om det finns en objektreferens.

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

Nu när du har lärt dig om objektfunktioner kan du använda dem i dina PQL-frågor. Mer information om andra PQL-funktioner finns i översikten [över](./overview.md)profilfrågespråk.