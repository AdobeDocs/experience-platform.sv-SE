---
title: data
description: Lär dig hur du skickar data som inte är XDM till Adobe via dataobjektet.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

Med objektet `data` kan du skicka en nyttolast till Adobe som inte matchar ett XDM-schema. Det är användbart i andra scenarier än XDM, som att skicka data direkt till Adobe Analytics, Adobe Target eller Adobe Audience Manager. När data anländer till datastream kan du använda [dataprep-mappning](/help/data-prep/ui/mapping.md) för att tilldela XDM-fält till varje fält i `data`-objektet. Om en produkt redan har konfigurerats av Adobe för att identifiera fält i objektet `data` kan du skicka data i befintligt skick till en datastam.

>[!IMPORTANT]
>
>Data i det här objektet måste ha minst en av följande åtgärder:
>
>* En tjänst i datastream måste konfigureras för att hämta data från en angiven egenskap i objektet `data`.
>* Den angivna egenskapen måste mappas till ett XDM-fält med hjälp av dataprep.
>
>Om en viss egenskap inte är mappad till ett XDM-fält eller används av en konfigurerad tjänst, går dessa data förlorade permanent.

Ange objektet `data` som en del av JSON-objektet i parametern för kommandot `sendEvent`. För data som du planerar att mappa i datastream kan du strukturera det här objektet hur du vill. För data som används av vissa tjänster måste objekthierarkin matcha vad tjänsten förväntar sig. Du kan inkludera både objektet `data` och objektet [`xdm`](xdm.md) i samma `sendEvent`-kommando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Använd objektet `data` med Adobe Analytics {#analytics}

Du kan använda objektet `data` med Adobe Analytics för att skicka data till en rapportsvit utan ett XDM-schema. Variabler är konfigurerade att använda samma syntax som AppMeasurement-variabler, vilket förenklar uppgraderingsprocessen till Web SDK. Mer information finns i [Variabelmappning av dataobjekt till Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) i Adobe Analytics implementeringsguide.

## Använd objektet `data` med hjälp av taggtillägget Web SDK

Objektet `data` är tillgängligt som ett [variabelt dataelement](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) när du använder taggtillägget Web SDK.
