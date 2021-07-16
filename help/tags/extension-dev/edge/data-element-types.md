---
title: Dataelementtyper för Edge-tillägg
description: Lär dig hur du definierar en biblioteksmodul av typen data-element för ett taggtillägg i en edge-egenskap.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Dataelementtyper i edge-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

En biblioteksmodul av typen data-element hämtar en datadel. Modulförfattaren bestämmer hur data hämtas. Du kan t.ex. använda en dataelementtyp för att tillåta Adobe Experience Platform-användare att hämta data från XDM-lagret eller deras anpassade datalager.

>[!IMPORTANT]
>
>Det här dokumentet innehåller dataelementtyper för kanttillägg. Om du utvecklar ett webbtillägg läser du i guiden om [dataelementtyper för webbtillägg](../web/data-element-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i taggtillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

Om du vill att användarna ska kunna hämta data från det anpassade datalagret kan modulen se ut som i det här exemplet.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Om du vill att de data som returneras för datalagret ska kunna konfigureras av Adobe Experience Platform-användaren, kan du tillåta att användaren anger ett nyckelnamn och sedan spara namnet till `settings`-objektet. Objektet kan se ut ungefär så här.

```js
{
  keyName: "campaignId"
}
```

Om du vill använda det användardefinierade lokala lagringsobjektnamnet måste modulen ändras till följande:

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## Kontext för modulen Bibliotek

Alla dataelementmoduler har åtkomst till en `context`-variabel som anges när modulen anropas. Du kan läsa mer [här](./context.md).
