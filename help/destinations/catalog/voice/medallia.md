---
keywords: Medallia;media
title: Medietillägg
seo-title: Medietillägg
description: Medietillägget är en röst för kundens destination i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Medietillägget är en röst för kundens destination i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# [!DNL Medallia] Tillägg  {#medallia-extension}

## Översikt {#overview}

Distribuera [!DNL Medallia] snabbt och smidigt på dina webbegenskaper. Tillägget gör det även möjligt att identifiera enkäthändelser, samla in kundfeedback i realtid via dataelement, använda det i regler för att personalisera kundupplevelsen och dela data med Adobe Analytics.

[!DNL Medallia] är en röst för kundens programtillägg i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103279.medallia-for-adobe-launch.html).

Det här målet är ett Adobe Experience Platform Launch-tillägg. Mer information om hur plattformsstartstillägg fungerar i Platform finns i [Översikt över Adobe Experience Platform Launch-tillägg](../launch-extensions/overview.md).

![Media Extension](../../assets/catalog/voice/medallia/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations]-katalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha tillgång till Adobe Experience Platform Launch. Platform Launch erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till Platform Launch och be dem att ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget [!DNL Medallia]:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [plattformsgränssnittet](http://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Förutsättningar](#prerequisites).

I **[!UICONTROL Select available Platform Launch property]**-fönstret väljer du den plattformsstartegenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i Platform Launch. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i [egenskapssidans avsnitt](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) i dokumentationen för Platform Launch.

Arbetsflödet tar dig till Platform Launch för att slutföra installationen.

Information om alternativ för tilläggskonfiguration och installationsstöd finns på sidan [Media på Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103279.medallia-for-adobe-launch.html).

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägg till ett nytt tillägg](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) i dokumentationen för plattformsstart.

## Använda tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i Platform Launch.

I Platform Launch kan du konfigurera regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för tillägg finns i [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i plattformens startgränssnitt.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande **[!UICONTROL Install]** som plattformsgränssnitt för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att komma till plattformsstart och konfigurera eller ta bort tillägget.

Mer information om hur du uppgraderar tillägget finns i [Tilläggsuppgradering](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i dokumentationen för Platform Launch.