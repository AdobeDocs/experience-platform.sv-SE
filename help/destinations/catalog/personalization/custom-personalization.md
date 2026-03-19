---
keywords: anpassad personalisering; mål; upplevelseplattform anpassad destination;
title: Anpassad personaliseringsanslutning
description: Det här målet innehåller extern personalisering, innehållshanteringssystem, annonsservrar och andra applikationer som körs på din webbplats för att hämta målgruppsinformation från Adobe Experience Platform. Det här målet ger personalisering i realtid baserat på målgruppsmedlemskap i användarprofiler.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---


# Anpassad personaliseringsanslutning {#custom-personalization-connection}

## Destinationsändringslogg {#changelog}

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Maj 2023 | Funktioner och dokumentation | Från om med maj 2023 har anslutningen **[!UICONTROL Custom personalization]** stöd för [attributbaserad anpassning](../../ui/activate-edge-personalization-destinations.md#map-attributes) och är allmänt tillgänglig för alla kunder. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profilattribut kan innehålla känsliga data. För att skydda dessa data måste du använda [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) när du konfigurerar **[!UICONTROL Custom Personalization]**-målet för attributbaserad personalisering. Alla Edge Network API-anrop måste göras i en [autentiserad kontext](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication).
>
><br>Du kan hämta profilattribut via [ Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) genom att lägga till en integrering på serversidan som använder samma datastream som du redan använder för din webb- eller Mobile SDK-implementering.
>
><br>Om du inte uppfyller kraven ovan baseras personaliseringen endast på målgruppsmedlemskap.

## Översikt {#overview}

Konfigurera den här destinationen så att externa personaliseringsplattformar, content management-system, annonsservrar och andra applikationer som körs på kundens webbplatser kan hämta målgruppsinformation från Adobe Experience Platform.

## Förutsättningar {#prerequisites}

Det här målet kräver någon av följande datainsamlingsmetoder, beroende på implementeringen:

* Använd [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) om du vill samla in data från din webbplats.
* Använd [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) om du vill samla in data från ditt mobilprogram.
* Använd [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) om du inte använder Web SDK eller Mobile SDK, eller om du vill anpassa användarupplevelsen baserat på profilattribut.

>[!IMPORTANT]
>
>**Attributbaserade personaliseringskrav:** Om du vill anpassa baserat på profilattribut (inte bara målgruppsmedlemskap) måste du **** använda [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) med autentiserad integration på serversidan, oavsett om du också använder Web SDK eller Mobile SDK för datainsamling.
>
>Endast SDK och SDK för mobiler stöder endast personalisering baserat på medlemskap för målgrupper. Edge Network API är **obligatoriskt** för att säkert hämta profilattribut för personalisering.

>[!IMPORTANT]
>
>Läs guiden om hur du [aktiverar målgruppsdata till kantanpassningsmål](../../ui/activate-edge-personalization-destinations.md) innan du skapar en anpassad personaliseringsanslutning. Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter.

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som genererats i andra Experience Platform-appar som Adobe Journey Optimizer, </li><li> med mera. </li></ul> |

{style="table-layout:auto"}



Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data som lagras i Adobe Experience Platform Data Lake. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Du begär alla målgrupper som är mappade i det anpassade anpassningsmålet för en enda profil. Olika anpassade anpassningsmål kan ställas in för olika [Adobe Data Collection-datastreams](../../../datastreams/overview.md). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Om datastreams"
>abstract="Det här alternativet avgör i vilket datainsamlingsdatastam som målgrupperna ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Du måste konfigurera ett datastream innan du kan konfigurera målet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html" text="Lär dig konfigurera ett datastream"

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för målet. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **[!UICONTROL Integration alias]**: Det här värdet skickas till Experience Platform Web SDK som ett JSON-objektnamn.
* **[!UICONTROL Datastream]**: Detta avgör i vilken datainsamling som målgrupperna ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Mer information finns i [Konfigurera ett datastream](../../../datastreams/overview.md).

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera profiler och målgrupper för kantanpassning](../../ui/activate-edge-personalization-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data {#exported-data}

Om du använder [taggar i Adobe Experience Platform](/help/tags/home.md) för att distribuera Experience Platform Web SDK använder du funktionen [send event complete](/help/tags/extensions/client/web-sdk/event-types.md) och din anpassade kodsåtgärd har en `event.destinations`-variabel som du kan använda för att visa exporterade data.

Här är ett exempelvärde för variabeln `event.destinations`:

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

Om du inte använder [taggar](/help/tags/home.md) för att distribuera Experience Platform Web SDK kan du använda [kommandosvar](/help/collection/js/commands/command-responses.md) för att se exporterade data.

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

### Exempelsvar för [!UICONTROL Custom Personalization With Attributes] {#example-response-custom-personalization-with-attributes}

När du använder **[!UICONTROL Custom Personalization With Attributes]** ser API-svaret ut ungefär som i exemplet nedan.

Skillnaden mellan **[!UICONTROL Custom Personalization With Attributes]** och **[!UICONTROL Custom Personalization]** är inkluderingen av avsnittet `attributes` i API-svaret.

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

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](../../../data-governance/home.md).
