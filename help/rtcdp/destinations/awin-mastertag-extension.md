---
title: Awin Advertiser Mastertag-tillägg
seo-title: Awin Advertiser Mastertag-tillägg
description: Awin Advertiser Mastertag-tillägget är en annonsdestination i Adobes kunddataplattform i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: null
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# Awin Advertiser Mastertag-tillägg {#awin-mastertag-extension}

## Översikt {#overview}

MasterTag är ett JavaScript-bibliotek som innehåller alla funktioner som krävs för Awin-spårningslösningen och ska bifogas villkorslöst till alla sidor på webbplatsen, inklusive bekräftelsesidan, men exklusive alla sidor som visar eller bearbetar betalningsinformation.

Awin Advertiser Mastertag är ett reklamtillägg i Adobes kunddataplattform i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Det här målet är ett Experience Platform Launch-tillägg. Mer information om hur Launch-tillägg fungerar i Adobe CDP i realtid finns i Översikt över [Experience Platform Launch-tillägg](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Awin Advertiser Mastertag-tillägg i användargränssnittet](/help/rtcdp/destinations/assets/awin-mastertag-extension.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt Adobe CDP i realtid.

Om du vill använda det här tillägget måste du ha tillgång till Experience Platform Launch. Experience Platform Launch erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till Launch och be dem att ge dig behörighet att installera tillägg så att du kan installera dem **[!UICONTROL manage_properties]** .

## Installera tillägg {#install-extension}

Så här installerar du Awin Advertiser Mastertag-tillägget:

1. Gå till [Adobe Real-time CDP-gränssnittet](http://platform.adobe.com/)**[!UICONTROL Destinations > Catalog]**.
2. Välj tillägget i katalogen eller använd sökfältet.
3. Klicka på målet för att markera det och välj sedan **[!UICONTROL Install Extension]** i den högra listen. Om **[!UICONTROL Install Extension]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).
4. I **[!UICONTROL Select available Launch property]** fönstret väljer du den Launch-egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i Launch. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i delen [](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i Launch-dokumentationen.
5. Arbetsflödet tar dig till Launch för att slutföra installationen.

Information om alternativen för tilläggskonfiguration och installationsstöd finns på sidan [Awin Advertiser Mastertag på Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

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
