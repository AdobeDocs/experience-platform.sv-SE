---
title: Använd svar
description: Utför en åtgärd baserat på ett svar från Edge Network.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Använd svar

Med åtgärdstypen **[!UICONTROL Apply response]** kan du utföra olika åtgärder baserat på ett svar från Edge Network. Den här åtgärdstypen används vanligtvis i hybriddistributioner där servern gör ett första anrop till Edge Network. Den här åtgärdstypen tar svaret från det anropet och initierar Web SDK i webbläsaren. Om du använder den här åtgärdstypen kan klientbelastningstiden minskas för hybridpersonalisering.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ sedan in [!UICONTROL Action type] på **[!UICONTROL Apply response]**.

![Bild av Experience Platform användargränssnitt som visar typen Använd svarsåtgärd.](../assets/apply-response.png)

## Användningsfall

* **Manuell delning mellan datainsamling och personalisering**: Du kan utlösa en [Skicka-händelse](send-event.md)-åtgärd med återgivningsbeslut inställda på `false` och sedan få en&quot;Skicka händelse klar&quot;-regel att fånga upp löftet. Den första åtgärden i den här regeln kan vara &quot;Använd svar&quot;. Med det här arbetsflödet kan du fördröja DOM-manipuleringen tills din organisations egen kod har slutat med annat arbete.
* **Edge-svar som tagits emot utanför Web SDK**: Om du använder ett annat bibliotek för att kommunicera med Edge Network kan du tillåta att Web SDK fortfarande hanterar svaret från Edge Network med den här åtgärden.

## Tillgängliga fält

Den här åtgärdstypen stöder följande konfigurationsalternativ:

* **[!UICONTROL Instance]**: Den SDK-instans som åtgärden gäller för. Den här nedrullningsbara menyn är inaktiverad om implementeringen använder en enda SDK-instans.
* **[!UICONTROL Response headers]**: Markera det dataelement som returnerar ett objekt som innehåller huvudnycklar och värden som returneras från Edge Network-serveranropet.
* **[!UICONTROL Response body]**: Välj det dataelement som returnerar objektet som innehåller JSON-nyttolasten som tillhandahålls av Edge Network-svaret.
* **[!UICONTROL Render visual personalization decisions]**: Aktivera det här alternativet för att automatiskt återge det personaliseringsinnehåll som tillhandahålls av Edge Network och dölja innehållet i förväg för att förhindra flimmer.
