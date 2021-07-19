---
keywords: Advertising Cloud;advertising cloud cloud extension; annonsmolnmål
title: Adobe Advertising Cloud-tillägg
description: Adobe Advertising Cloud-tillägget är ett reklammål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Adobe Advertising Cloud-tillägg {#adobe-advertising-cloud-extension}

## Översikt {#overview}

Det här är [!DNL Advertising Cloud]-tillägget för implementering av [!DNL Advertising Cloud]-konverterings- och segmenttaggar för både DSP och sökning (DCO stöds inte för närvarande).

Adobe Advertising Cloud är ett reklamtillägg i Adobe Experience Platform.

Målet är ett [!DNL Adobe Experience Platform Launch]-tillägg. Mer information om hur [!DNL Platform Launch]-tillägg fungerar i Platform finns i [Översikt över Experience Platform Launch-tillägg](../launch-extensions/overview.md).

![Adobe Advertising Cloud-tillägg](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha åtkomst till [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta organisationens administratör för att få åtkomst till [!DNL Launch] och be dem ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du Adobe Advertising Cloud-tillägget:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [plattformsgränssnittet](http://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Förutsättningar](#prerequisites).

I fönstret **[!UICONTROL Select available Platform Launch property]** väljer du den [!DNL Platform Launch]-egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Platform Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i [egenskapssidans avsnitt](../../../tags/ui/administration/companies-and-properties.md#properties-page) i [!DNL Launch]-dokumentationen.

Arbetsflödet tar dig till [!DNL Platform Launch] för att slutföra installationen.

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägg till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) i [!DNL Platform Launch]-dokumentationen.


## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i [!DNL Platform Launch].

I [!DNL Platform Launch] kan du konfigurera regler för de installerade tilläggen så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för tillägg finns i [Regeldokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i gränssnittet [!DNL Platform Launch].

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande **[!UICONTROL Install]** som plattformsgränssnitt för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [Installera tillägget](#install-extension) för att komma till [!DNL Platform Launch] och konfigurera eller ta bort tillägget.

Mer information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i [!DNL Platform Launch]-dokumentationen.
