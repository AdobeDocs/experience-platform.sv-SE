---
title: Hjälp om Adobe Experience Platform Web SDK
seo-title: Hjälp om Adobe Experience Platform Web SDK
description: Lär dig vad Adobe Experience Platform Web SDK är och hur det kan användas.
seo-description: låta Adobe Experience Cloud kunder interagera med de olika tjänsterna i Experience Cloud.
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Vad är Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud kunder kan interagera med de olika tjänsterna i [!DNL Experience Cloud] Adobe [!DNL Experience Platform Edge Network].

I följande video visas en översikt över Adobe Experience Platform [!DNL Web SDK] och [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK:er som ersatts av Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ersätter följande SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Detta är inte bara en wrapper runt befintliga bibliotek. Det är en fullständig omskrivning. Syftet är att klara utmaningar med taggar som måste aktiveras i rätt ordning, inkonsekvens med versionsproblem i biblioteket och bättre beroendehantering. Det är ett nytt sätt att implementera [!DNL Experience Cloud] och det är en [öppen källkod](https://github.com/adobe/alloy).

Förutom ett nytt bibliotek finns det en ny slutpunkt som effektiviserar HTTP-begäranden till Adobe-lösningar. Tidigare skickade Visitor.js ett blockerande anrop till besökar-ID-tjänsten och AT.js skickade ett anrop till Adobe Target, DIL.js skickade ett anrop till Adobe Audience Manager och slutligen AppMeasurement.js skickade ett anrop till Adobe Analytics. Det nya biblioteket och slutpunkten kan hämta ett ID, hämta en [!DNL Target] upplevelse, skicka data till [!DNL Audience Manager]och skicka data till Adobe Experience Platform i ett enda anrop.

I följande video visas Adobe Experience Platform [!DNL Web SDK] och [!DNL Edge Network] in action. I videoexemplet används ett enda anrop till Adobe som skickar data till [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]och [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)


## Komma igång

Vi rekommenderar att du [tittar i vår guide](getting-started/quick-start-with-launch.md) om hur du kommer igång med Adobe Launch.

Produkten utvecklas ständigt och växer för att klara fler och fler användningsfall. Ta en titt på vår [fallpanel](https://github.com/adobe/alloy/projects/5)för att hålla dig à jour med det senaste. Vi håller detta uppdaterat med de användningsfall som vi för närvarande stöder och de som vi arbetar med för att du ska kunna fatta bästa möjliga beslut.

* __Använd ärenden som ännu inte stöds__ - Det här är exempel som finns på vår färdplan och som kan stödjas i framtiden.
* __Pågående__ användningsfall - Det här är de användningsfall som teamet arbetar med att slutföra för publicering.
* __Användningsexempel__ som stöds - Det här är de användningsområden som stöds och fungerar idag.
* __Användningsfall som vi inte stöder__ - Det här är användningsfall som vi har beslutat att inte stödja.
