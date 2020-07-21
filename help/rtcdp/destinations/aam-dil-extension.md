---
title: Audience Manager DIL-tillägg
seo-title: Audience Manager DIL-tillägg
description: Tillägget Audience Manager DIL är ett mål för Data Management Platform (DMP) i Adobe Real-time Customer Data Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Tillägget Audience Manager DIL är ett mål för Data Management Platform (DMP) i Adobe Real-time Customer Data Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 5%

---


# Audience Manager DIL-tillägg {#aam-dil-extension}

## Översikt {#overview}

Detta är tillägget Adobe Audience Manager Data Integration Library (implementering på klientsidan). Obs! Det här tillägget är inte avsett att användas för vidarebefordran av Adobe Analytics-data på serversidan. För SSF använder du Adobe Analytics-tillägget. Viktigt: Från och med version 8.0 är DIL beroende av [!DNL Experience Cloud] ID-tjänsten, version 3.3 eller senare. Implementera både [!DNL Experience Cloud] ID-tjänsten och DIL för fullständig [!DNL Audience Manager] dataintegrering.

[!DNL Audience Manager] DIL är ett tillägg till Platform (DMP) för datahantering i Adobe Customer Data Platform i realtid. Mer information om tilläggsfunktionen finns på [Audience Manager-tilläggssidan](https://docs.adobe.com/content/help/sv-SE/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) i dokumentationen för Experience Platform Launch.

Det här målet är ett [!DNL Experience Platform Launch] tillägg. Mer information om hur Launch-tillägg fungerar i Adobe CDP i realtid finns i Översikt över [](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch-tillägg.

![Audience Manager DIL-tillägg](/help/rtcdp/destinations/assets/aam-dil-extension.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] katalogen för alla kunder som har köpt Adobe CDP i realtid.

Om du vill använda det här tillägget måste du ha tillgång till [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till [!DNL Launch] och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du [!DNL Audience Manager] DIL-tillägget:

1. Gå till [Adobe Real-time CDP-gränssnittet](http://platform.adobe.com/)**[!UICONTROL Destinations > Catalog]**.
2. Välj tillägget i katalogen eller använd sökfältet.
3. Klicka på målet för att markera det och välj sedan **[!UICONTROL Install Extension]** i den högra listen. Om **[!UICONTROL Install Extension]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).
4. I **[!UICONTROL Select available Launch property]** fönstret väljer du den [!DNL Launch] egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i Launch. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i [!DNL Launch] dokumentationen.
5. Arbetsflödet tar dig [!DNL Launch] till att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på [Audience Manager-tilläggssidan](https://docs.adobe.com/content/help/sv-SE/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) i [!DNL Experience Launch] dokumentationen.

Du kan också installera tillägget direkt i [Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägga till ett nytt tillägg](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) i [!DNL Launch] dokumentationen.


## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i [!DNL Launch].

I [!DNL Launch]kan du konfigurera regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i [Regeldokumentation](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i [!DNL Launch] gränssnittet.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande användargränssnittet för CDP i realtid **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [installationstillägget](#install-extension) för att komma åt [!DNL Launch] och konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i [!DNL Launch] dokumentationen.



