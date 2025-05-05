---
keywords: Marketo Web Personalization;marketo web personalization;Marketo Web Personalization extension;marketo web personalization extension;marketo;Marketo
title: Marketo Web Personalization-tillägg
description: Tillägget Marketo Web Personalization är ett personaliseringsmål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan i Adobe Exchange.
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# [!DNL Marketo Web Personalization]-tillägg {#marketo-web-personalization-extension}

## Översikt {#overview}

Det här tillägget distribuerar skriptet för [!DNL Marketo's] Web Personalization- och ContentAI-program. [!DNL Marketo] Web Personalization identifierar och personaliserar unikt innehåll för webbbesökares egenskaper, till exempel bekräftelsegrafik för anonyma besökare och en mängd beteendeattribut i [!DNL Marketo] Engagement Platform för kända besökare. [!DNL Marketo] ContentAI innehåller funktioner för AI-baserade rekommendationer och personalisering för webb- och e-postkampanjer som är unika för B2B-kunder.

[!DNL Marketo Web Personalization] är ett personaliseringstillägg i Adobe Experience Platform. Mer information om webbanpassning och innehålls-AI i Marketo finns i [Webböversikt för Personalization](https://experienceleague.adobe.com/docs/marketo/using/product-docs/web-personalization/understanding-web-personalization/web-personalization-overview.html?lang=sv-SE).

Det här målet är ett taggtillägg. Mer information om hur taggtillägg fungerar i Experience Platform finns i [Översikt över taggtillägg](../launch-extensions/overview.md).

![Marketo Web Personalization Extension](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## Förhandskrav {#prerequisites}

Det här tillägget är tillgängligt i katalogen [!DNL Destinations] för alla kunder som har köpt Experience Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Adobe Experience Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till taggar och be dem att ge dig behörigheten **[!UICONTROL manage_properties]** så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget [!DNL Marketo Web Personalization]:

Gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** i [Experience Platform-gränssnittet](https://platform.adobe.com/).

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om kontrollen **[!UICONTROL Configure]** är nedtonad saknar du behörigheten **[!UICONTROL manage_properties]**. Se [Krav](#prerequisites).

Välj den egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i avsnittet [Egenskaper](../../../tags/ui/administration/companies-and-properties.md#properties-page) i taggdokumentationen.

Arbetsflödet vägleder dig genom de olika stegen för att slutföra installationen.

Du kan också installera tillägget direkt i [användargränssnittet för datainsamling](https://experience.adobe.com/#/data-collection/). Mer information finns i avsnittet om att [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) i taggdokumentationen.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler.

Du kan konfigurera regler för de installerade tilläggen så att händelsedata skickas till tilläggets mål endast i vissa situationer. Mer information om hur du konfigurerar regler för dina tillägg finns i [taggdokumentationen](../../../tags/ui/managing-resources/rules.md).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande **[!UICONTROL Install]** för tillägget i Experience Platform-gränssnittet. Stäng av installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i handboken om uppgraderingsprocessen för [tillägget](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
