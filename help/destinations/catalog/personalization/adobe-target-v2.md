---
keywords: måltillägg;mål;mål v2;mål v2-tillägg
title: Adobe Target v2-tillägg
description: Tillägget Adobe Target v2 är ett personaliseringsmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Adobe Target v2-tillägg {#adobe-target-v2-extension}

## Översikt {#overview}

Adobe Target är en Adobe Experience Cloud-lösning som innehåller allt ni behöver för att skräddarsy och personalisera kundernas upplevelse och maximera intäkterna från era webbplatser, mobilsajter, appar, sociala medier och andra digitala kanaler.

Adobe Target v2 är ett personaliseringstillägg i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102722.adobe-target-v2-launch-extension.html).

Det här målet är ett Adobe Experience Platform Launch-tillägg. Mer information om hur tillägg till Platforma launcher fungerar i Platform finns i [Översikt över tillägg till Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Adobe Target v2-tillägg](../../assets/catalog/personalization/adobe-target-v2/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations]-katalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha åtkomst till [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta organisationens administratör för att få åtkomst till [!DNL Platform Launch] och be dem ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget Adobe Target v2:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [plattformsgränssnittet](http://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Förutsättningar](#prerequisites).

I fönstret **[!UICONTROL Select available Launch property]** väljer du den [!DNL Launch]-egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i [egenskapssidans avsnitt](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) i [!DNL Launch]-dokumentationen.

Arbetsflödet tar dig till [!DNL Launch] för att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på [Adobe Target v2-tilläggssidan](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/targetv2-extension/adobe-target-extension-v2.html) i [!DNL Experience Launch]-dokumentationen.

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägg till ett nytt tillägg](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) i [!DNL Platform Launch]-dokumentationen.


## Använda tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i [!DNL Platform Launch].

I [!DNL Platform Launch] kan du konfigurera regler för de installerade tilläggen så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för tillägg finns i [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i gränssnittet [!DNL Platform Launch].

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande **[!UICONTROL Install]** som plattformsgränssnitt för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [Installera tillägget](#install-extension) för att komma till [!DNL Platform Launch] och konfigurera eller ta bort tillägget.

Mer information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i [!DNL Platform Launch]-dokumentationen.
