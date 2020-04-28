---
title: Hjälp för Adobe Experience Platform Web SDK
seo-title: Hjälp för Adobe Experience Platform Web SDK
description: Lär dig vad Adobe Experience Platform Web SDK är och hur det kan användas.
seo-description: gör det möjligt för kunder med Adobe Experience Cloud att interagera med de olika tjänsterna i Experience Cloud.
translation-type: tm+mt
source-git-commit: 5027ae2cd083631d7122346796ef93572c129d3f

---


# (Beta) Vad är Adobe Experience Platform Web SDK

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK är för närvarande en betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att kunder i Adobe Experience Cloud kan interagera med de olika tjänsterna i Experience Cloud via Adobe Experience Platform Edge Network.

## SDK:er som ersätts av Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ersätter följande SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Detta är inte bara en wrapper runt befintliga bibliotek. Det är en fullständig omskrivning. Syftet är att klara utmaningar med taggar som aktiveras i rätt ordning, inkonsekvens med versionsproblem i biblioteket och bättre beroendehantering. Det är ett nytt sätt att implementera Experience Cloud.

Förutom ett nytt bibliotek finns det en ny slutpunkt som effektiviserar HTTP-begäranden till Adobes lösningar. Tidigare skickade Visitor.js ett blockerande anrop till besökar-ID-tjänsten och AT.js skickade ett anrop till Adobe Target, DIL.js skickade ett anrop till Adobe Audience Manager och slutligen skickade AppMeasurement.js ett anrop till Adobe Analytics. Det nya biblioteket och slutpunkten kan hämta ett ID, hämta en Target-upplevelse, skicka data till Audience Manager och skicka data till Adobe Experience Platform i ett enda samtal.