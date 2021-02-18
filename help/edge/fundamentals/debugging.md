---
title: Felsökning i Adobe Experience Platform Web SDK
description: Lär dig hur du växlar felsökningsfunktioner i Experience Platform Web SDK.
keywords: felsöka webb-sdk;felsöka;konfigurera;konfigurera kommando;felsökningskommando;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Felsökning

När felsökning är aktiverat skickar SDK meddelanden till webbläsarkonsolen som kan vara till hjälp vid felsökning av implementeringen och vid förståelse för hur SDK fungerar. Felsökning resulterar också i en synkron validering på serversidan av data som samlas in mot det schema du har konfigurerat.

Felsökning är inaktiverat som standard, men kan aktiveras på tre olika sätt:

* `configure` kommando
* `setDebug` kommando
* frågesträngsparameter

## Växla felsökning med kommandot Konfigurera

När du konfigurerar SDK med kommandot `configure` aktiverar du felsökning genom att ange alternativet `debugEnabled` till `true`.

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

Växla felsökning med ett separat `debug`-kommando enligt följande:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Om du inte vill ändra kod på webbsidan eller inte vill att loggmeddelanden ska skapas för alla användare på webbplatsen är detta särskilt användbart eftersom du kan köra kommandot `debug` i webbläsarens JavaScript-konsol när som helst.

## Växla felsökning med en frågesträngsparameter

Växla felsökning genom att ställa in en `alloy_debug`-frågesträngsparameter på `true` eller `false` enligt följande:

```HTTP
http://example.com/?alloy_debug=true
```

Precis som kommandot `debug` är det särskilt användbart om du inte vill ändra kod på webbsidan eller inte vill att loggmeddelanden ska skapas för alla användare på webbplatsen, eftersom du kan ange frågesträngsparametern när du läser in webbsidan i webbläsaren.

## Prioritet och varaktighet

När felsökning ställs in via kommandot `debug` eller frågesträngsparametern åsidosätts alla alternativ som har angetts för `debug` i kommandot `configure`. I dessa två fall förblir felsökning aktiverat under hela sessionen. Det innebär att om du aktiverar felsökning med felsökningskommandot eller frågesträngsparametern är den aktiverad tills något av följande:

* Sessionens slut
* Du kör kommandot `debug`
* Du ställer in frågesträngsparametern igen

## Hämtar biblioteksinformation

Det är ofta praktiskt att komma åt en del av informationen bakom biblioteket som du har laddat in på din webbplats. Om du vill göra det kör du kommandot `getLibraryInfo` enligt följande:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

För närvarande innehåller det angivna `libraryInfo`-objektet följande egenskaper:

* `version` Det här är versionen av det inlästa biblioteket. Om t.ex. versionen av biblioteket som läses in var 1.0.0 är värdet `1.0.0`.
