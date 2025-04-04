---
keywords: Audience Manager DIL-tillägg;målgruppshanterare;dil-tillägg
title: Audience Manager DIL-tillägg
description: Audience Manager DIL-tillägget är ett mål för datahanteringsplattformen (DMP) i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan i Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Audience Manager DIL-tillägg {#aam-dil-extension}

## Översikt {#overview}

Detta är tillägget Adobe Audience Manager Data Integration Library (implementering på klientsidan). Obs! Det här tillägget är inte avsett att användas för vidarebefordran av Adobe Analytics-data på serversidan. För SSF använder du Adobe Analytics-tillägget. Viktigt: Från och med version 8.0 är DIL beroende av [!DNL Experience Cloud] ID-tjänsten, version 3.3 eller senare. Implementera både [!DNL Experience Cloud] ID-tjänsten och DIL för fullständiga [!DNL Audience Manager] dataintegreringsfunktioner.

[!DNL Audience Manager] DIL är ett tillägg för datahanteringsplattform (DMP) i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på sidan [Audience Manager-tillägg](../../../tags/extensions/client/audience-manager/overview.md) i taggdokumentationen.

Det här målet är ett taggtillägg. Mer information om hur tillägg fungerar i Experience Platform finns i [Översikt över taggtillägg](../launch-extensions/overview.md).

![Audience Manager DIL-tillägg](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Förhandskrav {#prerequisites}

Det här tillägget är tillgängligt i katalogen [!DNL Destinations] för alla kunder som har köpt Experience Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Adobe Experience Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till taggar och be dem att ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du DIL-tillägget [!DNL Audience Manager]:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [Experience Platform-gränssnittet](https://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Krav](#prerequisites).

Välj den egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Läs mer om egenskaper i [taggdokumentationen](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Arbetsflödet vägleder dig genom de olika stegen för att slutföra installationen.

Mer information om alternativen för tilläggskonfigurationen finns på [Audience Manager-tilläggssidan](../../../tags/extensions/client/audience-manager/overview.md) i taggdokumentationen.

Du kan också installera tillägget direkt i [användargränssnittet för datainsamling](https://experience.adobe.com/#/data-collection/). Mer information finns i guiden om att [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler. I användargränssnittet för datainsamling kan du ange regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för dina tillägg finns i översikten över [regler](../../../tags/ui/managing-resources/rules.md) i taggdokumentationen.

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas ändå **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i handboken om uppgraderingsprocessen för [tillägget](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
