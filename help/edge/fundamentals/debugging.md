---
title: Felsökning i Adobe Experience Platform Web SDK
description: Lär dig hur du växlar felsökningsfunktioner i Experience Platform Web SDK.
keywords: felsöka webb-sdk;felsöka;konfigurera;konfigurera kommando;felsökningskommando;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Felsökning

När felsökning är aktiverat skickar SDK meddelanden till webbläsarkonsolen som kan vara till hjälp vid felsökning av implementeringen och vid förståelse för hur SDK fungerar.

Felsökning är inaktiverat som standard, men kan aktiveras på fyra olika sätt:

* `configure` kommando
* `setDebug` kommando
* frågesträngsparameter
* Växlar på Aktivera felsökning i Adobe Experience Platform Debugger. Adobe Experience Platform är ett kraftfullt verktyg som undersöker dina webbsidor och hjälper dig att felsöka implementeringsproblem med dina Experience Cloud-produkter. Adobe Experience Platform Debugger finns som [Krom](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) tillägg. Felsökning kan aktiveras på konfigurationsfliken i avsnittet AEP Web SDK.

![Användargränssnittsbild för felsökning i Experience Platform visar konfigurationsskärmen.](../assets/enable-debugging.png)

## Växla felsökning med kommandot Konfigurera

När SDK konfigureras med `configure` kommando, aktivera felsökning genom att ställa in `debugEnabled` alternativ till `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Detta aktiverar felsökning för alla användare på webbsidan i stället för bara för din webbläsare.

## Växla felsökning med kommandot Felsökning

Växla felsökning med en separat `debug` enligt följande:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Om du inte vill ändra kod på webbsidan eller inte vill att loggmeddelanden ska skapas för alla användare på webbplatsen är detta särskilt användbart eftersom du kan köra `debug` -kommandot i webbläsarens JavaScript-konsol när som helst.

## Växla felsökning med en frågesträngsparameter

Växla felsökning genom att ställa in en `alloy_debug` frågesträngsparameter till `true` eller `false` enligt följande:

```HTTP
http://example.com/?alloy_debug=true
```

Liknar `debug` om du inte vill ändra kod på webbsidan eller inte vill att loggmeddelanden ska skapas för alla användare på webbplatsen, är detta särskilt användbart eftersom du kan ange frågesträngsparametern när du läser in webbsidan i webbläsaren.

## Prioritet och varaktighet

När felsökning ställs in via `debug` kommando- eller frågesträngsparameter, åsidosätter den `debug` i `configure` -kommando. I dessa två fall förblir felsökning aktiverat under hela sessionen. Det innebär att om du aktiverar felsökning med felsökningskommandot eller frågesträngsparametern är den aktiverad tills något av följande:

* Sessionens slut
* Du kör `debug` kommando
* Du ställer in frågesträngsparametern igen

## Hämtar biblioteksinformation

Det är ofta praktiskt att komma åt en del av informationen bakom biblioteket som du har laddat in på din webbplats. Om du vill göra det kör du `getLibraryInfo` enligt följande:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

För närvarande, `libraryInfo` -objektet innehåller följande egenskaper:

* `version`: Det här är versionen av det inlästa biblioteket. Om t.ex. versionen av biblioteket som läses in var 1.0.0 blir värdet `1.0.0`. När biblioteket körs inuti taggtillägget (med namnet&quot;AEP Web SDK&quot;) är versionen biblioteksversionen och taggtilläggsversionen som är kopplad till ett plustecken (+). Om biblioteksversionen till exempel är 1.0.0 och taggtilläggets version är 1.2.0, blir värdet 1.0 `1.0.0+1.2.0`.
* `commands`: Alla tillgängliga kommandon stöds av det inlästa biblioteket.
* `configs`: Dessa är alla aktuella konfigurationer i det inlästa biblioteket.
