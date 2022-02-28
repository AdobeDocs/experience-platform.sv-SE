---
title: Använda Adobe Analytics med Platform Web SDK
description: Lär dig hur du skickar data till Adobe Analytics med Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;mapped data;mapped vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 45becec3b198821e38afbc21fe42a8901e352888
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Använda Adobe Analytics med Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] kan skicka data till Adobe Analytics. Detta fungerar genom översättning `xdm` till ett format som Adobe Analytics kan använda.

## Inställningar

Adobe Analytics hämtar automatiskt de data som du skickar om du har en rapportsvit mappad i användargränssnittet för kundkonfiguration. Här kan du mappa en eller flera rapporter till en viss konfiguration. När en rapportsvit har mappats börjar data automatiskt flöda.

## Automatiskt mappade data

Adobe Experience Platform [!DNL Edge Network] mappar automatiskt många XDM-variabler. En fullständig lista över dessa variabler finns [här](automatically-mapped-vars.md).

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

![Gränssnitt för bearbetningsregler](./assets/edge_analytics_processing_rules.png)
