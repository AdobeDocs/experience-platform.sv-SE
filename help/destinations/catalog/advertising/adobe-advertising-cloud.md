---
keywords: Advertising Cloud;advertising cloud cloud extension; annonsmolnmål
title: Adobe Advertising Cloud-tillägg
description: Adobe Advertising Cloud-tillägget är ett reklammål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Adobe Advertising Cloud-tillägg {#adobe-advertising-cloud-extension}

## Översikt {#overview}

Det här är [!DNL Advertising Cloud] tillägg för genomförande [!DNL Advertising Cloud] konverterings- och segmenttaggar för både DSP och sökning (DCO stöds inte för närvarande).

Adobe Advertising Cloud är ett reklamtillägg i Adobe Experience Platform.

Målet är ett taggtillägg. Mer information om hur taggtillägg fungerar i Platform finns i [taggtillägg - översikt](../launch-extensions/overview.md).

![Adobe Advertising Cloud-tillägg](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till användargränssnittet för datainsamling och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du Adobe Advertising Cloud-tillägget:

I [Plattformsgränssnitt](https://platform.adobe.com/), gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i rätt spår. Om **[!UICONTROL Configure]** kontrollen är nedtonad, du saknar **[!UICONTROL manage_properties]** behörighet. Se [Förutsättningar](#prerequisites).

Välj taggegenskapen som du vill installera tillägget i. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Läs om egenskaperna i [taggdokumentation](../../../tags/ui/administration/companies-and-properties.md).

Arbetsflödet tar dig till användargränssnittet för datainsamling för att slutföra installationen.

Du kan även installera tillägget direkt i [Användargränssnitt för datainsamling](https://experience.adobe.com/#/data-collection/). Se guiden [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) för mer information.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler. I användargränssnittet för datainsamling kan du ange regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i översikten på [regler](../../../tags/ui/managing-resources/rules.md) i taggdokumentationen.

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas ändå gränssnittet **[!UICONTROL Install]** för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Om du vill uppgradera tillägget läser du i guiden på sidan [uppgraderingsprocess för tillägg](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
