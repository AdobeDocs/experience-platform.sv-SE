---
keywords: strömning,
title: HTTP API-anslutning
description: Med HTTP API-målet i Adobe Experience Platform kan du skicka profildata till HTTP-slutpunkter från tredje part.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: f098df9df2baa971db44a6746949f021e212ae3e
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# (Beta) HTTP API-anslutning

>[!IMPORTANT]
>
>HTTP API-målet i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

HTTP API-målet är en [!DNL Adobe Experience Platform] direktuppspelningsmål som hjälper dig att skicka profildata till HTTP-slutpunkter från tredje part.

Om du vill skicka profildata till HTTP-slutpunkter måste du först [ansluta till målet](#connect-destination) in [!DNL Adobe Experience Platform].

## Användningsfall {#use-cases}

HTTP-målet riktar sig till kunder som behöver exportera XDM-profildata och målgruppssegment till generiska HTTP-slutpunkter.

HTTP-slutpunkter kan antingen vara kundernas egna system eller tredjepartslösningar.

## Förutsättningar {#prerequisites}

>[!IMPORTANT]
>
>Kontakta Adobe eller Adobe kundtjänst om du vill aktivera betafunktionen för HTTP API-mål för ditt företag.

Om du vill använda HTTP API-målet för att exportera data från Experience Platform måste du uppfylla följande krav:

* Du måste ha en HTTP-slutpunkt som stöder REST API.
* HTTP-slutpunkten måste ha stöd för Experience Platform-profilschemat. Ingen omvandling till ett nyttolastschema från tredje part stöds i HTTP API-målet. Se [exporterade data](#exported-data) för ett exempel på utdataschemat för Experience Platform.
* HTTP-slutpunkten måste ha stöd för rubriker.
* HTTP-slutpunkten måste ha stöd [Autentiseringsuppgifter för OAuth 2.0-klient](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) autentisering. Detta krav är giltigt medan HTTP API-målet är i betafasen.
* Klientens autentiseringsuppgifter måste inkluderas i POSTENS innehåll till din slutpunkt, vilket visas i exemplet nedan.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```


Du kan också använda [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) för att konfigurera en integrering och skicka Experience Platform-profildata till en HTTP-slutpunkt.

## Anslut till målet {#connect-destination}

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **[!UICONTROL httpEndpoint]**: den [!DNL URL] för den HTTP-slutpunkt som du vill skicka profildata till.
   * Du kan också lägga till frågeparametrar i [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: den [!DNL URL] av HTTP-slutpunkten som används för [!DNL OAuth2] autentisering.
* **[!UICONTROL Client ID]**: den [!DNL clientID] parametern som används i [!DNL OAuth2] klientautentiseringsuppgifter.
* **[!UICONTROL Client Secret]**: den [!DNL clientSecret] parametern som används i [!DNL OAuth2] klientautentiseringsuppgifter.

   >[!NOTE]
   >
   >Endast [!DNL OAuth2] klientautentiseringsuppgifter stöds för närvarande.

* **[!UICONTROL Name]**: Ange ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: Ange en beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Custom Headers]**: Ange eventuella anpassade rubriker som du vill ska ingå i målanropen, enligt följande format: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >Den aktuella implementeringen kräver minst en anpassad rubrik. Den här begränsningen kommer att åtgärdas i en framtida uppdatering.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera målgruppsdata till exportmål för direktuppspelningsprofiler](../../ui/activate-streaming-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Målattribut {#attributes}

I [[!UICONTROL Select attributes]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe rekommenderar att du väljer en unik identifierare från [union](../../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet.

## Beteende vid export av profiler {#profile-export-behavior}

Experience Platform optimerar beteendet för profilexport till HTTP API-målet, så att endast data exporteras till API-slutpunkten när relevanta uppdateringar av en profil har gjorts efter segmentkvalificering eller andra viktiga händelser. Profiler exporteras till ditt mål i följande situationer:

* Profiluppdateringen utlöstes av en ändring av segmentmedlemskapet för minst ett av segmenten som mappats till målet. Profilen har till exempel kvalificerats för ett av de segment som är mappade till målet eller har avslutat ett av de segment som är mappade till målet.
* Profiluppdateringen utlöstes av en ändring i [identitetskarta](/help/xdm/field-groups/profile/identitymap.md). En profil som redan är kvalificerad för ett av de segment som är mappade till målet har till exempel lagts till som en ny identitet i attributet för identitetskarta.
* Profiluppdateringen utlöstes av en attributändring för minst ett av attributen som är mappade till målet. Ett av attributen som är mappade till målet i mappningssteget läggs till i en profil.

I alla de fall som beskrivs ovan exporteras endast de profiler där relevanta uppdateringar har gjorts till ditt mål. Om ett segment som är mappat till målflödet till exempel har hundra medlemmar och fem nya profiler är kvalificerade för segmentet, kommer exporten till målet att vara inkrementell och endast innehålla de fem nya profilerna.

Observera att alla mappade attribut exporteras för en profil, oavsett var ändringarna finns. I exemplet ovan exporteras alltså alla mappade attribut för de fem nya profilerna även om attributen inte har ändrats.

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform] data får plats i [!DNL HTTP] mål i JSON-format. Exporten nedan innehåller till exempel en profil som har kvalificerats för ett visst segment och avslutat ett annat segment, och den innehåller profilattributets förnamn, efternamn, födelsedatum och personlig e-postadress. Identiteterna för den här profilen är ECID och e-post.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
