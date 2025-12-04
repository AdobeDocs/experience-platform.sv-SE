---
title: Använd förslag
description: Rendera förslag i ensidiga program utan att öka mätvärdena.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Använd förslag

Åtgärdstypen **[!UICONTROL Apply propositions]** gör att du kan återge utkast i enkelsidiga program utan att öka måtten. Den här åtgärdstypen är användbar när du arbetar med ensidiga program där delar av sidan återges på nytt, vilket kan innebära att personaliseringar som redan används på sidan skrivs över.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ sedan in [!UICONTROL Action type] på **[!UICONTROL Apply propositions]**.

![Gränssnittet för Experience Platform-taggar visar åtgärdstypen Använd förslag.](../assets/apply-propositions.png)

## Användningsfall

Du kan använda den här åtgärdstypen för olika användningsområden, till exempel:

1. **Återgivningsruta för HTML erbjuder**. Förslag som uttryckligen begärts via ett omfång eller en yta från en **[!UICONTROL Send event]**-åtgärd återges inte automatiskt. Du kan använda åtgärdstypen **[!UICONTROL Apply propositions]** för att ange för Web SDK var de ska återges genom att ange förslagets metadata.
2. **Återge erbjudandena för en vy i ett ensidigt program**. När du återger en vyändringshändelse kan du, om analysdata inte är klara än, använda åtgärden **[!UICONTROL Apply propositions]** för att återge vyförslagen överst på sidan. Mer information finns i [övre och nedre delen av sidhändelser (andra sidvyn - alternativ 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md). Ange **[!UICONTROL View name]** i formuläret om du vill använda det.
3. **Återge förslag**. När webbplatsen använder ett ramverk som React för att återge innehåll kan du behöva tillämpa personaliseringen på nytt. I sådana fall kan du använda åtgärdstypen **[!UICONTROL Apply propositions]** för att göra detta.

Den här åtgärdstypen skickar ingen visningshändelse för renderade inlägg. Den håller reda på återgivna förslag så att de kan inkluderas i efterföljande **[!UICONTROL Send event]** anrop.

## Tillgängliga fält

Den här åtgärdstypen stöder följande fält:

* **[!UICONTROL Instance]**: Den SDK-instans som åtgärden gäller för. Den här nedrullningsbara menyn är inaktiverad om implementeringen använder en enda SDK-instans.
* **[!UICONTROL Propositions]**: En array med objekt som du vill återge igen.
* **[!UICONTROL View name]**: Namnet på den vy som ska återges.
* **[!UICONTROL Proposition metadata]**: Ett objekt som avgör hur HTML kan användas. Du kan ange den här informationen antingen via formuläret eller via ett dataelement. Den innehåller följande egenskaper:
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
