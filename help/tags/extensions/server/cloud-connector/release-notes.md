---
title: Versionsinformation för Adobe Experience Platform Cloud Connector-tillägget
description: Den senaste versionsinformationen för Cloud Connector-tillägget i Adobe Experience Platform.
source-git-commit: e232ad7a9b581e65f7f4240bbc06155aec409eb7
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# Versionsinformation om Adobe Experience Platform Cloud Connector Extension

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

## 17 januari 2023

v1.0.1

* Åtgärda ett problem där en giltig JSON-fil som klistras in i textområdet Body Raw sparades som en sträng i stället för som en JSON-fil.
* Tillåt inte att Body anges på GET- eller HEAD-begäran.
* Åtgärda ett fel där ett svar som är större än 5 kB skulle få regelkörningen att misslyckas.

