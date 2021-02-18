---
title: Mappa Adobe Analytics-variabler manuellt i Adobe Experience Platform Web SDK
description: Lär dig hur du manuellt mappar variabler till Adobe Analytics med bearbetningsregler i Experience Platform Web SDK.
seo-description: Mappa variabler manuellt till Adobe Analytics med bearbetningsregler med Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Mappa variabler manuellt i Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kan mappa vissa variabler automatiskt, men anpassade variabler måste mappas manuellt.

För XDM-data som inte automatiskt mappas till [!DNL Analytics] kan du använda [kontextdata](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/contextdata.html) för att matcha ditt [schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html). Sedan kan den mappas till [!DNL Analytics] med [bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) för att fylla i [!DNL Analytics]-variabler.

Du kan också använda en standarduppsättning med åtgärder och produktlistor för att skicka eller hämta data med Adobe Experience Platform Web SDK. Mer information finns i [Produkter](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Kontextdata

XDM-data som ska användas av [!DNL Analytics] förenklas med punktnotation och görs tillgängliga som `contextData`. I följande lista över värdepar visas ett exempel på `context data`:

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## Behandlingsregler

Alla data som samlas in av edge-nätverket kan nås via [bearbetningsregler](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). I [!DNL Analytics] kan du använda bearbetningsregler för att införliva kontextdata i [!DNL Analytics]-variabler.

I följande regel är Adobe Analytics till exempel inställt på att fylla i **interna söktermer (eVar2)** med data som är associerade med **a.x._atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM-schema

Adobe Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data. [!DNL Analytics] kontextdata fungerar med den struktur som definieras av schemat.

I följande exempel visas hur kommandot [`event`](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) kan användas med alternativet `xdm` för att skicka och hämta data med Adobe Experience Platform Web SDK. I det här exemplet matchar kommandot `event` schemat [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) så att värdena productListItems `name` och `SKU` spåras:


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

Mer information om att spåra händelser med Adobe Experience Platform [!DNL Web SDK] finns i [Spåra händelser](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
