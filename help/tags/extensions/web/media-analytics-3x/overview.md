---
title: Adobe Media Analytics (3.x SDK) for Audio and Video Extension Overview
description: Läs mer om taggtillägget Adobe Media Analytics (3.x SDK) för ljud och video i Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Adobe Media Analytics (3.x SDK) for Audio and Video extension overview

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Använd den här dokumentationen om du vill ha information om hur du installerar, konfigurerar och implementerar Adobe Media Analytics (3.x SDK) för Audio- och Video-tillägg (Media Analytics-tillägg). Här finns alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel, tillsammans med exempel och länkar till exempel.

Tillägget Media Analytics (MA) lägger till JavaScript Media SDK (Media 3.x SDK). Det här tillägget innehåller funktioner för att lägga till `Media`-spårarinstansen till en tagghanterad plats eller ett tagghanterat projekt. MA-tillägget kräver ytterligare två tillägg:

* [Analystillägg](../analytics/overview.md)
* [Experience Cloud ID-tillägg](../id-service/overview.md)

>[!IMPORTANT]
>
>Det här tillägget distribueras med Media 3.x SDK, som inte är bakåtkompatibelt med Media 2.x SDK. Om sidan redan använder Media 2.x SDK ska du använda [Adobe Media Analytics for Audio and Video Extension](../media-analytics/overview.md) i stället för det här tillägget.

När du har inkluderat alla tre av de tillägg som nämns ovan i det tagghanterade projektet kan du fortsätta på ett av två sätt:

* Använd `Media` API:er från webbprogrammet
* Inkludera, eller bygg, ett spelarspecifikt tillägg som mappar specifika mediespelarhändelser till API:erna i `Media`-spårarinstansen. Den här instansen visas genom MA-tillägget.

## Installera och konfigurera MA-tillägget

* **Installera:** Om du vill installera MA-tillägget öppnar du tilläggsegenskapen, markerar  **[!UICONTROL Extensions > Catalog]**, håller pekaren över  **[!UICONTROL Adobe Media Analytics (3.x SDK) for Audio and Video]** tillägget och väljer  **[!UICONTROL Install]**.

* **Konfigurera:** Om du vill konfigurera MA-tillägget öppnar du  [!UICONTROL Extensions] fliken, håller pekaren över tillägget och väljer  **[!UICONTROL Configure]**:

![Konfiguration av MA-tillägg](../../../images/ext-ma-config.png)

### Konfigurationsalternativ:

| Alternativ | Beskrivning |
| :--- | :--- |
| Collection API Server | Definierar API-servern för mediainsamling (kontakta Adobe för att få tillgång till den här servern) |
| Programversion | Versionen av mediespelarappen/SDK |
| Spelarnamn | Namnet på den mediespelare som används (t.ex. &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Kanal | Egenskapen Kanalnamn |
| Felsökningsloggning | Aktivera eller inaktivera loggning |
| Aktivera SSL | Aktivera eller inaktivera sändning av ping via HTTPS |
| Exportera API:er till Window-objekt | Aktivera eller inaktivera export av Media Analytics-API:er till globalt omfång |
| Variabelnamn | En variabel som du använder för att exportera Media Analytics-API:er under `window`-objektet |

**Påminnelse:** För MA-tillägget krävs  [](../analytics/overview.md) Analytics och  [Experience Cloud ](../id-service/overview.md) IDextensions. Du måste också lägga till dessa tillägg i tilläggsegenskapen och konfigurera dem.

## Använda MA-tillägget

### Använda från en webbsida/JS-app

MA-tillägget exporterar medie-API:erna i det globala fönsterobjektet genom att aktivera inställningen &quot;Exportera API:er till fönsterobjekt&quot; på sidan [!UICONTROL Configuration]. Den exporterar API:erna under det konfigurerade variabelnamnet. Om till exempel variabelnamnet är konfigurerat till `ADB` kan Media API:er nås av `window.ADB.Media`.

>[!IMPORTANT]
>
>MA-tillägget exporterar bara API:erna när `window["CONFIGURED_VARIABLE_NAME"]` är odefinierat och inte åsidosätter befintliga variabler.

1. **Media-API:er:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Detta visar alla API:er och konstanter från Media SDK: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **Skapa mediespårarinstans:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **Returvärde:** En  `Media` spårningsinstans för att spåra en mediesession.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. Använd Media Tracker-instansen och följ [JS API-dokumentationen](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) för att implementera mediespårning.

Du kan hämta exempelspelaren här: [Exempelspelare för MA](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). Exempelspelaren fungerar som en referens för att visa hur man använder MA-tillägget för att stödja Media Analytics direkt från en webbapp.


### Använda från andra tillägg

MA-tillägget visar `media` som en delad modul för andra tillägg. (Mer information om delade moduler finns i [Dokumentation för delade moduler](https://developer.adobelaunch.com/extensions/shared_modules/).)

>[!IMPORTANT]
>
>Delade moduler kan bara nås från andra tillägg. Det innebär att en webbsida/JavaScript-app inte kan komma åt de delade modulerna eller använda `turbine` (se kodexempel nedan) utanför ett tillägg.

1. **Media-API:er:** `media` delad modul

   Detta visar alla API:er och konstanter från Media SDK: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Skapa Media Tracker-instansen enligt följande:

   **Returvärde:** En  `Media` spårningsinstans för att spåra en mediesession.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. Använd Media Tracker-instansen och följ [JS API-dokumentationen](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) för att implementera mediespårning.

>[!NOTE]
>
>**Testa:** För den här versionen måste du överföra tillägget till  [Platform](../../../extension-dev/submit/upload-and-test.md), där du har tillgång till alla beroende tillägg, för att testa tillägget.
