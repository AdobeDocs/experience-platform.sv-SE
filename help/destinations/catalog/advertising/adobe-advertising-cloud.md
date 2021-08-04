---
keywords: Advertising Cloud;advertising cloud cloud extension; annonsmolnmål
title: Adobe Advertising Cloud-tillägg
description: Adobe Advertising Cloud-tillägget är ett reklammål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Adobe Advertising Cloud-tillägg {#adobe-advertising-cloud-extension}

## Översikt {#overview}

Det här är [!DNL Advertising Cloud]-tillägget för implementering av [!DNL Advertising Cloud]-konverterings- och segmenttaggar för både DSP och sökning (DCO stöds inte för närvarande).

Adobe Advertising Cloud är ett reklamtillägg i Adobe Experience Platform.

Målet är ett taggtillägg. Mer information om hur taggtillägg fungerar i Platform finns i [översikten över taggtillägg](../launch-extensions/overview.md).

![Adobe Advertising Cloud-tillägg](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta organisationens administratör för att få åtkomst till användargränssnittet för datainsamling och be dem ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du Adobe Advertising Cloud-tillägget:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [plattformsgränssnittet](https://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Förutsättningar](#prerequisites).

Välj taggegenskapen som du vill installera tillägget i. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Läs mer om egenskaper i [taggdokumentationen](../../../tags/ui/administration/companies-and-properties.md).

Arbetsflödet tar dig till användargränssnittet för datainsamling för att slutföra installationen.

Du kan också installera tillägget direkt i [användargränssnittet för datainsamling](https://experience.adobe.com/#/data-collection/). Mer information finns i guiden om att [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler. I användargränssnittet för datainsamling kan du ange regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för dina tillägg finns i översikten över [regler](../../../tags/ui/managing-resources/rules.md) i taggdokumentationen.

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas ändå **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [Installera tillägget](#install-extension) för att konfigurera eller ta bort tillägget.

Om du vill uppgradera tillägget läser du guiden för [uppgraderingsprocessen](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
