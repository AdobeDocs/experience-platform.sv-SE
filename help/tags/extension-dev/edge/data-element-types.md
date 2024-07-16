---
title: Dataelementtyper för Edge-tillägg
description: Lär dig hur du definierar en biblioteksmodul av typen data-element för ett taggtillägg i en edge-egenskap.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Dataelementtyper i edge-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

I taggar är dataelement alias för datadelar på en webb- eller mobilsida, oavsett var dessa data finns i händelsen som servern tar emot. Ett dataelement kan refereras av regler och fungerar som en abstraktion för att komma åt dessa datadelar. När platsen för data ändras i framtiden (till exempel när händelsenyckeln som innehåller värdet ändras) kan ett enskilt dataelement konfigureras om medan alla regler som refererar till det dataelementet kan förbli oförändrade.

Dataelementtyperna tillhandahålls av tillägg och tilläggsförfattaren bestämmer hur informationen hämtas. Du kan t.ex. använda en dataelementtyp för att tillåta Adobe Experience Platform-användare att hämta data från XDM-lagret eller deras anpassade datalager.

Det här dokumentet beskriver hur du definierar dataelementtyper för ett kanttillägg i Adobe Experience Platform.

>[!IMPORTANT]
>
>Om du utvecklar ett webbtillägg läser du i handboken om [dataelementtyper för webbtillägg](../web/data-element-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i kanttillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

Dataelementtyper består vanligtvis av följande:

1. En vy som visas i användargränssnittet för Experience Platform och datainsamling där användare kan ändra inställningar för dataelementet.
2. En biblioteksmodul som skickas i taggens körningsbibliotek för att tolka inställningarna och hämta data.

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
