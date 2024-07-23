---
title: Felsökningsmetoder
description: Lär dig hur du växlar felsökningsfunktioner i Web SDK.
keywords: felsöka webb-sdk;felsöka;felsökningskommando;setDebug;debugEnabled;debug
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Felsökningsmetoder

När felsökning är aktiverat skickar Web SDK meddelanden till webbläsarkonsolen som kan vara till hjälp vid felsökning av implementeringen. Felsökning är värdefullt när du vill förstå hur SDK fungerar enligt de regler och dataelement som du har etablerat.

Felsökning är som standard inaktiverat, men kan aktiveras på fyra olika sätt. Du kan använda vilken kombination som helst av dessa metoder för att aktivera eller inaktivera felsökning som passar ditt utvecklingsarbetsflöde bäst.

## Använd `debugEnabled` i kommandot `configure`

Ange det booleska värdet `debugEnabled` som true när tillägget konfigureras. Det här alternativet används vanligtvis för utvecklingsmiljöer, eftersom det möjliggör felsökning för alla som besöker en sida på webbplatsen:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

Mer information finns i [`debugEnabled`](../commands/configure/debugenabled.md).

## Använd kommandot `setDebug`

På samma sätt som ovanstående booleska uttryck aktiverar det här kommandot felsökning för alla besökare på sidan.

```js
alloy("setDebug", {"enabled": true});
```

Mer information finns i kommandot [`setDebug`](../commands/setdebug.md).

## Ange en frågesträngsparameter

Du kan aktivera felsökning genom att lägga till frågesträngen `?alloy_debug=true` i slutet av valfri URL. Exempel:

`http://example.com/?alloy_debug=true`

Den här metoden gäller bara din lokala dator, vilket gör att du kan felsöka produktionsplatser utan att aktivera felsökning för alla. Aktivering av felsökning på det här sättet är fortfarande aktiverat under resten av webbläsarsessionen eller tills du inaktiverar den.

## Använd Adobe Experience Platform Debugger

Adobe Experience Platform Debugger är ett kraftfullt verktyg som undersöker dina webbsidor och hjälper dig att felsöka implementeringen av Experience Cloud-produkter. Du kan aktivera felsökning på konfigurationsfliken i avsnittet AEP Web SDK.

![Aktivera felsökning](../assets/enable-debugging.png)

Mer information finns i [Översikt över Adobe Experience Platform Debugger](/help/debugger/home.md).
