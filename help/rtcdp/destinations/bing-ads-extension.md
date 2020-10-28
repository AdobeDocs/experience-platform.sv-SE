---
keywords: bing;bing ads event tracking;event tracking bing;UET;UET extension
title: Bing Ads UET-tillägg (Universal Event Tracking)
seo-title: Bing Ads UET-tillägg (Universal Event Tracking)
description: Tillägget Bing Ads Universal Event Tracking (UET) är en annonsdestination i Adobe Customer Data Platform i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Tillägget Bing Ads Universal Event Tracking (UET) är en annonsdestination i Adobe Customer Data Platform i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: d9bf874dbfcc00c0a6e267f1a2e96f1223054825
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---


# [!DNL Bing Ads Universal Event Tracking] (UET)-tillägg {#bing-ads-extension}

## Översikt {#overview}

[!DNL Bing Ads Universal Event Tracking] (UET) för [!DNL Experience Platform Launch] är ett användbart sätt att spåra vad som händer efter att någon har klickat på din sökannons. Genom att använda en enda UET-tagg för att registrera vad kunderna gör på er webbplats kan ni utnyttja dessa data och spåra konverteringar eller målgrupper med hjälp av återmarknadsföringslistor.

[!DNL Bing Ads Universal Event Tracking] (UET) är ett annonstillägg i Adobe Customer Data Platform i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Det här målet är ett [!DNL Adobe Experience Platform Launch] tillägg. Mer information om hur [!DNL Platform Launch] tillägg fungerar i CDP i realtid i Adobe finns i Översikt över [tillägg i](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Bing Ads-tillägg](assets/bing-ads-extension.png)


## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] katalogen för alla kunder som har köpt CDP i realtid i Adobe.

Om du vill använda det här tillägget måste du ha tillgång till [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till [!DNL Platform Launch] och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du [!DNL Bing Ads Universal Event Tracking] (UET)-tillägget:

1. I CDP-gränssnittet [för](http://platform.adobe.com/)Adobe i realtid går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Välj tillägget i katalogen eller använd sökfältet.
3. Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om **[!UICONTROL Configure]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).
4. I **[!UICONTROL Select available Platform Launch property]** fönstret väljer du den [!DNL Platform Launch] egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Platform Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i [!DNL Launch] dokumentationen.
5. Arbetsflödet tar dig [!DNL Platform Launch] till att slutföra installationen.

Mer information om alternativ för tilläggskonfigurering och installationsstöd finns på sidan [Bing Ads Universal Event Tracking (UET) på Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägga till ett nytt tillägg](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) i [!DNL Platform Launch] dokumentationen.


## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i [!DNL Platform Launch].

I [!DNL Platform Launch]kan du konfigurera regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i [Regeldokumentation](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i [!DNL Platform Launch] gränssnittet.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande CDP-gränssnittet för tillägget i realtid i Adobe **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [installationstillägget](#install-extension) för att komma åt [!DNL Platform Launch] och konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i [!DNL Platform Launch] dokumentationen.
