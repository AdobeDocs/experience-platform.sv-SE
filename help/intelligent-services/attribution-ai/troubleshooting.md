---
keywords: Experience Platform;komma igång;attribueringai;populära ämnen;attribueringsindata;attribueringai output;attribueringai troublesholeshooting;attribueringsfel
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Attribution AI
title: Felsökning av Attribution AI
description: Hitta svar på vanliga fel i Attribution AI.
type: Documentation
source-git-commit: 896dda631cd4182f278de0607bea442d8366fe8c
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
