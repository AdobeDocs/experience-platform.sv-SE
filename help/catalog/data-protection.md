---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Dataskydd i Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Dataskydd i Adobe Experience Platform

Alla data som importeras och används av Adobe Experience Platform lagras i Data Lake, ett mycket detaljerat datalager som innehåller alla data som hanteras av Platform, oavsett ursprung eller filformat. Alla data som lagras i Data Lake krypteras, lagras och hanteras i ett isolerat Microsoft Azure Data Lake Storage-konto som är unikt för din organisation.

Följande processflödesdiagram visar hur data importeras, bearbetas, krypteras och bevaras av Experience Platform:

![](images/data-protection/flow.png)

Mer information om hur vilande data krypteras i Data Lake Storage finns i dokumentet om [datakryptering i Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Information om hur vilande data krypteras i Cosmos DB finns i dokumentet om [datakryptering i Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).