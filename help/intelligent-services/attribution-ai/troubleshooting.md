---
keywords: Experience Platform;komma igång;attribueringai;populära ämnen;attribueringsindata;attribueringai output;attribueringai troublesholeshooting;attribueringsfel
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: Felsökning av Attribution AI
description: Hitta svar på vanliga fel i Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Felsökning av Attribution AI

Det här dokumentet innehåller svar på vanliga frågor om Attribution AI.

## Det går inte att komma åt Attribution AI i Chrome Incognito

Det finns inläsningsfel i Google Chrome-läget på grund av uppdateringar i Google Chrome-säkerhetsinställningarna för inkodade lägen. Vi arbetar aktivt med Chrome för att göra experience.adobe.com till en betrodd domän.

<img src="./images/faq/error.PNG" width="500" /><br />

### Rekommenderad korrigering

För att lösa det här problemet måste du lägga till experience.adobe.com som en webbplats som alltid kan använda cookies. Börja med att navigera till **chrome://settings/cookies**. Bläddra sedan nedåt till **Anpassade beteenden** följt av att välja **Lägg till** intill&quot;webbplatser som alltid kan använda cookies&quot;. Kopiera och klistra in i den pover som visas `[*.]experience.adobe.com` väljer du **Inklusive cookies från tredje part** på den här platsen. När du är klar väljer du **Lägg till** och ladda om Attribution AI i inkognito.

![rekommenderad korrigering](./images/faq/cookies2.gif)
