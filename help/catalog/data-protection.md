---
keywords: Experience Platform;hem;populära ämnen;katalog;dataskydd;krypteringsdatasjön
solution: Experience Platform
title: Dataskydd i Adobe Experience Platform
topic-legacy: data protection
description: Alla data som lagras i Data Lake krypteras, lagras och hanteras i ett isolerat Microsoft Azure Data Lake Storage-konto som är unikt för din organisation. Följande processflödesdiagram visar hur data importeras, bearbetas, krypteras och bevaras av Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Dataskydd i Adobe Experience Platform

Alla data som importeras och används av Adobe Experience Platform lagras i [!DNL Data Lake], ett mycket detaljerat datalager som innehåller alla data som hanteras av [!DNL Platform], oavsett ursprung eller filformat. Alla data som lagras i [!DNL Data Lake] krypteras, lagras och hanteras i ett isolerat lagringskonto för [!DNL Microsoft Azure Data Lake] som är unikt för din organisation.

Följande processflödesdiagram visar hur data importeras, bearbetas, krypteras och bevaras av [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Mer information om hur vilande data krypteras i [!DNL Data Lake Storage] finns i dokumentet om [datakryptering i Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Information om hur vilande data krypteras i [!DNL Cosmos DB] finns i dokumentet om [datakryptering i Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).
