---
title: Felsökningsmetoder
description: Lär dig hur du växlar felsökningsfunktioner i Web SDK.
keywords: felsöka webb-sdk;felsöka;konfigurera;konfigurera kommando;felsökningskommando;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Felsökningsmetoder

När felsökning är aktiverat skickar Web SDK meddelanden till webbläsarkonsolen som kan vara till hjälp vid felsökning av implementeringen. Felsökning är värdefullt när du vill förstå hur SDK fungerar enligt de regler och dataelement som du har etablerat.

Felsökning är som standard inaktiverat, men kan aktiveras på fyra olika sätt. Du kan använda vilken kombination som helst av dessa metoder för att aktivera eller inaktivera felsökning som passar ditt utvecklingsarbetsflöde bäst.

## Använd `debugEnabled` i `configure` kommando

Ange `debugEnabled` boolesk till true när tillägget konfigureras. Det här alternativet används vanligtvis för utvecklingsmiljöer, eftersom det möjliggör felsökning för alla som besöker en sida på webbplatsen:

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

Se [`debugEnabled`](../commands/configure/debugenabled.md) för mer information.

## Använd `setDebug` kommando

På samma sätt som ovanstående booleska uttryck aktiverar det här kommandot felsökning för alla besökare på sidan.

```js
alloy("setDebug", {"enabled": true});
```

Se [`setDebug`](../commands/setdebug.md) för mer information.

## Ange en frågesträngsparameter

Du kan aktivera felsökning genom att lägga till frågesträngen `?alloy_debug=true` till slutet av en URL. Exempel:

`http://example.com/?alloy_debug=true`

Den här metoden gäller bara din lokala dator, vilket gör att du kan felsöka produktionsplatser utan att aktivera felsökning för alla. Aktivering av felsökning på det här sättet är fortfarande aktiverat under resten av webbläsarsessionen eller tills du inaktiverar den.

## Använd Adobe Experience Platform Debugger

Adobe Experience Platform Debugger är ett kraftfullt verktyg som undersöker dina webbsidor och hjälper dig att felsöka implementeringen av Experience Cloud-produkter. Du kan aktivera felsökning på konfigurationsfliken i avsnittet AEP Web SDK.

![Aktivera felsökning](../assets/enable-debugging.png)

Se [Adobe Experience Platform Debugger - översikt](/help/debugger/home.md) för mer information.
