---
title: Felsökning
seo-title: Adobe Experience Platform Web SDK-felsökning
description: Lär dig hur du växlar felsökning för Experience Platform Web SDK
seo-description: Lär dig hur du växlar felsökning för Experience Platform Web SDK
keywords: debugging web sdk;debugging;configure;configure command;debug command;edgeConfigId;setDebug;debugEnabled;debug;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Felsökning

När felsökning är aktiverat skickar SDK meddelanden till webbläsarkonsolen som kan vara till hjälp vid felsökning av implementeringen och vid förståelse för hur SDK fungerar. Felsökning resulterar också i en synkron validering på serversidan av data som samlas in mot det schema du har konfigurerat.

Felsökning är inaktiverat som standard, men kan aktiveras på tre olika sätt:

* `configure` kommando
* `setDebug` kommando
* frågesträngsparameter

## Växla felsökning med kommandot Konfigurera

När du konfigurerar SDK med `configure` kommandot aktiverar du felsökning genom att ange `debugEnabled` alternativet till `true`.

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

Växla felsökning med ett separat `debug` kommando enligt följande:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Om du inte vill ändra kod på webbsidan eller inte vill att loggmeddelanden ska skapas för alla användare på webbplatsen, är detta särskilt användbart eftersom du kan köra `debug` kommandot i webbläsarens JavaScript-konsol när som helst.

## Växla felsökning med en frågesträngsparameter

Växla felsökning genom att ange en frågesträngsparameter till `alloy_debug` eller `true` `false` enligt följande:

```HTTP
http://example.com/?alloy_debug=true
```

På samma sätt som `debug` kommandot är det här särskilt användbart om du inte vill ändra kod på webbsidan eller inte vill att loggmeddelanden ska skapas för alla användare på webbplatsen, eftersom du kan ange frågesträngsparametern när du läser in webbsidan i webbläsaren.

## Prioritet och varaktighet

När felsökning ställs in via `debug` kommando- eller frågesträngsparametern åsidosätts alla `debug` alternativ som ställs in med `configure` kommandot. I dessa två fall förblir felsökning aktiverat under hela sessionen. Det innebär att om du aktiverar felsökning med felsökningskommandot eller frågesträngsparametern är den aktiverad tills något av följande:

* Sessionens slut
* Du kör `debug` kommandot
* Du ställer in frågesträngsparametern igen
