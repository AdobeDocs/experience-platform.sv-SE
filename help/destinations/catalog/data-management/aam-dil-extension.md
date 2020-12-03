---
keywords: Audience Manager DIL extension;destination audience manager;dil extension
title: Audience Manager DIL utökningen
seo-title: Audience Manager DIL utökningen
description: Tillägget Audience Manager DIL är en DMP-destination (Data Management Platform) i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Tillägget Audience Manager DIL är en DMP-destination (Data Management Platform) i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Audience Manager DIL utökningen {#aam-dil-extension}

## Översikt {#overview}

Det här är Adobe Audience Manager Data Integration Library-tillägget (implementering på klientsidan). Obs! Det här tillägget är inte avsett att användas för vidarebefordran av Adobe Analytics-data på serversidan. För SSF använder du Adobe Analytics-tillägget. Viktigt: Från och med version 8.0 är DIL beroende av [!DNL Experience Cloud] ID-tjänsten, version 3.3 eller senare. Implementera både [!DNL Experience Cloud] ID-tjänsten och DIL för att få fullständig [!DNL Audience Manager] dataintegrering.

[!DNL Audience Manager] DIL är ett DMP-tillägg (Data Management Platform) i kunddataplattformen i realtid. Mer information om tilläggsfunktionen finns på [Audience Manager-tilläggssidan](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) i dokumentationen för Experience Platform Launch.

Det här målet är ett [!DNL Experience Platform Launch] tillägg. Mer information om hur Launch-tillägg fungerar i CDP i realtid finns i Översikt över [](../launch-extensions/overview.md)Experience Platform Launch-tillägg.

![Audience Manager DIL utökningen](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] katalogen för alla kunder som har köpt CDP i realtid.

Om du vill använda det här tillägget måste du ha tillgång till [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till [!DNL Platform Launch] och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget [!DNL Audience Manager] DIL:

I CDP-gränssnittet [i](http://platform.adobe.com/)realtid går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om **[!UICONTROL Configure]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).

I **[!UICONTROL Select available Launch property]** fönstret väljer du den [!DNL Launch] egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i Launch. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i [!DNL Launch] dokumentationen.

Arbetsflödet tar dig [!DNL Launch] till att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på [Audience Manager-tilläggssidan](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) i [!DNL Experience Launch] dokumentationen.

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



