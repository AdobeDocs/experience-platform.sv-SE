---
Keywords: ECID;ecid
title: Experience Cloud ID-tjänsttillägg
seo-title: Experience Cloud ID-tjänsttillägg
description: Tillägget Experience Cloud ID Service är ett personaliseringsmål i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Tillägget Experience Cloud ID Service är ett personaliseringsmål i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 2%

---


# [!DNL Experience Cloud] ID-tjänsttillägg {#adobe-ecid-extension}

## Översikt {#overview}

Det här tillägget implementerar [!DNL Experience Cloud] ID-tjänsten, som identifierar besökare över alla [!DNL Experience Cloud] lösningar.

[!DNL Experience Cloud] ID-tjänsten är ett personaliseringstillägg i kunddataplattformen i realtid. Mer information om tilläggsfunktioner finns på [Experience Cloud ID-tjänsttilläggets sida](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html) i [!DNL Experience Platform Launch] dokumentationen.

Det här målet är ett [!DNL Adobe Experience Platform Launch] tillägg. Mer information om hur [!DNL Platform Launch] tillägg fungerar i CDP i realtid i Adobe finns i Översikt över [tillägg i](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Adobe ECID-tillägg](/help/rtcdp/destinations/assets/adobe-ecid-extension.png)


## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt CDP i realtid i Adobe.

Om du vill använda det här tillägget måste du ha tillgång till [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till [!DNL Launch] och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du [!DNL Experience Cloud] ID-tjänsttillägget:

1. I CDP-gränssnittet [för](http://platform.adobe.com/)Adobe i realtid går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Välj tillägget i katalogen eller använd sökfältet.
3. Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om **[!UICONTROL Configure]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).
4. I **[!UICONTROL Select available Platform Launch property]** fönstret väljer du den [!DNL Platform Launch] egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Platform Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i [!DNL Launch] dokumentationen.
5. Arbetsflödet tar dig [!DNL Platform Launch] till att slutföra installationen.

Mer information om alternativ för tilläggskonfiguration och installationssupport finns på sidan [med](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html) Experience Cloud ID-tjänsttillägg i [!DNL Experience Launch] dokumentationen.

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