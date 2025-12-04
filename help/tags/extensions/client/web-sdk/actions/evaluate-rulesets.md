---
title: Utvärdera regeluppsättningar
description: Utlösa en utvärdering av en regeluppsättning manuellt.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---

# Utvärdera regeluppsättningar

Åtgärdstypen **[!UICONTROL Evaluate rulesets]** gör att du manuellt kan aktivera utvärderingar av regeluppsättningar. Regler returneras av Adobe Journey Optimizer för funktioner som webbläsarmeddelanden.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ sedan in [!UICONTROL Action type] på **[!UICONTROL Evaluate rulesets]**.

![Bild av Experience Platform användargränssnitt som visar åtgärdsmakrotypen Utvärdera regeluppsättningar för svar.](../assets/evaluate-rulesets.png)

## Tillgängliga fält

Den här åtgärdstypen stöder följande alternativ:

* **[!UICONTROL Render visual personalization decisions]**: En kryssruta som, när den är aktiverad, återger visuella anpassningsbeslut för de regeluppsättningsobjekt som matchar.
* **[!UICONTROL Decision context]**: Ett nyckelvärdesschema som används vid utvärdering av Adobe Journey Optimizer-regler för enhetsbeslut. Du kan ange beslutskontexten manuellt eller via ett dataelement.
