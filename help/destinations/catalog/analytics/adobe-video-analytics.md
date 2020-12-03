---
keywords: media analytics extension;media analytics;audio and video extension
title: Adobe Media Analytics för ljud- och videotillägg
seo-title: Adobe Media Analytics för ljud- och videotillägg
description: Tillägget Adobe Media Analytics för ljud och video är ett analysmål i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Adobe Media Analytics for Video-tillägget är ett analysmål i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# Adobe Media Analytics for Audio and Video Extension {#adobe-analytics-for-video-extension}

## Översikt {#overview}

Adobe Media Analytics for Audio and Video är ett tillägg till basanalysverktyget som ger kunderna robusta mått för video, ljud och annonser.

Adobe Media Analytics for Audio and Video är ett analystillägg i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100157.html).

Det här målet är ett [!DNL Adobe Experience Platform Launch] tillägg. Mer information om hur [!DNL Platform Launch] tillägg fungerar i CDP i realtid finns i Översikt över [tillägg i](../launch-extensions/overview.md)Experience Platform Launch.

![Adobe Media Analytics för ljud- och videotillägg](../../assets/catalog/analytics/adobe-video-analytics/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] katalogen för alla kunder som har köpt CDP i realtid.

Om du vill använda det här tillägget måste du ha tillgång till [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till [!DNL Platform Launch] och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget Adobe Analytics for Video:

I CDP-gränssnittet [i](http://platform.adobe.com/)realtid går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om **[!UICONTROL Configure]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).

I **[!UICONTROL Select available Platform Launch property]** fönstret väljer du den [!DNL Platform Launch] egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Platform Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i [!DNL Launch] dokumentationen.

Arbetsflödet tar dig [!DNL Platform Launch] till att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på [Adobe Media Analytics for Audio and Video Extension page](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html) i [!DNL Experience Launch] dokumentationen.

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägga till ett nytt tillägg](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) i [!DNL Platform Launch] dokumentationen.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i [!DNL Platform Launch].

I [!DNL Platform Launch]kan du konfigurera regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i [!DNL Platform Launch] gränssnittet.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande CDP-gränssnittet i realtid **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [installationstillägget](#install-extension) för att komma åt [!DNL Platform Launch] och konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i [!DNL Platform Launch] dokumentationen.



