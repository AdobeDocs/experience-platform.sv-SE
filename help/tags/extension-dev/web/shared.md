---
title: Delade moduler i webbtillägg
description: Lär dig definiera delade biblioteksmoduler för webbtillägg i Adobe Experience Platform.
exl-id: ec013a39-966c-43f3-bc36-31198990a17e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Delade moduler i webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

En delad modul är en mekanism som du kan använda för att kommunicera med andra tillägg. Tillägg A kan till exempel läsa in en datadel asynkront och göra den tillgänglig för tillägg B via ett [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

I JavaScript-implementeringar instansieras alla delade moduler med metoden [`getSharedModule`](../turbine.md#shared) som tillhandahålls av den kostnadsfria variabeln `turbine`.

Delade moduler inkluderas i taggbibliotek även när de aldrig anropas inifrån andra tillägg. Om du inte vill öka biblioteksstorleken i onödan bör du vara försiktig med vad du visar som en delad modul.

Delade moduler har ingen vykomponent.

När du utvecklar ett eget taggtillägg kan du definiera de delade moduler som du vill att det ska innehålla. Du kan till exempel skapa en modul som läser in ett användar-ID asynkront och sedan delar användar-ID med andra tillägg via ett löfte:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

I [tilläggsmanifestet](../manifest.md) måste du ange ett namn för den här delade modulen. Om du namnger den `user-id-promise` kan ett annat tillägg få åtkomst till den här delade modulen enligt följande:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Delade moduler kan vara vad som helst som du vanligtvis kan exportera från en CommonJS-modul (till exempel funktioner, objekt, strängar, tal eller booleska värden).
