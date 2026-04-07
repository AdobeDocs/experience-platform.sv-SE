---
keywords: anpassad personalisering; mål; upplevelseplattform anpassad destination;
title: Anpassad Personalization-anslutning
description: Lär dig hur du konfigurerar Personalization-destinationen för att hämta målgruppsdata från Adobe Experience Platform för anpassning av webbplatser i realtid.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 3779531814cbf7e5718db0ac88aca266f14a1b21
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---


# Anpassad Personalization-anslutning {#custom-personalization-connection}

## Destinationsändringslogg {#changelog}

Använd den här ändringsloggen för att spåra uppdateringar av det anpassade Personalization-målet.

| Releasamånad | Uppdateringstyp | Beskrivning |
| --- | --- | --- |
| Maj 2023 | Funktioner och dokumentation | Från om med maj 2023 har anslutningen **[!UICONTROL Custom personalization]** stöd för [attributbaserad anpassning](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) och är allmänt tillgänglig för alla kunder. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Profilattribut kan innehålla känsliga data. Om du vill skydda dessa data använder du [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) när du konfigurerar **[!UICONTROL Custom Personalization]**-målet för attributbaserad personalisering. Alla Edge Network API-anrop måste göras i en [autentiserad kontext](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication).
>
>Hämta profilattribut via [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) genom att lägga till en integration på serversidan som använder samma datastream som du redan använder för din webb- eller Mobile SDK-implementering.
>
>Om ni inte uppfyller kraven ovan baseras personaliseringen endast på målgruppsmedlemskap.

## Översikt {#overview}

Ange det här målet för att tillåta externa personaliseringsplattformar, innehållshanteringssystem, annonsservrar och andra program som körs på kundwebbplatser att hämta målgruppsinformation från [!DNL Adobe Experience Platform].

## Förutsättningar {#prerequisites}

Detta mål kräver en av följande datainsamlingsmetoder, beroende på implementeringen:

* Använd [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) för att samla in data från din webbplats.
* Använd [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) för att samla in data från ditt mobilprogram.
* Använd [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) om du inte använder Web SDK eller Mobile SDK, eller om du vill anpassa användarupplevelsen baserat på profilattribut.

>[!IMPORTANT]
>
>**Attributbaserade personaliseringskrav:** Om du vill anpassa baserat på profilattribut (inte bara målgruppsmedlemskap) **måste** använda [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/) med autentiserad integration på serversidan, oavsett om du också använder Web SDK eller Mobile SDK för datainsamling.
>
>Endast SDK och SDK för mobiler stöder personalisering enbart baserat på målgruppsmedlemskap. Edge Network API är **obligatoriskt** för att säkert hämta profilattribut för personalisering.

>[!IMPORTANT]
>
>Innan du skapar en anpassad Personalization-anslutning läser du guiden om hur du [aktiverar målgruppsdata för kantanpassningsmål](/help/destinations/ui/activate-edge-personalization-destinations.md). Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter.

## Målgrupper {#supported-audiences}

I följande tabell visas de målgruppstyper som du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](/help/segmentation/home.md). |
| Alla andra målgrupper kommer | Ja | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li>anpassade uppladdningsgrupper [importerade](/help/segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li>lookalike-målgrupper,</li><li>federerade målgrupper,</li><li>målgrupper som har genererats i andra Experience Platform-appar som [!DNL Adobe Journey Optimizer],</li><li>med mera.</li></ul> |

{style="table-layout:auto"}

Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Rikta in er på specifika grupper av människor baserat på kundprofiler. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data lagrade i datasjön [!DNL Adobe Experience Platform]. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

I följande tabell beskrivs exporttypen och frekvensen för destinationen.

| Objekt | Typ | Anteckningar |
| --- | --- | --- |
| Exporttyp | **[!UICONTROL Profile request]** | Begär alla målgrupper som mappats i det anpassade Personalization-målet för en enda profil. Olika anpassade Personalization-mål kan ställas in för olika [Adobe Data Collection-datastreams](/help/datastreams/overview.md). |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Om datastreams"
>abstract="Det här alternativet avgör i vilket datainsamlingsdatastam som målgrupperna ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Du måste konfigurera ett datastream innan du kan konfigurera målet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html" text="Lär dig konfigurera ett datastream"

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](/help/destinations/ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När [konfigurerar](/help/destinations/ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning för målet. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **[!UICONTROL Integration alias]**: En obligatorisk sträng som identifierar det här målet i personaliseringssvaret. Aliasvärdet returneras till din webbplats eller app tillsammans med målgrupperna (och, om de är konfigurerade, attribut) som är kopplade till det här målet. Använd aliaset i koden på klient- eller serversidan för att hitta och bearbeta rätt personaliseringsobjekt när flera personaliseringsmål är aktiva på samma dataström. Aliaset måste vara unikt i en sandlåda för alla anpassade Personalization-mål.
* **[!UICONTROL Datastream]**: Detta avgör i vilken datainsamling som målgrupperna ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Mer information finns i [Konfigurera ett datastream](/help/datastreams/overview.md).

### Aktivera aviseringar {#enable-alerts}

Aktivera aviseringar om du vill få meddelanden om status för dataflödet till det här målet. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](/help/destinations/ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera profiler och målgrupper för att kanalisera personaliseringsmål](/help/destinations/ui/activate-edge-personalization-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Exporterade data {#exported-data}

Om du använder [taggar i Adobe Experience Platform](/help/tags/home.md) för att distribuera Experience Platform Web SDK använder du funktionen [send event complete](/help/tags/extensions/client/web-sdk/event-types.md) . Din anpassade kodsåtgärd kommer att ha en `event.destinations`-variabel som du kan använda för att visa exporterade data.

Här är ett exempelvärde för variabeln `event.destinations`:

```json
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

Tolka JSON-svaret från [!DNL Adobe Experience Platform] för att hitta integreringsaliaset för programmet som du integrerar med [!DNL Adobe Experience Platform]. Skicka målgrupps-ID:n till programmets kod som målparametrar. Nedan visas ett exempel på hur detta ser ut när det gäller målsvaret.

```js
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

### Exempelsvar för anpassad Personalization med attribut {#example-response-attributes}

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

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
