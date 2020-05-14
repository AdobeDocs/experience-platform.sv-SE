---
title: Skicka data till Adobe Analytics
seo-title: Skicka data till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar data till Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig hur du skickar data till Adobe Analytics med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Skicka data till Adobe Analytics

Adobe Experience Platform Web SDK kan skicka data till Adobe Analytics. Detta fungerar genom att översätta `xdm` till ett format som Adobe Analytics kan använda.

## Inställningar

Adobe Analytics hämtar automatiskt de data som du skickar om du har en rapportsvit mappad i användargränssnittet för kundkonfiguration. Här kan du mappa en eller flera rapporter till en viss konfiguration. När en rapportsvit har mappats börjar data automatiskt flöda.

## Automatiskt mappade data

Adobe Experience Platform Edge Network mappar automatiskt många XDM-variabler. En fullständig lista över automatiskt mappade variabler visas [här](../analytics/automatically-mapped-vars.md).

## Manuellt mappade data

Alla data som samlas in av edge-nätverket kan nås via bearbetningsregler. Data förenklas med punktnotation och är tillgängliga som contextData.

Om du hade ett schema som såg ut så här.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

Då är de kontextdatanycklar som är tillgängliga för dig.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

Här är ett exempel på en bearbetningsregel som skulle använda dessa data.

![Gränssnitt för bearbetningsregler](../../../assets/edge_analytics_processing_rules.png)
