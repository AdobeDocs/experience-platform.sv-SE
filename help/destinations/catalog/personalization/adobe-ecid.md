---
Keywords: ECID;ecid
title: Tjänsttillägg för Experience Cloud ID
description: Tillägget för Experience Cloud ID-tjänsten är ett personaliseringsmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan i Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# [!DNL Experience Cloud]-ID-tjänsttillägg {#adobe-ecid-extension}

## Översikt {#overview}

Det här tillägget implementerar ID-tjänsten [!DNL Experience Cloud], som identifierar besökare i alla [!DNL Experience Cloud]-lösningar.

[!DNL Experience Cloud] ID-tjänsten är ett personaliseringstillägg i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på sidan [Experience Cloud ID-tjänsttillägg](../../../tags/extensions/client/id-service/overview.md) i taggningsdokumentationen.

Det här målet är ett taggtillägg. Mer information om hur taggtillägg fungerar i Experience Platform finns i [Översikt över taggtillägg](../launch-extensions/overview.md).

![Adobe ECID-tillägg](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Förhandskrav {#prerequisites}

Det här tillägget är tillgängligt i målkatalogen för alla kunder som har köpt Experience Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Experience Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till användargränssnittet för datainsamling och be dem ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tjänsttillägget [!DNL Experience Cloud] ID:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [Experience Platform-gränssnittet](https://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Krav](#prerequisites).

Välj taggegenskapen som du vill installera tillägget i. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Läs mer om egenskaper i [taggdokumentationen](../../../tags/ui/administration/companies-and-properties.md).

Arbetsflödet tar dig till användargränssnittet för datainsamling för att slutföra installationen.

Information om alternativ för tilläggskonfiguration och installationsstöd finns på [tilläggssidan för Experience Cloud ID-tjänsten](../../../tags/extensions/client/id-service/overview.md) i taggdokumentationen.

Du kan också installera tillägget direkt i [användargränssnittet för datainsamling](https://experience.adobe.com/#/data-collection/). Mer information finns i guiden om att [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler. I användargränssnittet för datainsamling kan du ange regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för dina tillägg finns i översikten över [regler](../../../tags/ui/managing-resources/rules.md) i taggdokumentationen.

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas ändå **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i handboken om uppgraderingsprocessen för [tillägget](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
