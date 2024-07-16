---
title: Installera Web SDK med NPM-paketet
description: Använd ett NPM-paket för att installera och referera till Web SDK-biblioteket.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Installera Web SDK med NPM-paketet

Adobe Experience Platform Web SDK är tillgängligt som ett [NPM-paket](https://www.npmjs.com). Genom att installera NPM-paketet får du kontroll över byggprocessen för Adobe Experience Platform Web SDK JavaScript-biblioteket. NPM-paketet visar EcmaScript version 5-moduler eller EcmaScript version 2015-moduler (ES6) som ska köras i webbläsaren.

```bash
npm install @adobe/alloy
```

NPM-paketet för Adobe Experience Platform Web SDK visar en `createInstance`-funktion. Namnalternativet som skickas till funktionen styr det prefix som används vid loggning. Nedan finns exempel på hur du använder paketet.

## Använda paketet som en ECMAScript 2015-modul (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM-paketet är beroende av CommonJS-moduler, och när du använder ett paket måste du därför se till att paketet har stöd för CommonJS-moduler. Vissa paketerare, till exempel [Rollup](https://rollupjs.org), kräver ett [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) som har stöd för CommonJS.

## Använda paketet som en ECMAScript 5-modul

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
