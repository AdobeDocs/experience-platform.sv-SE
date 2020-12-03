---
keywords: Nielsen BSDK;nielsen bsdk;nielsen BSDK
title: Nielsen BSDK-tillägg
seo-title: Nielsen BSDK-tillägg
description: Tillägget Nielsen BSDK är ett analysmål i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
seo-description: Tillägget Nielsen BSDK är ett analysmål i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på Adobe Exchange.
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# [!DNL Nielsen BSDK] Tillägg {#nielsen-bsdk-extension}

## Översikt {#overview}

[!DNL Nielsen Digital SDK] lanseringstillägget erbjuder målgruppsmätning via följande mätprodukter:

DCR: En mätningslösning som ger daglig mätning av icke-linjärt digitalt innehåll, inklusive innehåll med annonser, ger en heltäckande bild av hur det digitala innehållet konsumeras på datorer, mobiler, surfplattor och anslutna enheter.

DTVR: Detta gäller för linjär TV-visning på datorer och mobila enheter för deltagande programmeringskällor. Detta är den första lösningen som får ackreditering från MRC för dess bidrag till mätning av tv-publik för programmering som visas på datorer och mobila enheter.

[!DNL Nielsen BSDK] är ett analystillägg i kunddataplattformen i realtid. Mer information om tilläggsfunktionerna finns på tilläggssidan på [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

Det här målet är ett Adobe Experience Platform Launch-tillägg. Mer information om hur plattformstillägg fungerar i CDP i realtid finns i Översikt över [Adobe Experience Platform Launch-tillägg](../launch-extensions/overview.md).

![Nielsen BSDK Extension](../../assets/catalog/analytics/nielsen-bsdk/catalog.png)

## Förutsättningar {#prerequisites}

Det här tillägget är tillgängligt i [!DNL Destinations] katalogen för alla kunder som har köpt CDP i realtid.

Om du vill använda det här tillägget måste du ha tillgång till Adobe Experience Platform Launch. Platform Launch erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion. Kontakta din organisations administratör för att få åtkomst till plattformsstart och be dem att ge dig behörighet att installera tillägg så att du kan installera dem **[!UICONTROL manage_properties]** .

## Installera tillägg {#install-extension}

Så här installerar du [!DNL Nielsen BSDK] tillägget:

I CDP-gränssnittet [i](http://platform.adobe.com/)realtid går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Välj tillägget i katalogen eller använd sökfältet.

Klicka på målet för att markera det och välj sedan **[!UICONTROL Configure]** i den högra listen. Om **[!UICONTROL Configure]** kontrollen är nedtonad saknar du **[!UICONTROL manage_properties]** behörigheten. Se [Förutsättningar](#prerequisites).

I **[!UICONTROL Select available Platform Launch property]** fönstret väljer du den Platform Launch-egenskap där du vill installera tillägget. Du kan också skapa en ny egenskap i Platform Launch. En egenskap är en samling regler, dataelement, konfigurerade tillägg, miljöer och bibliotek. Lär dig mer om egenskaper i delen [](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Egenskaper i dokumentationen för plattformsinstallationen.

Arbetsflödet tar dig till Platform Launch för att slutföra installationen.

Information om alternativ för tilläggskonfiguration och installationsstöd finns på [Nielsen BSDK-sidan på Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

Du kan också installera tillägget direkt i [Adobe Experience Platform Launch-gränssnittet](https://launch.adobe.com/). Se [Lägga till ett nytt tillägg](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) i dokumentationen för plattformsstarten.

## Så här använder du tillägget {#how-to-use}

När du har installerat tillägget kan du börja konfigurera regler för det direkt i Platform Launch.

I Platform Launch kan du konfigurera regler för dina installerade tillägg så att händelsedata skickas till tilläggsmålet endast i vissa situationer. Mer information om hur du ställer in regler för tillägg finns i [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurera, uppgradera och ta bort tillägg {#configure-upgrade-delete}

Du kan konfigurera, uppgradera och ta bort tillägg i plattformens startgränssnitt.

>[!TIP]
>
>Om tillägget redan är installerat på en av dina egenskaper visas fortfarande CDP-gränssnittet i realtid **[!UICONTROL Install]** för tillägget. Starta installationsarbetsflödet enligt beskrivningen i [installationstillägget](#install-extension) för att komma till Platform Launch och konfigurera eller ta bort tillägget.

Information om hur du uppgraderar ditt tillägg finns i [Tilläggsuppgradering](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) i dokumentationen för Platform Launch.