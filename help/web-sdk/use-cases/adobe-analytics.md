---
title: Skicka data till Adobe Analytics med Web SDK
description: Lär dig skicka data till Adobe Analytics med Adobe Experience Platform Web SDK.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---


# Skicka data till Adobe Analytics via Web SDK

Experience Platform Web SDK kan skicka data till Adobe Analytics via Experience Platform Edge Network. I Adobe finns flera alternativ för att skicka data till Adobe Analytics via Web SDK:

* Lägg till [**[!UICONTROL Adobe Analytics ExperienceEvent field group]**](../../xdm/field-groups/event/analytics-full-extension.md) i ditt schema och använd sedan [`XDM` object ](../commands/sendevent/xdm.md).
* Använd [`data`-objektet ](../commands/sendevent/data.md) för att skicka data till Adobe Analytics utan ett XDM-schema.
* Använd automatiskt genererade [kontextdatavariabler](https://experienceleague.adobe.com/sv/docs/analytics/implementation/vars/page-vars/contextdata) och [bearbetningsregler](https://experienceleague.adobe.com/sv/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## Använd objektet `XDM` {#use-xdm-object}

Om du vill använda ett fördefinierat schema som är specifikt för Adobe Analytics kan du lägga till [Adobe Analytics ExperienceEvent-schemafältgruppen](../../xdm/field-groups/event/analytics-full-extension.md) i ditt schema. När du har lagt till det kan du fylla i schemat med objektet `xdm` i Web SDK för att skicka data till en rapportserie. När data kommer till Edge Network översätts XDM-objektet till ett format som Adobe Analytics förstår.

Det finns två sätt att skicka data till Adobe Analytics via Web SDK:

* [Skicka data till Adobe Analytics med taggtillägget Web SDK](https://experienceleague.adobe.com/sv/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Skicka data till Adobe Analytics med Web SDK JavaScript-biblioteket](https://experienceleague.adobe.com/sv/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Mer information om en fullständig referens till XDM-fält och hur de mappas till Analytics-variabler finns i [Mappning av objektvariabeln XDM till Adobe Analytics](https://experienceleague.adobe.com/sv/docs/analytics/implementation/aep-edge/xdm-var-mapping) i Adobe Analytics implementeringsguide.

## Använd objektet `data` {#use-data-object}

Ett alternativ till att använda XDM-objektet är att använda dataobjektet i stället. Dataobjektet är inriktat på implementeringar som för närvarande använder AppMeasurement, vilket gör uppgraderingen till Web SDK mycket enklare.

Beroende på om du använder AppMeasurement eller Analytics-taggtillägget kan du läsa följande handböcker för mer information om hur du migrerar till Web SDK:

* [Migrera från taggtillägget Adobe Analytics till taggtillägget Web SDK](https://experienceleague.adobe.com/sv/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migrera från AppMeasurement till Web SDK](https://experienceleague.adobe.com/sv/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

I dokumentationen om [dataobjektvariabelmappning till Adobe Analytics](https://experienceleague.adobe.com/sv/docs/analytics/implementation/aep-edge/data-var-mapping) i Adobe Analytics implementeringsguide finns en fullständig referens till dataobjektfält och hur de mappas till Analytics-variabler.

## Använd kontextdatavariabler {#use-context-data-variables}

Alla variabler som inte mappas automatiskt är tillgängliga som [kontextdatavariabler](https://experienceleague.adobe.com/sv/docs/analytics/implementation/vars/page-vars/contextdata). Du kan sedan använda [bearbetningsregler](https://experienceleague.adobe.com/sv/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) för att mappa kontextdatavariabler till analysvariabler. Om du till exempel har ett anpassat XDM-schema som ser ut så här:

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

Då är de här fälten de kontextdatanycklar som är tillgängliga i bearbetningsregelgränssnittet:

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## Vanliga frågor och svar

+++Hur skiljer jag på sidvisningsanrop från länkspårningsanrop i Web SDK?

I AppMeasurementet i Adobe Analytics används separata metodanrop för sidvyer ([`t()` metod ](https://experienceleague.adobe.com/sv/docs/analytics/implementation/vars/functions/t-method)) och länkspårningsanrop ([`tl()` metod ](https://experienceleague.adobe.com/sv/docs/analytics/implementation/vars/functions/tl-method)). Web SDK innehåller i stället bara kommandot [`sendEvent`](../commands/sendevent/overview.md) för att skicka både sidvyer och länkspårning. De data som du inkluderar i en händelse avgör om det är en [sidvy](https://experienceleague.adobe.com/sv/docs/analytics/components/metrics/page-views) eller en [sidhändelse](https://experienceleague.adobe.com/sv/docs/analytics/components/metrics/page-events) i Adobe Analytics.

Som standard betraktas alla händelser som sidvisningar i Adobe Analytics. Om du vill ställa in en Web SDK-händelse på ett Adobe Analytics länkspårningsanrop anger du följande fält:

* **XDM-objekt**: `xdm.web.webInteraction.name`, `web.webInteraction.type` och `web.webInteraction.URL`
* **Dataobjekt**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType` och `data.__adobe.analytics.linkURL`
* **Kontextdata**: Stöds inte

Mer information finns i [`tl()`-metoden ](https://experienceleague.adobe.com/sv/docs/analytics/implementation/vars/functions/tl-method) i Adobe Analytics implementeringsguide.

Om du aktiverar [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) i kommandot `configure` fylls fälten i automatiskt.

+++

+++Hur skiljer en datastream på data från andra tjänster med data som är avsedda för Adobe Analytics?

Alla händelser som skickas till en datastream skickas till alla konfigurerade tjänster. Om du till exempel gör separata anrop för personalisering och analys skickas båda händelserna till Analytics och Target. Dessa händelser registreras i analysrapporter och kan påverka mätvärden som studsfrekvens.

Om du använder Web SDK kombineras dessa anrop vanligtvis i kommandot [`sendEvent`](../commands/sendevent/overview.md).

+++
