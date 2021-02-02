---
keywords: Analystillägg;analystillägg;målanalys
title: Adobe Analytics-tillägg
seo-title: Adobe Analytics-tillägg
description: Adobe Analytics-tillägget är ett analysmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Adobe Analytics-tillägget är ett analysmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Adobe Analytics-tillägg {#adobe-analytics-extension}

## Översikt {#overview}

Adobe Analytics är en branschledande lösning som ger er möjlighet att förstå era kunder som människor och styra verksamheten med kundanalys.

Adobe Analytics är ett analystillägg i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100156.html).

Målet är ett [!DNL Adobe Experience Platform Launch]-tillägg. Mer information om hur [!DNL Platform Launch]-tillägg fungerar i Platform finns i [Översikt över Experience Platform Launch-tillägg](../launch-extensions/overview.md).

![Adobe Analytics-tillägg](../../assets/catalog/analytics/adobe-analytics/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha åtkomst till [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta organisationens administratör för att få åtkomst till [!DNL Launch] och be dem ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du Adobe Analytics-tillägget:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [plattformsgränssnittet](http://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Förutsättningar](#prerequisites).

I fönstret **[!UICONTROL Select available Platform Launch property]** väljer du den [!DNL Platform Launch]-egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Platform Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i [egenskapssidans avsnitt](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) i [!DNL Launch]-dokumentationen.

Arbetsflödet tar dig till [!DNL Platform Launch] för att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på sidan [Adobe Analytics-tillägg](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) i dokumentationen för Experience [!DNL Launch].

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägg till ett nytt tillägg](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) i [!DNL Platform Launch]-dokumentationen.

## Använda tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i [!DNL Platform Launch].

I [!DNL Platform Launch] kan du konfigurera regler för de installerade tilläggen så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för tillägg finns i [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i gränssnittet [!DNL Platform Launch].

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande **[!UICONTROL Install]** som plattformsgränssnitt för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [Installera tillägget](#install-extension) för att komma till [!DNL Platform Launch] och konfigurera eller ta bort tillägget.

Mer information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i [!DNL Platform Launch]-dokumentationen.



