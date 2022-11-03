---
keywords: gtag;google gtag;Google extension;google gtag extension;GTAG
title: Google Gtag-tillägg
description: Tillägget Google Gtag är ett reklammål i Adobe Experience Platform. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Google Gtag-tillägg {#gtag-advertising-extension}

>[!IMPORTANT]
>
>Tillägget Google Gtag som beskrivs här har ersatts och ersatts av [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) tillägg utvecklad av [!DNL Acronym]. Du hittar [!DNL Google Global Site Tag (gtag)] tillägget inom [[!UICONTROL Tags]](../../../tags/home.md) i användargränssnittet för datainsamling eller användargränssnittet för Experience Platform.

## Översikt {#overview}

Läs in Google `gtag.js` till din webbplats för att skicka händelsedata till [!DNL Google Analytics], Google Ads och [!DNL Google Marketing Platform]. Det här tillägget lägger bara till gtag-koden på din plats. Du måste använda andra Google-tillägg för att lägga till händelser och åtgärder som ska använda gtag.

Google gtag är ett reklamtillägg i Adobe Experience Platform. Mer information om tilläggsfunktioner finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Målet är ett taggtillägg. Mer information om hur taggtillägg fungerar i Platform finns i [taggtillägg - översikt](../launch-extensions/overview.md).

![Google Gtag-tillägg](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] för alla kunder som har köpt Platform.

Om du vill använda det här tillägget måste du ha tillgång till taggar i Adobe Experience Platform. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde. Kontakta din organisations administratör för att få åtkomst till taggar och be dem att ge dig **[!UICONTROL manage_properties]** behörighet så att du kan installera tillägg.

## Installera tillägg {#install-extension}

Så här installerar du tillägget Google Gtag:

I [Plattformsgränssnitt](https://platform.adobe.com/), gå till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i rätt spår. Om **[!UICONTROL Configure]** kontrollen är nedtonad, du saknar **[!UICONTROL manage_properties]** behörighet. Se [Förutsättningar](#prerequisites).

Välj den egenskap i vilken du vill installera tillägget. Du kan också skapa en ny egenskap. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Läs om egenskaperna i [Avsnittet Egenskaper](../../../tags/ui/administration/companies-and-properties.md#properties-page) i taggdokumentationen.

Arbetsflödet vägleder dig genom stegen för att slutföra installationen.

Mer information om alternativ för tilläggskonfiguration och installationssupport finns i [Google gtag page on Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Du kan även installera tillägget direkt i [Användargränssnitt för datainsamling](https://experience.adobe.com/#/data-collection/). Mer information finns i avsnittet om [lägga till ett nytt tillägg](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) i taggdokumentationen.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler.

Du kan konfigurera regler för de installerade tilläggen så att händelsedata skickas till tilläggets mål endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i [taggdokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i användargränssnittet för datainsamling.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande plattformsgränssnittet **[!UICONTROL Install]** för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [Installera tillägg](#install-extension) för att konfigurera eller ta bort tillägget.

Om du vill uppgradera tillägget läser du i guiden på sidan [uppgraderingsprocess för tillägg](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) i taggdokumentationen.
