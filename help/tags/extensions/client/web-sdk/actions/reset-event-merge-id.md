---
title: Återställ sammanfognings-ID
description: Föråldrad åtgärd som gör att du kan separera händelser som anropas på samma sida.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Återställ sammanfognings-ID

>[!IMPORTANT]
>
>Den här åtgärden är föråldrad. Använd inställningarna för [Samla in interna länkar](../configure/data-collection.md#collect-internal-link-clicks) i stället.

Åtgärdstypen **[!UICONTROL Reset merge ID]** gör att du kan separera händelser som anropas på samma sida. Det används vanligtvis i scenarier med interna länkar där du kan ha flera nyttolaster som du vill skicka till Adobe. Med den här åtgärden kan du återställa en händelses sammanfognings-ID så att de inte betraktas som en del av samma händelse när de har anlänt till Edge Network.

Om du vill styra hur flera händelser på samma sida separeras eller sammanfogas använder du alternativet [Samla interna länkklick](../configure/data-collection.md#collect-internal-link-clicks) när du konfigurerar taggtillägget.
