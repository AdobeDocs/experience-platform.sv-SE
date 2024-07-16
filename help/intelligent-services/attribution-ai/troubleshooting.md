---
keywords: Experience Platform;komma igång;attribueringai;populära ämnen;attribueringsindata;attribueringai output;attribueringai troublesholeshooting;attribueringsfel
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Felsökning av Attribution AI
description: Hitta svar på vanliga fel i Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Felsökning av Attribution AI

Det här dokumentet innehåller svar på vanliga frågor om Attribution AI.

## Det går inte att komma åt Attribution AI i Chrome Incognito

Det finns inläsningsfel i Google Chrome inkognito-läge på grund av uppdateringar i Google Chrome inkognito-lägessäkerhetsinställningarna. Vi arbetar aktivt med Chrome för att göra experience.adobe.com till en betrodd domän.

<img src="./images/faq/error.PNG" width="500" /><br />

### Rekommenderad åtgärd

För att lösa det här problemet måste du lägga till experience.adobe.com som en webbplats som alltid kan använda cookies. Börja med att gå till **chrome://settings/cookies**. Bläddra sedan nedåt till avsnittet **Anpassade beteenden** följt av att klicka på knappen **Lägg till** bredvid&quot;webbplatser som alltid kan använda cookies&quot;. Kopiera och klistra in `[*.]experience.adobe.com` i den pover som visas och markera sedan kryssrutan **Inkludera cookies från tredje part** på den här webbplatsen. När du är klar väljer du **Lägg till** och läser in Attribution AI igen i incognito.

![rekommenderad korrigering](./images/faq/cookies2.gif)
