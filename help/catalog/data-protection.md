---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Dataskydd i Adobe Experience Platform
topic: data protection
description: Alla data som lagras i Data Lake krypteras, lagras och hanteras i ett isolerat Microsoft Azure Data Lake Storage-konto som är unikt för din organisation. Följande processflödesdiagram visar hur data importeras, bearbetas, krypteras och bevaras av Experience Platform.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Dataskydd i Adobe Experience Platform

Alla data som importeras och används av Adobe Experience Platform lagras i [!DNL Data Lake]ett mycket detaljerat datalager som innehåller alla data som hanteras av, [!DNL Platform]oavsett ursprung eller filformat. Alla data som lagras i [!DNL Data Lake] krypteras, lagras och hanteras i ett isolerat [!DNL Microsoft Azure Data Lake] lagringskonto som är unikt för din organisation.

Följande processflödesdiagram visar hur data importeras, bearbetas, krypteras och bevaras av [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Mer information om hur vilande data krypteras i [!DNL Data Lake Storage]finns i dokumentet om [datakryptering i Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Information om hur vilande data krypteras i [!DNL Cosmos DB]finns i dokumentet om [datakryptering i Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).