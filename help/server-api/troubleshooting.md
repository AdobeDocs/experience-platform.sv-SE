---
title: Felsökning
description: Lär dig hur du felsöker fel när du använder API:t för Adobe Experience Platform Edge Network Server
seo-description: Learn how to troubleshoot errors when using the Adobe Experience Platform Edge Network Server API
keywords: edge network;gateway;api;troubleshoot;errors;griffon
exl-id: f0223fca-30ec-4229-93a5-3faa6cef5482
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 1%

---

# Felsökning

Med API:t för Adobe Experience Platform Edge Network Server kan du samla in felsökningsinformation från tjänster när dina händelser bearbetas via Edge Network-datainsamlingsflödet.

Samma mekanism som används av [Felsökning för Experience Platform](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) gör att du kan felsöka API-baserade implementeringar.

Använda [Projektgaller](https://aep-sdks.gitbook.io/docs/beta/project-griffon)kan du skapa ett felsökningssessions-ID som du kan använda i Edge Network-begäranden för att spåra händelser.
