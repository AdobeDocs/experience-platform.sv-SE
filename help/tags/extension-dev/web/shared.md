---
title: Delade moduler i webbtillägg
description: Lär dig hur du definierar delade biblioteksmoduler för webbtillägg i Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Delade moduler i webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

En delad modul är en mekanism som du kan använda för att kommunicera med andra tillägg. Tillägg A kan till exempel läsa in en datadel asynkront och göra den tillgänglig för tillägg B via ett [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

I JavaScript-implementeringar instansieras alla delade moduler med metoden [`getSharedModule`](../turbine.md#shared) som finns i den kostnadsfria variabeln `turbine`.

Delade moduler inkluderas i taggbibliotek även när de aldrig anropas inifrån andra tillägg. Om du inte vill öka biblioteksstorleken i onödan bör du vara försiktig med vad du visar som en delad modul.

Delade moduler har ingen vykomponent.

När du utvecklar ett eget taggtillägg kan du definiera de delade moduler som du vill att det ska innehålla. Du kan till exempel skapa en modul som läser in ett användar-ID asynkront och sedan delar användar-ID med andra tillägg via ett löfte:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

I [tilläggsmanifestet](../manifest.md) måste du ange ett namn för den här delade modulen. Om du namnger den `user-id-promise` kan ett annat tillägg få åtkomst till den delade modulen enligt följande:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

Delade moduler kan vara vad som helst som du vanligtvis kan exportera från en CommonJS-modul (till exempel funktioner, objekt, strängar, tal eller booleska värden).
