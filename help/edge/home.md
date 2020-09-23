---
title: Adobe Experience Platform Web SDK - hjälp
seo-title: Adobe Experience Platform Web SDK - hjälp
description: Lär dig vad Adobe Experience Platform Web SDK är och hur det kan användas.
seo-description: låta Adobe Experience Cloud kunder interagera med de olika tjänsterna i Experience Cloud.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Vad är Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud kunder kan interagera med de olika tjänsterna i [!DNL Experience Cloud] Adobe [!DNL Experience Platform Edge Network]. Förutom JavaScript-biblioteket finns det ett [Launch-tillägg](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) som kan hjälpa dig med dina Web SDK-konfigurationer.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] är en del av den samling som utgör Experience Edge. Experience Edge består av tre tekniker:

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript SDK och [!DNL Launch] tillägg som dramatiskt förenklar driftsättningen av [!DNL Adobe] tekniker
* **Adobe Experience Platform Mobile SDK:** Ett tillägg till v5 Mobile SDK så att kunderna kan använda den nya distributionsmetoden
* **[!DNL Adobe Experience Platform Edge Network]:** Ett globalt distribuerat servernätverk som möjliggör en ny metod för att distribuera [!DNL Adobe] produkter

Det [!DNL Adobe Experience Edge] är ett nytt ramverk för datainsamling med låg fördröjning, anslutningsbar datoranvändning och snabb dataaktivering i alla adresserbara kanaler.

[!DNL Adobe Experience Edge] tillhandahåller en enda konsoliderad SDK för alla kanaler (JavaScript, Mobile, Server-side), som skickar data till en gemensam Adobe-domän (`adobedc.net`) och tar emot en enda nyttolast för data- och upplevelseleverans.

På serversidan gör en enhetlig edge-gateway och ett gemensamt ramverk för plattformstjänster det enkelt att plugin och driftsätta nya funktioner i den här realtidsmiljön.  Arkitekturen:

* Minskar kundens tid till värde
* Ändrar behovet av punktintegreringar
* Förbättrar prestanda jämfört med gamla bibliotek
* Minskar kostnaderna
* Ökar innovationshastigheten
* Skapar hållbara konkurrensfördelar för Adobe-kunder

Med ett enda konsoliderat edge-system kan kunderna hantera sina annonserings-, marknadsförings- eller personaliseringskampanjer i alla kanaler som en integrerad upplevelse.  Det gör det möjligt [!DNL Adobe] att leverera tjänster med lägre total ägandekostnad för kunderna.  Det bidrar också till att öka produktutvecklingshastigheten genom att göra realtidskanten pluggbar så att [!DNL Adobe] och kunderna snabbare kan lägga till nya funktioner och kunddefinierad logik i realtidssystemet.

## Videoöversikt

I följande videofilm visas en översikt över Adobe Experience Platform [!DNL Web SDK] och [!DNL Edge Network].

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

* **Användningsfall som ännu inte stöds:** Det här är användningsfall som ligger på vår färdplan och som ska stödjas i framtiden.
* **Pågående användningsfall:** Det här är de användningsområden som teamet arbetar med att slutföra för lansering.
* **Användningsexempel:** Det här är de användningsområden som stöds och som fungerar idag.
* **Användningsfall som vi inte stöder:** Vi har fattat ett beslut om att inte ge stöd.
