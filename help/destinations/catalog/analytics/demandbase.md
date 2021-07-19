---
keywords: demandbase-tillägg;demandbase;demandbase-mål
title: Demandbase-tillägg
description: Demandbase-tillägget är ett analysmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 112a9575-4527-4a32-9610-a9d18ffd84f1
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# [!DNL Demandbase] extension {#demandbase-extension}

## Översikt {#overview}

Få insikter om B2B-konton direkt i Adobe Analytics där du kan segmentera trafik och beteende efter bransch, intäkt och målkonton. [!DNL Demandbase] Denna kontobaserade vy ger unika insikter om engagemang, konvertering och källan för era mest värdefulla besökare.

[!DNL Demandbase] är ett analystillägg i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101605.html).

Det här målet är ett Adobe Experience Platform Launch-tillägg. Mer information om hur tillägg till Platforma launcher fungerar i Platform finns i [Översikt över tillägg till Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Demandbase-tillägg](../../assets/catalog/analytics/demandbase/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha tillgång till Adobe Experience Platform Launch. platform launch erbjuds Adobe Experience Cloud-kunder som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till Platform launch och be dem att ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget [!DNL Demandbase]:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [plattformsgränssnittet](http://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Förutsättningar](#prerequisites).

I fönstret **[!UICONTROL Select available Platform Launch property]** väljer du den Platform launch i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i Platforma launchen. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [Egenskaper](../../../tags/ui/administration/companies-and-properties.md#properties-page) i dokumentationen för Platforma launchen.

Arbetsflödet tar dig till Platforma launchen för att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på sidan [Demandbase-tillägg](https://exchange.adobe.com/experiencecloud.details.101605.html) på Adobe Exchange.

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägg till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) i dokumentationen för Platforma launchen.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i Platforma launchen.

I Platform launch kan du konfigurera regler för de installerade tilläggen så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för tillägg finns i [Regeldokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i Platforma launchens gränssnitt.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande **[!UICONTROL Install]** som plattformsgränssnitt för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [Installera tillägget](#install-extension) för att komma till Platforma launchen och konfigurera eller ta bort tillägget.

Mer information om hur du uppgraderar tillägget finns i [Tilläggsuppgradering](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i Platforma launchens dokumentation.
