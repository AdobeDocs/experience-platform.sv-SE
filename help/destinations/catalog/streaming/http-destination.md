---
keywords: strömning,
title: HTTP-anslutning
description: Med HTTP API-målet i Adobe Experience Platform kan du skicka profildata till HTTP-slutpunkter från tredje part.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 8d2c5ef477d4707be4c0da43ba1f672fac797604
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# (Beta) [!DNL HTTP] API-anslutning

>[!IMPORTANT]
>
>The [!DNL HTTP] målet i Platform är för närvarande i betaversion. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

The [!DNL HTTP] API-målet är en [!DNL Adobe Experience Platform] direktuppspelningsmål som hjälper dig att skicka profildata till tredje part [!DNL HTTP] slutpunkter.

Skicka profildata till [!DNL HTTP] slutpunkter måste du först ansluta till målet i [[!DNL Adobe Experience Platform]](#connect-destination).

## Användningsfall {#use-cases}

The [!DNL HTTP] målet är avsett för kunder som behöver exportera XDM-profildata och målgruppssegment till generiska [!DNL HTTP] slutpunkter.

[!DNL HTTP] slutpunkterna kan antingen vara kundernas egna system eller tredjepartslösningar.

## Anslut till målet {#connect}

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

Dina exporterade [!DNL Experience Platform] data får plats i [!DNL HTTP] mål i JSON-format. Händelsen nedan innehåller till exempel e-postadressprofilattributet för en målgrupp som har kvalificerat sig för ett visst segment och avslutat ett annat segment. Identiteterna för den här potentiella kunden är [!DNL ECID] och mejl.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
