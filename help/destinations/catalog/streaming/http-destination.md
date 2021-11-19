---
keywords: strömning,
title: HTTP-anslutning
description: Med HTTP API-målet i Adobe Experience Platform kan du skicka profildata till HTTP-slutpunkter från tredje part.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 3bec18f1b7209b1f329dc90aadb597edb6143291
workflow-type: tm+mt
source-wordcount: '347'
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
