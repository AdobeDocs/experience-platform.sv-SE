---
keywords: Awin Advertiser mastertag extension;mastertag tag;Awin;awin;AWIN
title: Awin Advertiser Mastertag-tillägg
seo-title: Awin Advertiser Mastertag-tillägg
description: Awin Advertiser Mastertag-tillägget är en annonsdestination i Adobe Customer Data Platform i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Awin Advertiser Mastertag-tillägget är en annonsdestination i Adobe Customer Data Platform i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 164c51e543d5eba11e4756723f3fecd84ec48f59
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 2%

---


# [!DNL Awin Advertiser Mastertag] extension {#awin-mastertag-extension}

## Översikt {#overview}

Detta [!DNL MasterTag] är ett JavaScript-bibliotek som innehåller alla funktioner som krävs för Awin-spårningslösningen och som ska läggas till ovillkorligt på varje sida på webbplatsen, inklusive bekräftelsesidan, men inte någon sida som visar eller bearbetar betalningsinformation.

[!DNL Awin Advertiser Mastertag] är en annonsutökning i kunddataplattformen Adobe i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Det här målet är ett [!DNL Experience Platform Launch] tillägg. Mer information om hur Launch-tillägg fungerar i CDP i realtid i Adobe finns i Översikt över [](/help/rtcdp/destinations/experience-platform-launch-extensions.md)tillägg i Experience Platform Launch.

![Awin Advertiser Mastertag-tillägg i användargränssnittet](/help/rtcdp/destinations/assets/awin-mastertag-extension.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] katalogen för alla kunder som har köpt CDP i realtid i Adobe.

Om du vill använda det här tillägget måste du ha tillgång till [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till [!DNL Launch] och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du [!DNL Awin Advertiser Mastertag] tillägget:

1. I CDP-gränssnittet [för](http://platform.adobe.com/)Adobe i realtid går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Välj tillägget i katalogen eller använd sökfältet.
3. Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om **[!UICONTROL Configure]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).
4. I **[!UICONTROL Select available Launch property]** fönstret väljer du den [!DNL Launch] egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i [!DNL Launch] dokumentationen.
5. Arbetsflödet tar dig [!DNL Launch] till att slutföra installationen.

Mer information om alternativ för tilläggskonfiguration och installationsstöd finns på sidan [Awin Advertiser Mastertag på Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

Du kan också installera tillägget direkt i [Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägga till ett nytt tillägg](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) i [!DNL Launch] dokumentationen.


## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i [!DNL Launch].

I [!DNL Launch]kan du konfigurera regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i [Regeldokumentation](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i [!DNL Launch] gränssnittet.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande CDP-gränssnittet för tillägget i realtid i Adobe **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [installationstillägget](#install-extension) för att komma åt [!DNL Launch] och konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i [!DNL Launch] dokumentationen.
