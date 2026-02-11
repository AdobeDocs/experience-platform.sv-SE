---
title: Uppdatera variabel
description: Ändrar innehållet i ett variabelt dataelement.
exl-id: 6c558d1e-85b4-45f9-ba4d-5fed1ec6e308
source-git-commit: 50881ef9498196f2de5519f050800334019a2586
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Uppdatera variabel

Med åtgärden **[!UICONTROL Update variable]** kan du göra partiella eller stegvisa ändringar i ett [variabeldataelement](../data-element-types.md#variable). Du kan använda den här åtgärden för att skapa ett objekt som senare kan refereras i en [[!UICONTROL Send event]](send-event.md)-åtgärd. Att fylla i dataelement och tilldela dem till egenskaper i ett XDM-objekt passar de flesta användningsfall. Den här åtgärden ger större flexibilitet så att du kan ställa in egenskaper på olika dataelement baserat på regelförhållanden.

Innan du använder den här åtgärden måste du ha skapat ett variabeldataelement. När du har valt ett variabeldataelement att ändra visas en redigerare där du kan ange önskade fält för den här åtgärden.

![Skärmbild av uppdateringsvariabelåtgärden i åtgärdskonfigurationsgränssnittet](../assets/update-variable.png)

Det XDM-schema som används i redigeraren matchar det schema som valts i variabeldataelementet. Du kan ange en eller flera egenskaper för objektet genom att expandera objekt och välja önskade egenskaper. I skärmbilden nedan är till exempel egenskapen `producedBy` inställd på dataelementet `%Produced by data element%`.

![Skärmbild av åtgärdskonfigurationsgränssnittet som visar en uppdaterad egenskap &#x200B;](../assets/update-variable-set-property.png)

Om du väljer ett variabeldataelement som använder ett dataobjekt i stället för ett XDM-objekt, beror tillgängliga fält på vilka produkter som valts när dataelementet konfigureras. Om du till exempel skapar ett dataobjekt som innehåller Adobe Analytics, fält och sedan väljer variabeldataelementet i det här användargränssnittet, får du fält som du kan fylla i specifikt för Adobe Analytics.

![Skärmbild av åtgärdskonfigurationsgränssnittet som visar ett variabelt dataelement baserat på ett dataobjekt](../assets/variable-data-element-data.png)
