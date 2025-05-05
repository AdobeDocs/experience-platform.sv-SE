---
keywords: livefyre;livefyre extension
title: Adobe Livefyre-tillägg
description: Adobe Livefyre är en social destination i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan i Adobe Exchange.
exl-id: a134c144-e7b8-4d48-8c90-5999e5ceb8a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Adobe Livefyre-tillägg {#adobe-livefyre-extension}

## Översikt {#overview}

Med Adobe Livefyre kan ni upptäcka, ordna och publicera ett konstant flöde av användargenererat innehåll på er webbplats för att skapa autentiska och personaliserade upplevelser.

Adobe Livefyre är en social utbyggnad i Adobe Experience Platform. Mer information om Adobe Livefyre finns i [Handboken för Livefyre-implementering](https://experienceleague.adobe.com/docs/livefyre/implementation/home.html?lang=sv-SE).

Det här målet är ett taggtillägg. Mer information om hur taggtillägg fungerar i Experience Platform finns i [Översikt över taggtillägg](../launch-extensions/overview.md).

![Adobe Livefyre-tillägg](../../assets/catalog/social/adobe-livefyre/catalog.png)

## Förhandskrav {#prerequisites}

Det här tillägget är tillgängligt i katalogen [!DNL Destinations] för alla kunder som har köpt Experience Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Adobe Experience Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till taggar och be dem att ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du Adobe Livefyre-tillägget:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [Experience Platform-gränssnittet](https://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Krav](#prerequisites).

Välj taggegenskapen som du vill installera tillägget i. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Läs mer om egenskaper i [taggdokumentationen](../../../tags/ui/administration/companies-and-properties.md).

Arbetsflödet tar dig till användargränssnittet för datainsamling för att slutföra installationen.

Du kan också installera tillägget direkt i [användargränssnittet för datainsamling](https://experience.adobe.com/#/data-collection/). Mer information finns i guiden om att [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler. I användargränssnittet för datainsamling kan du ange regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du konfigurerar regler för dina tillägg finns i översikten över [regler](../../../tags/ui/managing-resources/rules.md) i taggdokumentationen.

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas ändå **[!UICONTROL Install]** för tillägget. Stäng av installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i handboken om uppgraderingsprocessen för [tillägget](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
