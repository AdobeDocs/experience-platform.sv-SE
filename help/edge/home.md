---
title: Hjälp för Adobe Experience Platform Web SDK
seo-title: Hjälp för Adobe Experience Platform Web SDK
description: Lär dig vad Adobe Experience Platform Web SDK är och hur det kan användas.
seo-description: gör det möjligt för kunder med Adobe Experience Cloud att interagera med de olika tjänsterna i Experience Cloud.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Vad är Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att kunder i Adobe Experience Cloud kan interagera med de olika tjänsterna i Experience Cloud via Adobe Experience Platform Edge Network.

## SDK:er som ersätts av Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ersätter följande SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Detta är inte bara en wrapper runt befintliga bibliotek. Det är en fullständig omskrivning. Syftet är att klara utmaningar med taggar som aktiveras i rätt ordning, inkonsekvens med versionsproblem i biblioteket och bättre beroendehantering. Det är ett nytt sätt att implementera Experience Cloud och det är [öppen källkod](https://github.com/adobe/alloy)

Förutom ett nytt bibliotek finns det en ny slutpunkt som effektiviserar HTTP-begäranden till Adobes lösningar. Tidigare skickade Visitor.js ett blockerande anrop till besökar-ID-tjänsten och AT.js skickade ett anrop till Adobe Target, DIL.js skickade ett anrop till Adobe Audience Manager och slutligen skickade AppMeasurement.js ett anrop till Adobe Analytics. Det nya biblioteket och slutpunkten kan hämta ett ID, hämta en Target-upplevelse, skicka data till Audience Manager och skicka data till Adobe Experience Platform i ett enda samtal.

## Komma igång

Vi rekommenderar att du [tar en titt på vår guide](getting-started/quick-start-with-launch.md) om hur du kommer igång snabbt.

Produkten utvecklas ständigt och växer för att klara fler och fler användningsfall. För att hålla dig à jour med det senaste kan vi ta en titt på vår [fallpanel](https://github.com/adobe/alloy/projects/5). Vi håller detta uppdaterat med de användningsfall som vi för närvarande stöder och de som vi arbetar på för att du ska kunna fatta bästa möjliga beslut.

* __Använd fall som ännu inte stöds__ - är exempel på fall som ligger på vår färdplan och som ska utföras i framtiden.
* __Pågående__ användningsfall - Det här är de användningsfall som teamet arbetar med att slutföra för publicering.
* __Användningsexempel__ som stöds - Det här är de användningsområden som stöds och fungerar idag.
* __Användningsfall som vi inte stöder__ - Det här är användningsfall som vi har beslutat att inte stödja.
