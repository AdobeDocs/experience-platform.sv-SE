---
title: Mappa Adobe Analytics-variabler manuellt i Adobe Experience Platform Web SDK
description: Lär dig hur du manuellt mappar variabler till Adobe Analytics med bearbetningsregler i Experience Platform Web SDK.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;xdm;schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Mappa variabler manuellt i Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kan mappa vissa variabler automatiskt, men anpassade variabler måste mappas manuellt.

För XDM-data som inte automatiskt mappas till [!DNL Analytics]kan du använda [kontextdata](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=sv) för att matcha [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html). Sedan kan den mappas till [!DNL Analytics] använda [bearbetningsregler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) fylla i [!DNL Analytics] variabler.

Du kan också använda en standarduppsättning med åtgärder och produktlistor för att skicka eller hämta data med Adobe Experience Platform Web SDK. Om du vill göra det läser du [Samla in information om handel och produkter](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Kontextdata

Ska användas av [!DNL Analytics], förenklas XDM-data med punktnotation och blir tillgängliga som `contextData`. I följande lista med värdepar visas ett exempel på vad `context data` ser ut som när den förenklas:

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

## Bearbetar regler

Alla data som samlas in via edge-nätverket kan nås via [bearbetningsregler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). I [!DNL Analytics]kan du använda bearbetningsregler för att lägga in kontextdata i [!DNL Analytics] variabler.

I följande regel är Adobe Analytics inställt på att fylla i **Interna söktermer (eVar2)** med data som är kopplade till **a.x._atag.search.term(Context Data)**.

![Användargränssnittsbild för analys visar ett regelexempel.](assets/examplerule.png)

## XDM-schema

Adobe Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data. [!DNL Analytics] kontextdata fungerar med den struktur som definieras av schemat.

I följande exempel visas hur [`event` kommando](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html) kan användas med `xdm` möjlighet att skicka och hämta data med Adobe Experience Platform Web SDK. I det här exemplet `event` kommandot matchar [Schema för handelsinformation för ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) så att productListItems `name` och `SKU` värden spåras:


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

Mer information om hur du spårar händelser med Adobe Experience Platform [!DNL Web SDK], se [Spåra händelser](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html).
