---
keywords: JW player;jw player;JW Player;jw extension;JW extension
title: JW Player Analytics-tillägg (Beta)
description: Tillägget JW Player Analytics (Beta) är ett analysmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 32bdb2db-5c1b-4184-b6d3-b07dc4d0b324
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# [!DNL JW Player Analytics] (Beta)-tillägg {#jw-player-analytics-extension}

## Översikt {#overview}

Det här tillägget installerar [!DNL JW Player]-kortet för att ansluta [!DNL JW Player]-händelser till Adobe Video Analytics. Utnyttja möjligheterna i Adobe Video Analytics för att få detaljerade insikter om kundernas videovisningsvanor.

[!DNL JW Player Analytics] (Beta) är ett analystillägg i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101523.jw-player-analytics-launch-extension.html).

Det här målet är ett taggtillägg. Mer information om hur taggtillägg fungerar i Platform finns i [Översikt över taggtillägg](../launch-extensions/overview.md).

![JW-analystillägg](../../assets/catalog/analytics/jw-analytics/catalog.png)

## Förhandskrav {#prerequisites}

Det här tillägget är tillgängligt i katalogen [!DNL Destinations] för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Adobe Experience Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till taggar och be dem att ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Installera tillägget [!DNL JW Player Analytics] (Beta):

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [Plattformsgränssnittet](https://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Krav](#prerequisites).

Välj den egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [Egenskaper](../../../tags/ui/administration/companies-and-properties.md#properties-page) i taggdokumentationen.

Arbetsflödet vägleder dig genom de olika stegen för att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på tilläggssidan [JW Player Analytics (Beta)](https://exchange.adobe.com/experiencecloud.details.101523.jw-player-analytics-launch-extension.html) i Adobe Exchange.

Du kan också installera tillägget direkt i [användargränssnittet för datainsamling](https://experience.adobe.com/#/data-collection/). Mer information finns i avsnittet om att [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) i taggdokumentationen.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler.

Du kan konfigurera regler för de installerade tilläggen så att händelsedata skickas till tilläggets mål endast i vissa situationer. Mer information om hur du konfigurerar regler för dina tillägg finns i [taggdokumentationen](../../../tags/ui/managing-resources/rules.md).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande **[!UICONTROL Install]** som plattformsgränssnitt för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i handboken om uppgraderingsprocessen för [tillägget](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
