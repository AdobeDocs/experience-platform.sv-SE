---
title: Skicka data till Adobe Analytics
seo-title: Skicka data till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar data till Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig hur du skickar data till Adobe Analytics med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Skicka data till Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kan skicka data till Adobe Analytics. Detta fungerar genom att konvertera `xdm` till ett format som Adobe Analytics kan använda.

## Inställningar

Adobe Analytics hämtar automatiskt de data som du skickar om du har en rapportsvit mappad i användargränssnittet för kundkonfiguration. Här kan du mappa en eller flera rapporter till en viss konfiguration. När en rapportsvit har mappats börjar data automatiskt flöda.

## Automatiskt mappade data

Adobe Experience Platform mappar [!DNL Edge Network] automatiskt många XDM-variabler. En fullständig lista över automatiskt mappade variabler visas [här](../analytics/automatically-mapped-vars.md).

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

Då är de kontextdatanycklar som är tillgängliga för dig.

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

Här är ett exempel på en bearbetningsregel som skulle använda dessa data.

![Gränssnitt för bearbetningsregler](../../../assets/edge_analytics_processing_rules.png)
