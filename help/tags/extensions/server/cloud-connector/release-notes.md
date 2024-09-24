---
title: Versionsinformation för Adobe Experience Platform Cloud Connector-tillägget
description: De senaste versionsinformationen för Cloud Connector-tillägget i Adobe Experience-plattformen.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '128'
ht-degree: 100%

---

# Versionsinformation för Adobe Experience Platform Cloud Connector-tillägget

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

## 17 januari 2023

v1.0.1

* Åtgärdat ett problem där en giltig JSON som klistrats in i textområdet Body Raw sparades som en sträng i stället för en JSON.
* Tillåt inte att Body anges på GET- eller HEAD-begäranden.
* Åtgärdat en bugg där sparande av ett svar som var större än 5 kb gjorde att regelkörningen misslyckades.
