---
title: Tolka.ly Analytics-tillägg
seo-title: Tolka.ly Analytics-tillägg
description: The Parse.ly Analytics är ett analysmål i Adobe Real-time Customer Data Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Tillägget Parse.ly Analytics är ett analysmål i Adobe Real-time Customer Data Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# [!DNL Parse.ly Analytics] Tillägg {#parsely-analytics-extension}

## Översikt {#overview}

[!DNL Parse.ly Analytics] hjälper över 2 500 företag att använda data för att förstå sin onlinepublik. Det här tillägget installerar ett JavaScript-fragment som spårar hur besökare interagerar med innehåll på platsen.

Parse.ly är ett analystillägg i Adobe Real-time Customer Data Platform. Mer information om tilläggsfunktioner finns i [Parse.ly Analytics](https://www.parse.ly/).

Det här målet har tillägget Experience Platform Launch. Mer information om hur Launch-tillägg fungerar i Adobe CDP i realtid finns i Översikt över [](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch-tillägg.

![Tolka.ly Analytics Extension](assets/parsely-extension.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] katalogen för alla kunder som har köpt Adobe CDP i realtid.

Om du vill använda det här tillägget måste du ha tillgång till Experience Platform Launch. Experience Platform Launch erbjuds Adobe Experience Cloud-kunder som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till Launch och be dem att ge dig behörighet att installera tillägg så att du kan installera dem **[!UICONTROL manage_properties]** .

## Installera tillägg {#install-extension}

Så här installerar du [!DNL Parse.ly] tillägget:

1. Gå till [Adobe Real-time CDP-gränssnittet](http://platform.adobe.com/)**[!UICONTROL Destinations > Catalog]**.
2. Välj tillägget i katalogen eller använd sökfältet.
3. Klicka på målet för att markera det och välj sedan **[!UICONTROL Install Extension]** i den högra listen. Om **[!UICONTROL Install Extension]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).
4. I **[!UICONTROL Select available Launch property]** fönstret väljer du den Launch-egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i Launch. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i delen [](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i Launch-dokumentationen.
5. Arbetsflödet tar dig till Launch för att slutföra installationen.

Du kan också installera tillägget direkt i [Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägga till ett nytt tillägg](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) i Launch-dokumentationen.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i Launch.

I Launch kan du konfigurera regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i [Regeldokumentation](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i startgränssnittet.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande användargränssnittet för CDP i realtid **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [installationstillägget](#install-extension) för att komma åt Starta och konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i Launch-dokumentationen.