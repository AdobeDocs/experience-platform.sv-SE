---
keywords: personalisering, destination, upplevelseplattform anpassad destination,
title: Anpassat anpassningsmål
description: Den här destinationen erbjuder extern personalisering, innehållshanteringssystem, annonsservrar och andra program som körs på din webbplats som ett sätt att hämta segmentinformation från Adobe Experience Platform. Detta mål ger 1:1 i realtid och personalisering baserat på en användarprofils segmentmedlemskap.
source-git-commit: 6c21398a3f2fb26cc925ca1f5dcbe92b306a8325
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Anpassad personaliseringsanslutning (beta) {#custom-personalization-connection}

## Översikt {#overview}

>[!IMPORTANT]
>
>Anslutningen för anpassad personalisering i Adobe Experience Platform finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Det här målet är ett sätt att hämta segmentinformation från Adobe Experience Platform till externa personaliseringsplattformar, innehållshanteringssystem, annonsservrar och andra program som körs på kundens webbplatser.

## Förutsättningar {#prerequisites}

Integrationen drivs av [Adobe Experience Platform Web SDK](../../../edge/home.md). Du måste använda denna SDK för att kunna använda den här destinationen.

## Exporttyp {#export-type}

**Profilbegäran**  - du begär alla segment som är mappade i det anpassade anpassningsmålet för en enda profil. Olika anpassade personaliseringsmål kan ställas in för olika datamängder i Adobe Data Collection.

## Användningsfall {#use-cases}

Den här målgruppen delar målgrupper med en annonsserver och andra program än Adobe för personalisering, som ska användas i realtid för att avgöra vilken annons som användare ska se på en webbplats.

### Användningsfall 1

**Anpassa en hemsida**

En webbplats för uthyrning och försäljning i hemmet vill personalisera sin hemsida baserat på segmentkvalifikationer i Adobe Experience Platform. Företaget kan välja vilka målgrupper som ska få en personaliserad upplevelse och mappa dem till det anpassade personaliseringsmål som hade konfigurerats för deras personaliseringsprogram utanför Adobe som målinriktningskriterier.

**Målinriktad annonsering på plats**

Med ett separat anpassat anpassningsmål för sin annonsserver kan samma webbplats rikta in sig på annonser på webbplatsen med en annan uppsättning segment än Adobe Experience Platform som målinriktningskriterier.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **[!UICONTROL Integration alias]**: Värdet skickas till Experience Platform Web SDK som ett JSON-objektnamn.
* **[!UICONTROL Datastream ID]**: Detta anger i vilken datainsamlingsdatastam segmenten ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Mer information finns i [Konfigurera en datastream](../../../edge/fundamentals/datastreams.md).

## Aktivera segment till den här destinationen {#activate}

Läs [Aktivera profiler och segment för att profilera mål för begäran](../../ui/activate-profile-request-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment för den här destinationen.

## Exporterade data {#exported-data}

Om du använder [Adobe-taggar](../../../tags/home.md) för att distribuera Experience Platform Web SDK använder du funktionen [send event complete](../../../edge/extension/event-types.md) och din anpassade kodsåtgärd har en `event.destinations`-variabel som du kan använda för att visa exporterade data.

Om du inte använder [Adobe-taggar](../../../tags/home.md) för att distribuera Experience Platform Web SDK använder du funktionen [hantering av svar från händelser](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events).

JSON-svaret från Adobe Experience Platform kan analyseras för att hitta motsvarande integreringsalias för det program du integrerar med Adobe Experience Platform. Segment-ID:n kan skickas till programmets kod som målparametrar. Nedan visas ett exempel på hur detta skulle se ut när det gäller målsvaret.

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(results) {
    if(results.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = results.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = results.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] framtvingar datastyrning finns i [översikten över datastyrning](../../../data-governance/home.md).
