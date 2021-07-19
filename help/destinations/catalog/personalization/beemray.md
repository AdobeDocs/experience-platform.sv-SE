---
keywords: beemray,beemray-tillägg
title: Beemray-tillägg
description: Beemray-tillägget är ett personaliseringsmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 5bb639f5-42b5-48ae-a3e9-7585595ab925
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# [!DNL Beemray] extension {#beemray-extension}

## Översikt {#overview}

[!DNL Beemray] hjälper dig att snabba upp din produkt i ett situationssammanhang. Gör det möjligt för er att få insikter, skapa nya upplevelser, skapa interaktioner och engagera i ögonblick som verkligen betyder något. Beemray automatiserar kontextuell intelligens med maskininlärning. Beemray är knutet till Adobe Experience Cloud och övriga av era tekniska partners. Allt äger rum i realtid. Det här tillägget installerar [!DNL Beemray] SDK på din plats.

Beemray är ett personaliseringstillägg i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

Målet är ett [!DNL Adobe Experience Platform Launch]-tillägg. Mer information om hur [!DNL Platform Launch]-tillägg fungerar i Platform finns i [Översikt över Experience Platform Launch-tillägg](../launch-extensions/overview.md).

![Beemray-tillägg](../../assets/catalog/personalization/beemray/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations]-katalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha åtkomst till [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta organisationens administratör för att få åtkomst till [!DNL Platform Launch] och be dem ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget [!DNL Beemray]:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [plattformsgränssnittet](http://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Förutsättningar](#prerequisites).

I fönstret **[!UICONTROL Select available Platform Launch property]** väljer du den [!DNL Platform Launch]-egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap i [!DNL Platform Launch]. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i [egenskapssidans avsnitt](../../../tags/ui/administration/companies-and-properties.md#properties-page) i [!DNL Launch]-dokumentationen.

Arbetsflödet tar dig till [!DNL Platform Launch] för att slutföra installationen.

Information om alternativ för tilläggskonfiguration och installationsstöd finns på sidan [Beemray på Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

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
