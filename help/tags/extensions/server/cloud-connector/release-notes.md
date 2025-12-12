---
title: Versionsinformation för Adobe Experience Platform Cloud Connector-tillägget
description: De senaste versionsinformationen för Cloud Connector-tillägget i Adobe Experience-plattformen.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 100%

---

# Versionsinformation för Adobe Experience Platform Cloud Connector-tillägget

## 17 januari 2023

v1.0.1

* Åtgärdat ett problem där en giltig JSON som klistrats in i textområdet Body Raw sparades som en sträng i stället för en JSON.
* Tillåt inte att Body anges på GET- eller HEAD-begäranden.
* Åtgärdat en bugg där sparande av ett svar som var större än 5 kb gjorde att regelkörningen misslyckades.
