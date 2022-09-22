---
title: Åtgärdstyper för Edge Extensions
description: Lär dig hur du definierar en biblioteksmodul av åtgärdstyp för ett taggtillägg i en edge-egenskap.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Åtgärdstyper för kanttillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

I en taggregel är en åtgärd en åtgärd som utförs efter att regelvillkoren har utvärderats. Åtgärdstyper tillhandahålls av tillägg, och deras effekter definieras helt av tilläggsförfattaren.

Ett tillägg kan till exempel innehålla en&quot;show support chat&quot;-åtgärdstyp som kan visa en supportchattdialogruta för att hjälpa användare som kan ha problem med utcheckningen.

Det här dokumentet beskriver hur du definierar åtgärdstyper för ett kanttillägg i Adobe Experience Platform.

>[!IMPORTANT]
>
>Om du utvecklar ett webbtillägg läser du i handboken [åtgärdstyper för webbtillägg](../web/action-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i kanttillägg. Om du behöver en introduktion kan du se översikten på [formatering av biblioteksmodul](./format.md) innan du återgår till den här guiden.

Åtgärdstyper består vanligtvis av följande:

1. En vy som visas i användargränssnittet för datainsamling där användarna kan ändra inställningarna för åtgärden.
2. En biblioteksmodul som skickas i taggens körningsbibliotek för att tolka inställningarna och utföra en åtgärd.

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

Resultatet som returneras av en åtgärdsmodul kan vara vad som helst. Om åtgärden behöver köra en asynkron åtgärd kan du returnera en [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) som returnerar det resultat du vill ha när det har lösts.

Åtgärdsresultatet sparas i en `ruleStash` som är tillgänglig för alla moduler via `context` parameter (`context.arc.ruleStash`). Du kan lära dig mer om `ruleStash` [här](./context.md#rulestash).
