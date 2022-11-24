---
keywords: Audience Manager DIL-tillägg;målgruppshanterare;dil-tillägg
title: Audience Manager DIL utökningen
description: Tillägget Audience Manager DIL är ett mål för datahanteringsplattformen (DMP) i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Audience Manager DIL utökningen {#aam-dil-extension}

## Översikt {#overview}

Det här är Adobe Audience Manager Data Integration Library-tillägget (implementering på klientsidan). Obs! Det här tillägget är inte avsett att användas för vidarebefordran av Adobe Analytics-data på serversidan. För SSF använder du Adobe Analytics-tillägget. Viktigt: Från och med version 8.0 är DIL beroende av [!DNL Experience Cloud] ID-tjänst, version 3.3 eller senare. Implementera båda [!DNL Experience Cloud] Fullständig ID-tjänst och DIL [!DNL Audience Manager] funktioner för dataintegrering.

[!DNL Audience Manager] DIL är ett DMP-tillägg (Data Management Platform) i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns i [Audience Manager tilläggssida](../../../tags/extensions/client/audience-manager/overview.md) i taggdokumentationen.

Målet är ett taggtillägg. Mer information om hur tillägg fungerar i Platform finns i [taggtillägg - översikt](../launch-extensions/overview.md).

![Audience Manager DIL utökningen](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Adobe Experience Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till taggar och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du [!DNL Audience Manager] DIL-tillägg:

I [Plattformsgränssnitt](https://platform.adobe.com/), gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i rätt spår. Om **[!UICONTROL Configure]** kontrollen är nedtonad, du saknar **[!UICONTROL manage_properties]** behörighet. Se [Förutsättningar](#prerequisites).

Välj den egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Läs om egenskaperna i [taggdokumentation](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Arbetsflödet vägleder dig genom stegen för att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns i [Audience Manager tilläggssida](../../../tags/extensions/client/audience-manager/overview.md) i taggdokumentationen.

Du kan även installera tillägget direkt i [Användargränssnitt för datainsamling](https://experience.adobe.com/#/data-collection/). Se guiden [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) för mer information.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler. I användargränssnittet för datainsamling kan du ange regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i översikten på [regler](../../../tags/ui/managing-resources/rules.md) i taggdokumentationen.

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas ändå gränssnittet **[!UICONTROL Install]** för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Om du vill uppgradera tillägget läser du i guiden på sidan [uppgraderingsprocess för tillägg](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
