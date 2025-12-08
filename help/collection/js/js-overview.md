---
title: Web SDK JavaScript Library overview
description: Skicka data till Adobe Experience Platform Edge Network med JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Web SDK JavaScript Library overview

**Adobe Experience Platform Web SDK** är ett JavaScript-bibliotek på klientsidan som gör att du kan skicka data till Adobe Experience Platform Edge Network. Den här guiden dokumenterar implementeringssökvägen för Web SDK JavaScript-biblioteket (`alloy.js`), inklusive viktiga begrepp, installation, konfiguration och kommandon. Webbtaggtillägget SDK i användargränssnittet för datainsamling finns i [webbtaggtillägget för SDK](/help/tags/extensions/client/web-sdk/overview.md).

SDK på webben skickar data på ett lösningsagnostiskt sätt (XDM) till Experience Platform Edge Network, som sedan mappar data till lösningsspecifika format och destinationer och skickar dem i realtid.

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network erbjuder datainsamling med låg fördröjning, anslutningsbar datoranvändning och snabb dataaktivering i alla adresserbara kanaler. Det erbjuder en enda konsoliderad SDK för webben, mobiler och kanaler på serversidan, som skickar data till en gemensam Adobe-domän (`adobedc.net`) och tar emot en enda nyttolast för data- och upplevelseleverans.

På serversidan förenklar en enhetlig edge-gateway och ett gemensamt plattformstjänstramverk driftsättningen av nya funktioner samtidigt som den ger följande fördelar:

* Minska kundens tid till värde,
* behovet av punktintegreringar upphör,
* Förbättra prestanda jämfört med de gamla biblioteken.
* Minskade driftskostnader.
* Ökad innovationshastighet.
* Skapa konkurrensfördelar för Adobe-kunder.

Med ett konsoliderat edge-system kan ni hantera annonserings-, marknadsförings- och personaliseringskampanjer i alla kanaler. Det minskar den totala ägandekostnaden och stöder olika datatyper, vilket gör att du kan mappa din datamodell för användning med flera Experience Cloud-produkter.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotek som ersätts av Web SDK {#sdks}

Web SDK är ett bibliotek med öppen källkod som byggts från grunden och som integrerar funktioner i befintliga bibliotek. Här behandlas problem med taggutlösning, inkonsekvenser i versionerna och beroendehantering, som erbjuder ett sätt att implementera många Experience Cloud-produkter. Web SDK ersätter datainsamling för följande tjänster:

* Adobe Experience Platform Visitor ID-tjänst (`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`)
* Adobe Target (`AT.js`)
* Adobe Audience Manager (`DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

Det introducerar också en ny slutpunkt som effektiviserar HTTP-begäranden till Adobe-lösningar. Tidigare krävdes flera anrop för varje datainsamlingsbibliotek. Nu kan ett enskilt anrop hämta ett ID, hämta en [!DNL Target]-upplevelse, skicka data till [!DNL Audience Manager] och skicka data till Adobe Experience Platform.

## Migrera från befintliga bibliotek till Web SDK {#migrating-to-web-sdk}

Adobe har ett smidigt uppgraderingsalternativ som förenklar migreringen från alla befintliga bibliotek till Web SDK. Du kan migrera varje sida på webbplatsen separat utan att behöva migrera hela webbplatsen samtidigt. Du kan använda Web SDK på vissa sidor medan befintliga bibliotek finns kvar på andra, vilket ger en gradvis övergång.
