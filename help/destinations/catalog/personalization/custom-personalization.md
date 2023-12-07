---
keywords: anpassad personalisering; mål; upplevelseplattform anpassad destination;
title: Anpassad personaliseringsanslutning
description: Det här målet innehåller extern personalisering, innehållshanteringssystem, annonsservrar och andra applikationer som körs på din webbplats för att hämta målgruppsinformation från Adobe Experience Platform. Det här målet ger personalisering i realtid baserat på målgruppsmedlemskap i användarprofiler.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---


# Anpassad personaliseringsanslutning {#custom-personalization-connection}

## Destinationsändringslogg {#changelog}

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Maj 2023 | Funktioner och dokumentation | Från maj 2023 **[!UICONTROL Custom personalization]** anslutningsstöd [attributbaserad personalisering](../../ui/activate-edge-personalization-destinations.md#map-attributes) och är allmänt tillgängligt för alla kunder. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profilattribut kan innehålla känsliga data. För att skydda dessa data måste du använda [API för Edge Network Server](/help/server-api/overview.md) när du konfigurerar **[!UICONTROL Custom Personalization]** mål för attributbaserad personalisering. Alla Server-API-anrop måste göras i en [autentiserad kontext](../../../server-api/authentication.md).
>
><br>Om du redan använder Web SDK eller Mobile SDK för din integrering kan du hämta attribut via Server-API:t genom att lägga till en integration på serversidan.
>
><br>Om ni inte uppfyller kraven ovan kommer personaliseringen endast att baseras på målgruppsmedlemskap.

## Översikt {#overview}

Konfigurera den här destinationen så att externa personaliseringsplattformar, content management-system, annonsservrar och andra applikationer som körs på kundens webbplatser kan hämta målgruppsinformation från Adobe Experience Platform.

## Förutsättningar {#prerequisites}

Den här integreringen drivs av [Adobe Experience Platform Web SDK](../../../edge/home.md) eller [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/). Du måste använda någon av dessa SDK:er för att kunna använda det här målet.

>[!IMPORTANT]
>
>Innan du skapar en anpassad personaliseringsanslutning ska du läsa guiden om hur du [aktivera målgruppsdata för kantpersonalisering](../../ui/activate-edge-personalization-destinations.md). Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Du begär alla målgrupper som är mappade i det anpassade anpassningsmålet för en enda profil. Olika anpassade anpassningsmål kan konfigureras för olika [Datasamlingsdatamängder för Adobe](../../../datastreams/overview.md). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Om dataStream-ID"
>abstract="Det här alternativet avgör i vilket datainsamlingsdatastam som målgrupperna ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Du måste konfigurera ett datastream innan du kan konfigurera målet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html" text="Lär dig konfigurera ett datastream"

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **[!UICONTROL Integration alias]**: Det här värdet skickas till Experience Platform Web SDK som ett JSON-objektnamn.
* **[!UICONTROL Datastream ID]**: Detta avgör i vilken datainsamling som målgrupperna inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Se [Konfigurera ett datastream](../../../datastreams/overview.md) för mer information.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och målgrupper för kantanpassning](../../ui/activate-edge-personalization-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data {#exported-data}

Om du använder [Taggar i Adobe Experience Platform](../../../tags/home.md) för att distribuera Experience Platform Web SDK använder du [skicka händelse slutförd](../../../tags/extensions/client/web-sdk/event-types.md) -funktionalitet och din egen kodinsats har `event.destinations` som du kan använda för att visa exporterade data.

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

JSON-svaret från Adobe Experience Platform kan analyseras för att hitta motsvarande integreringsalias för det program du integrerar med Adobe Experience Platform. Målgrupps-ID:n kan skickas till programmets kod som målparametrar. Nedan visas ett exempel på hur detta skulle se ut när det gäller målsvaret.

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Exempelsvar för [!UICONTROL Custom Personalization With Attributes]

När du använder **[!UICONTROL Custom Personalization With Attributes]** ser API-svaret ut ungefär som i exemplet nedan.

Skillnaden mellan **[!UICONTROL Custom Personalization With Attributes]** och **[!UICONTROL Custom Personalization]** innebär att `attributes` i API-svaret.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](../../../data-governance/home.md).
