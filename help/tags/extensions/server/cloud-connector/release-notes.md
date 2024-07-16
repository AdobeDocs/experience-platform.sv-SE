---
title: Versionsinformation för Adobe Experience Platform Cloud Connector-tillägget
description: Den senaste versionsinformationen för Cloud Connector-tillägget i Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Versionsinformation om Adobe Experience Platform Cloud Connector Extension

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

## 17 januari 2023

v1.0.1

* Åtgärda ett problem där en giltig JSON-fil som klistras in i textområdet Body Raw sparades som en sträng i stället för som en JSON-fil.
* Tillåt inte att Body anges på GET- eller HEAD-begäran.
* Åtgärda ett fel där ett svar som är större än 5 kB skulle få regelkörningen att misslyckas.
