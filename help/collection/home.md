---
solution: Experience Platform
title: Översikt över datainsamling
description: Lär dig skicka data till Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Översikt över datainsamling

Adobe Experience Platform har en programsvit som gör att ni kan samla in kundupplevelsedata från olika källor och skicka dem till Adobe Experience Platform Edge Network. Dessa data kan sedan berikas, omformas och distribueras till Adobe eller andra mål än Adobe.

Adobe har stöd för följande kodspråk med dedikerade bibliotek för datainsamling:

* **JavaScript**: För webbplatser och webbaserade program
* **Kotlin**: För Android-enheter
* **Dra**: För iOS-enheter
* **BrightStorScript**: För Roku-enheter
* **Flutter**: För Android + iOS-program som använder Flutter
* **React Native**: För Android + iOS-program som använder React Native

Tagggränssnittet i Adobe Experience Platform Data Collection innehåller tilläggen Web SDK och Mobile SDK.

Om ingen av de ovan nämnda SDK:erna uppfyller ditt projekts behov kan du använda [Adobe Experience Platform Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) för att skicka data direkt till Adobe.

## Datainsamlingsprocess

I stället för att installera och implementera separata individuella bibliotek för varje Adobe-produkt kan du implementera en av SDK:erna ovan eller taggtillägg för att samla alla önskade data i en enda nyttolast. Nyttolasten skickas till en [datastream](/help/datastreams/overview.md) i Adobe Experience Platform Edge Network.

![Datainsamlingsdiagram](assets/tags-sdks.png)

Adobe Experience Platform Edge Network är ett globalt, snabbt och tillförlitligt nätverk av servrar som kan ta emot och bearbeta data i otrolig skala. När en datastream tar emot data distribueras dessa data till varje lösning som du har konfigurerat. Data skickas vidare i ett format som alla enskilda produkter förstår.

![Adobe-lösningsdiagram](assets/adobe-solutions.png)

Du kan också använda [händelsevidarebefordran](/help/tags/ui/event-forwarding/overview.md) för att omvandla, förbättra och skicka data till andra mål än Adobe med låg fördröjning och utan implementeringskod på klientsidan.

![Diagram för vidarebefordran av händelser](assets/event-forwarding.png)
