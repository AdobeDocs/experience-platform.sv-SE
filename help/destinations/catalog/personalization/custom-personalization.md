---
keywords: personalisering, destination, upplevelseplattform anpassad destination,
title: Anpassad personaliseringsanslutning
description: Den här destinationen erbjuder extern personalisering, innehållshanteringssystem, annonsservrar och andra program som körs på din webbplats för att hämta segmentinformation från Adobe Experience Platform. Detta mål ger personalisering i realtid baserat på medlemskap i användarprofilsegment.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 05217dead7e1365d6dcc0cc7ae4078628514d1d5
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 1%

---

# Anpassad personaliseringsanslutning {#custom-personalization-connection}

## Översikt {#overview}

Det här målet är ett sätt att hämta segmentinformation från Adobe Experience Platform till externa personaliseringsplattformar, innehållshanteringssystem, annonsservrar och andra program som körs på kundens webbplatser.

## Förutsättningar {#prerequisites}

Den här integreringen drivs av [Adobe Experience Platform Web SDK](../../../edge/home.md) eller [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). Du måste använda någon av dessa SDK:er för att kunna använda det här målet.

>[!IMPORTANT]
>
>Innan du skapar en anpassad personaliseringsanslutning ska du läsa guiden om hur du [konfigurera anpassningsmål för personalisering på samma sida och nästa sida](../../ui/configure-personalization-destinations.md). Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter.

## Exportera typ och frekvens {#export-type-frequency}

**Profilbegäran** - du begär alla segment som är mappade i det anpassade anpassningsmålet för en enda profil. Olika anpassade anpassningsmål kan konfigureras för olika [Datasamlingsdatamängder för Adobe](../../../edge/fundamentals/datastreams.md).

## Användningsfall {#use-cases}

Den här målgruppen delar målgrupper med annonsservrar och icke-Adobe-personaliseringsapplikationer, som ska användas i realtid för att avgöra vilken annonsanvändare som ska se på en webbplats.

### Användningsfall 1

**Anpassa en hemsida**

En webbplats för uthyrning och försäljning i hemmet vill personalisera sin hemsida baserat på segmentkvalifikationer i Adobe Experience Platform. Företaget kan välja vilka målgrupper som ska få en personaliserad upplevelse och mappa dem till det anpassade personaliseringsmål som hade konfigurerats för deras personaliseringsprogram utanför Adobe som målinriktningskriterier.

**Målinriktad annonsering på plats**

Med ett separat anpassat anpassningsmål för sin annonsserver kan samma webbplats rikta in sig på annonser på webbplatsen med en annan uppsättning segment än Adobe Experience Platform som målinriktningskriterier.

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Om dataStream-ID"
>abstract="Med det här alternativet anger du i vilken datainsamlingsdatastam segmenten ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Du måste konfigurera ett datastream innan du kan konfigurera målet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Lär dig konfigurera ett datastream"

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **[!UICONTROL Integration alias]**: Värdet skickas till Experience Platform Web SDK som ett JSON-objektnamn.
* **[!UICONTROL Datastream ID]**: Detta anger i vilken datainsamlingsdatastam segmenten ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Se [Konfigurera ett datastream](../../../edge/fundamentals/datastreams.md) för mer information.

## Aktivera segment till den här destinationen {#activate}

Läs [Aktivera profiler och segment för att profilera mål för begäran](../../ui/activate-profile-request-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

Om du använder [Taggar i Adobe Experience Platform](../../../tags/home.md) för att distribuera Experience Platform Web SDK använder du [skicka händelse slutförd](../../../edge/extension/event-types.md) -funktionalitet och din egen kodinsats har `event.destinations` variabel som du kan använda för att visa exporterade data.

Här är ett exempelvärde för `event.destinations` variabel:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Om du inte använder [Taggar](../../../tags/home.md) för att distribuera Experience Platform Web SDK använder du [hantera svar från händelser](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) för att se exporterade data.

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
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
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

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](../../../data-governance/home.md).
