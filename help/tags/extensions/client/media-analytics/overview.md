---
title: Adobe Media Analytics for Audio and Video Extension - översikt
description: Läs om taggtillägget Adobe Media Analytics för ljud och video i Adobe Experience Platform.
exl-id: 426cfd08-aead-4b35-824c-45494bca2fc8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 5%

---

# Adobe Media Analytics for Audio and Video extension overview

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Använd den här dokumentationen för information om hur du installerar, konfigurerar och implementerar Adobe Media Analytics för ljud- och videotillägg (tillägget Media Analytics). Här finns alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel, tillsammans med exempel och länkar till exempel.

Media Analytics-tillägget (MA) lägger till JavaScript Media SDK (Media 2.x SDK). Det här tillägget innehåller funktioner för att lägga till spårningsinstansen `MediaHeartbeat` till en taggplats eller ett -projekt. MA-tillägget kräver ytterligare två tillägg:

* [Analystillägg](../analytics/overview.md)
* [Experience Cloud ID-tillägg](../id-service/overview.md)

>[!IMPORTANT]
>
>Ljudspårning kräver Analytics Extension v1.6 eller senare.

När du har inkluderat alla tre av tilläggen som nämns ovan i taggprojektet kan du fortsätta på ett av två sätt:

* Använd `MediaHeartbeat` API:er från ditt webbprogram
* Inkludera, eller bygg, ett spelarspecifikt tillägg som mappar specifika mediespelarhändelser till API:erna på spårningsinstansen `MediaHeartbeat`. Den här instansen visas genom MA-tillägget.

## Installera och konfigurera MA-tillägget

* **Installera -** Om du vill installera MA-tillägget öppnar du tilläggsegenskapen, väljer **[!UICONTROL Extensions > Catalog]**, håller pekaren över **[!UICONTROL Adobe Media Analytics for Audio and Video]**-tillägget och väljer **[!UICONTROL Install]**.

* **Konfigurera -** Om du vill konfigurera MA-tillägget öppnar du fliken [!UICONTROL Extensions], hovrar över tillägget och väljer **[!UICONTROL Configure]**:

![Konfiguration av MA-tillägg](../../../images/ext-va-config.jpg)

### Konfigurationsalternativ:

| Alternativ | Beskrivning |
| :--- | :--- |
| Spårningsserver | Definierar servern för spårning av mediefärger (detta är inte samma server som analysspårningsservern) |
| Programversion | Versionen av mediespelarappen/SDK |
| Spelarnamn | Namnet på den mediespelare som används (t.ex. &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Kanal | Egenskapen Kanalnamn |
| Onlinevideoprovider | Namnet på onlinevideoplattformen som innehållet distribueras via |
| Felsökningsloggning | Aktivera eller inaktivera loggning |
| Aktivera SSL | Aktivera eller inaktivera sändning av ping via HTTPS |
| Exportera API:er till Window-objekt | Aktivera eller inaktivera export av Media Analytics-API:er till globalt omfång |
| Variabelnamn | En variabel som du använder för att exportera Media Analytics-API:er under objektet `window` |

**Påminnelse:** För MA-tillägget krävs tilläggen [Analytics](../analytics/overview.md) och [Experience Cloud ID](../id-service/overview.md). Du måste också lägga till dessa tillägg i tilläggsegenskapen och konfigurera dem.

## Använda MA-tillägget

### Använda från en webbsida/JS-app

MA-tillägget exporterar MediaHeartbeat-API:er i det globala fönsterobjektet genom att aktivera inställningen Exportera API:er till Window-objekt på sidan [!UICONTROL Configuration]. Den exporterar API:erna under det konfigurerade variabelnamnet. Om till exempel variabelnamnet är konfigurerat till `ADB` kan MediaHeartbeat användas av `window.ADB.MediaHeartbeat`.

>[!IMPORTANT]
>
>MA-tillägget exporterar bara API:erna när `window["CONFIGURED_VARIABLE_NAME"]` är odefinierad och inte åsidosätter befintliga variabler.

1. **Skapa MediaHeartbeat-instans:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **Parametrar:** Ett giltigt delegatobjekt som visar dessa funktioner.

   | Metod |  Beskrivning   |
   | :--- | :--- |
   | `getQoSObject()` | Returnerar `theMediaObject`-instans som innehåller aktuell QoS-information. Den här metoden anropas flera gånger under en uppspelningssession. Spelarimplementeringen måste alltid returnera de senast tillgängliga QoS-data. |
   | `getCurrentPlaybackTime()` | Returnerar spelhuvudets aktuella position. För VOD-spårning anges värdet i sekunder från början av medieobjektet. För LIVE/LIVE-spårning anges värdet i sekunder från programmets början. |

   **Returvärde:** Ett löfte som antingen löses med en `MediaHeartbeat`-instans eller avvisas med ett felmeddelande.

1. **Åtkomst till MediaHeartbeat-konstanter:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   Då visas alla konstanter och statiska metoder från klassen [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

   Du kan hämta exempelspelaren här: [MA-exempelspelaren](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). Exempelspelaren fungerar som en referens för att visa hur man använder MA-tillägget för att stödja Media Analytics direkt från en webbapp.

1. Skapa spårningsinstansen för MediaHeartbeat enligt följande:

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### Använda från andra tillägg

MA-tillägget visar de delade modulerna `get-instance` och `media-heartbeat` för andra tillägg. (Mer information om delade moduler finns i [Dokumentation om delade moduler](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Delade moduler kan bara nås från andra tillägg. Det innebär att en webbsida/JS-app inte kan komma åt de delade modulerna eller använda `turbine` (se kodexempel nedan) utanför ett tillägg.

1. **Skapa MediaHeartbeat-instans:** `get-instance` Delad modul

   **Parametrar:**

   * Ett giltigt delegatobjekt som visar dessa funktioner:

     | Metod |  Beskrivning   |
     | :--- | :--- |
     | `getQoSObject()` | Returnerar instansen `MediaObject` som innehåller aktuell QoS-information. Den här metoden anropas flera gånger under en uppspelningssession. Spelarimplementeringen måste alltid returnera de senast tillgängliga QoS-data. |
     | `getCurrentPlaybackTime()` | Returnerar spelhuvudets aktuella position. För VOD-spårning anges värdet i sekunder från början av medieobjektet. För LIVE/LIVE-spårning anges värdet i sekunder från programmets början. |

   * Ett valfritt config-objekt som visar dessa egenskaper:

     | Egenskap | Beskrivning | Obligatoriskt |
     | :--- | :--- | :--- |
     | Onlinevideoprovider | Namnet på onlinevideoplattformen som innehållet distribueras via. | Nej. Om det finns åsidosätter det värde som definierats under tilläggskonfigurationen. |
     | Spelarnamn | Namnet på den mediespelare som används (t.ex. &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) | Nej. Om det finns åsidosätter det värde som definierats under tilläggskonfigurationen. |
     | Kanal | Egenskapen Kanalnamn | Nej. Om det finns åsidosätter det värde som definierats under tilläggskonfigurationen. |

   **Returvärde:** Ett löfte som antingen löses med en `MediaHeartbeat`-instans eller avvisas med ett felmeddelande.

1. **Åtkomst till MediaHeartbeat-konstanter:** `media-heartbeat` Delad modul

   Den här modulen visar alla konstanter och statiska metoder från den här klassen: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

1. Skapa spårningsinstansen för MediaHeartbeat enligt följande:

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. Använd Media Heartbeat-instansen och följ [dokumentationen för SDK JS ](https://experienceleague.adobe.com/docs/media-analytics/using/legacy-implementations/legacy-media-sdks/setup-javascript/set-up-js-2.html?lang=sv-SE) och [JS API ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html) för att implementera mediespårning.

>[!NOTE]
>
>**Testar:** Om du vill testa tillägget i den här versionen måste du överföra det till [Experience Platform](../../../extension-dev/submit/upload-and-test.md), där du har tillgång till alla beroende tillägg.


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->
