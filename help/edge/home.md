---
title: Adobe Experience Platform Web SDK - översikt
description: Lär dig hur du använder Adobe Experience Platform Web SDK för att integrera plattformsfunktioner på din webbplats.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7607f01109de1f6207f2e910a8620698c60b89d4
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK - översikt

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud kunder kan interagera med de olika tjänsterna i [!DNL Experience Cloud] via Adobe Experience Platform Edge Network. Förutom JavaScript-biblioteket finns det ett [Experience Platform Launch-tillägg](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) som kan hjälpa dig med dina Web SDK-konfigurationer.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] är en del av den samling som utgör Experience Edge. Experience Edge består av tre tekniker:

* **[!DNL Adobe Experience Platform Web SDK]:** Ett JavaScript SDK och  [!DNL Experience Platform Launch] tillägg som dramatiskt förenklar driftsättningen av  [!DNL Adobe] tekniker
* **Adobe Experience Platform Mobile SDK:** Ett tillägg till v5 Mobile SDK så att kunderna kan använda den nya distributionsmetoden
* **[!DNL Adobe Experience Platform Edge Network]:** Ett globalt distribuerat nätverk med servrar som möjliggör en ny metod för att distribuera  [!DNL Adobe] produkter

[!DNL Adobe Experience Edge] är ett nytt ramverk för datainsamling med låg fördröjning, anslutningsbar datoranvändning och snabb dataaktivering i alla adresserbara kanaler.

[!DNL Adobe Experience Edge] tillhandahåller en enda konsoliderad SDK för alla kanaler (JavaScript, Mobile, Server-side), som skickar data till en gemensam Adobe-domän (`adobedc.net`) och tar emot en enda nyttolast för data- och upplevelseleverans.

På serversidan gör en enhetlig edge-gateway och ett gemensamt ramverk för plattformstjänster det enkelt att plugin och driftsätta nya funktioner i den här realtidsmiljön.  Arkitekturen:

* Minskar kundens tid till värde
* Ändrar behovet av punktintegreringar
* Förbättrar prestanda jämfört med gamla bibliotek
* Minskar kostnaderna
* Ökar innovationshastigheten
* Skapar hållbara konkurrensfördelar för Adobe-kunder

Med ett enda konsoliderat edge-system kan kunderna hantera sina annonserings-, marknadsförings- eller personaliseringskampanjer i alla kanaler som en integrerad upplevelse.  [!DNL Adobe] ger möjlighet att leverera tjänster med lägre total ägandekostnad för kunderna.  Det bidrar också till att öka produktutvecklingshastigheten genom att göra realtidskanten pluggbar så att [!DNL Adobe] och dess kunder snabbare kan lägga till nya funktioner och kunddefinierad logik i realtidssystemet.

## Videoöversikt

I följande video visas en översikt över Adobe Experience Platform [!DNL Web SDK] och Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK:er som ersatts av Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ersätter följande SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Detta är inte bara en wrapper runt befintliga bibliotek. Det är en fullständig omskrivning. Syftet är att klara utmaningar med taggar som måste aktiveras i rätt ordning, inkonsekvens med versionsproblem i biblioteket och bättre beroendehantering. Det är ett nytt sätt att implementera [!DNL Experience Cloud] och det är [öppen källkod](https://github.com/adobe/alloy).

Förutom ett nytt bibliotek finns det en ny slutpunkt som effektiviserar HTTP-begäranden till Adobe-lösningar. Tidigare skickade Visitor.js ett blockerande anrop till besökar-ID-tjänsten och AT.js skickade ett anrop till Adobe Target, DIL.js skickade ett anrop till Adobe Audience Manager och slutligen AppMeasurement.js skickade ett anrop till Adobe Analytics. Det nya biblioteket och slutpunkten kan hämta ett ID, hämta en [!DNL Target]-upplevelse, skicka data till [!DNL Audience Manager] och skicka data till Adobe Experience Platform i ett enda anrop.

I följande video visas Adobe Experience Platform [!DNL Web SDK] och Adobe Experience Platform [!DNL Edge Network] in action. I videoexemplet används ett enda anrop till Adobe som skickar data till [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] och [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Produkten utvecklas ständigt och växer för att klara fler och fler användningsfall. Se sidan [Användningsexempel som stöds](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html) om du vill hålla dig uppdaterad. På den här sidan listas de användningsfall som vi för närvarande stöder, med länkar till mer information om sådana finns.

* **Använd ärenden som ännu inte stöds:** Det här är exempel som finns på vår färdplan och som ska stödjas i framtiden.
* **Pågående användningsfall:** Detta är de användningsfall som teamet arbetar med att slutföra för lansering.
* **Användningsexempel som stöds:** Det här är de användningsområden som stöds och som fungerar idag.
* **Användningsfall som vi inte stöder:** Det här är användningsfall som vi har beslutat att inte stödja.
