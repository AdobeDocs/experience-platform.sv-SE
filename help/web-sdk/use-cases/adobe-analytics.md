---
title: Skicka data till Adobe Analytics med Web SDK
description: Lär dig skicka data till Adobe Analytics med Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;mapped data;mapped vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Skicka data till Adobe Analytics via Web SDK

Adobe Experience Platform Web SDK kan skicka data till Adobe Analytics via Adobe Experience Platform Edge Network. När data kommer till Edge Network översätts XDM-objektet till ett format som Adobe Analytics förstår.

## XDM-fältgrupp

För att göra det enklare att hämta de vanligaste Adobe Analytics-mätvärdena har Adobe en fältgrupp som är anpassad efter Adobe Analytics och som du kan använda. Mer information om schemat finns i [Schemafältgruppen Adobe Analytics ExperienceEvent Full Extension](/help/xdm/field-groups/event/analytics-full-extension.md).

## Variabelmappning

Edge Network mappar automatiskt många XDM-variabler. Se [Variabelmappning för analys i Edge Network](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html) i Adobe Analytics implementeringsguide för en omfattande variabellista med automatiskt mappade variabler.

Alla variabler som inte mappas automatiskt är tillgängliga som [Sammanhangsdatavariabler](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=sv). Du kan sedan använda [Bearbetar regler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) för att mappa kontextdatavariabler till analysvariabler. Om du till exempel har ett anpassat XDM-schema som ser ut så här:

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Då är de kontextdatanycklar som är tillgängliga i bearbetningsregelgränssnittet:

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Med Edge Network-samlingen skickas alla händelser till Analytics och alla andra tjänster som du har konfigurerat för din datastream. Om du till exempel har både Analytics och Target konfigurerade som tjänster och du gör separata anrop för personalisering och för Analytics, skickas båda händelserna till Analytics och Target. Dessa händelser registreras i analysrapporter och kan påverka mätvärden som studsfrekvens.

## Sidvyer och länkspårningsanrop

I AppMeasurementet i Adobe Analytics används separata metodanrop för sidvyer ([`t()` method](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) och länkspårningsanrop ([`tl()` method](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). Web SDK innehåller i stället bara [`sendEvent`](../commands/sendevent/overview.md) för att skicka både sidvyer och länkspårning. De data som du inkluderar i en händelse avgör om det är ett [sidvy](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html) eller en [sidhändelse](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) i Adobe Analytics.

Som standard betraktas alla händelser som sidvisningar i Adobe Analytics. Om du vill ställa in en Web SDK-händelse på ett Adobe Analytics länkspårningsanrop anger du följande XDM-fält:

* **`web.webInteraction.URL`**: Länk-URL.
* **`web.webInteraction.name`**: Namnet på den anpassade länken, länken Hämta eller länkdimensionen Avsluta, beroende på värdet i `web.webInteraction.type`
* **`web.webInteraction.type`**: Bestämmer vilken typ av länk som klickas. Giltiga värden är `other` (Anpassade länkar), `download` (Hämta länkar) och `exit` (Avsluta länkar).

Om du aktiverar [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) i `configure` så fylls dessa XDM-fält i automatiskt.
