---
title: Åtgärdstyper för Edge Extensions
description: Lär dig hur du definierar en biblioteksmodul av åtgärdstyp för ett taggtillägg i en edge-egenskap.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Åtgärdstyper för kanttillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

I en taggregel är en åtgärd en åtgärd som utförs efter att regelvillkoren har utvärderats. Åtgärdstyper tillhandahålls av tillägg, och deras effekter definieras helt av tilläggsförfattaren.

Ett tillägg kan till exempel innehålla en&quot;show support chat&quot;-åtgärdstyp som kan visa en supportchattdialogruta för att hjälpa användare som kan ha problem med utcheckningen.

Det här dokumentet beskriver hur du definierar åtgärdstyper för ett kanttillägg i Adobe Experience Platform.

>[!IMPORTANT]
>
>Om du utvecklar ett webbtillägg läser du i handboken om [åtgärdstyper för webbtillägg](../web/action-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i kanttillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

Åtgärdstyper består vanligtvis av följande:

1. En vy som visas i användargränssnittet för Experience Platform och datainsamling där användare kan ändra inställningar för åtgärden.
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

Resultatet som returneras av en åtgärdsmodul kan vara vad som helst. Om åtgärden behöver köra en asynkron aktivitet kan du returnera ett [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) som returnerar det resultat du vill ha när åtgärden har lösts.

Åtgärdsresultatet lagras i en `ruleStash`-nyckel som är tillgänglig för alla moduler via parametern `context` (`context.arc.ruleStash`). Du kan läsa mer om `ruleStash` [här](./context.md#rulestash).
