---
title: Åtgärdstyper för Edge Extensions
description: Lär dig hur du definierar en biblioteksmodul av åtgärdstyp för ett taggtillägg i en edge-egenskap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Åtgärdstyper för kanttillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

En biblioteksmodul av åtgärdstyp är utformad för att utföra en fördefinierad åtgärd. Effekten av den här åtgärden definieras helt av författaren. Modulen kan skapas som en fyr eller till och med omforma vissa data från händelsen.

>[!IMPORTANT]
>
>Det här dokumentet innehåller åtgärdstyper för kanttillägg. Om du utvecklar ett webbtillägg läser du i guiden om [åtgärdstyper för webbtillägg](../web/action-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i taggtillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

En modul för att vidarebefordra vissa data till en slutpunkt från tredje part kan till exempel se ut så här.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Om du vill göra slutpunkten konfigurerbar av användaren och tillåta indata och beständighet för en slutpunkt till inställningsobjektet i modulen, ser objektet ut ungefär så här.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Om du vill använda den användardefinierade slutpunkten måste modulen ändras till följande exempel.

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Åtgärdsresultat

Resultatet som returneras av en åtgärdsmodul kan vara vad som helst. Om åtgärden behöver utföra en asynkron åtgärd kan du returnera ett [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) som returnerar det resultat du vill ha när åtgärden har löst sig.

Åtgärdsresultatet lagras i en `ruleStash`-nyckel som är tillgänglig för alla moduler via parametern `context` (`context.arc.ruleStash`). Du kan läsa mer om `ruleStash` [här](./context.md#rulestash).
