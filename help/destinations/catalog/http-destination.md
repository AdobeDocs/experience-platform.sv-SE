---
keywords: strömning,
title: HTTP-anslutning
description: Med HTTP-målet i Adobe Experience Platform kan du skicka profildata till HTTP-slutpunkter från tredje part.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# (Alfa) [!DNL HTTP]-anslutning

>[!IMPORTANT]
>
>Målet [!DNL HTTP] i Platform är för närvarande alfavärdet. Dokumentationen och funktionaliteten kan komma att ändras.

## Översikt {#overview}

Målet [!DNL HTTP] är ett [!DNL Adobe Experience Platform]-mål för direktuppspelning som hjälper dig att skicka profildata till [!DNL HTTP]-slutpunkter från tredje part.

Om du vill skicka profildata till [!DNL HTTP]-slutpunkter måste du först ansluta till målet i [[!DNL Adobe Experience Platform]](#connect-destination).

## Användningsfall {#use-cases}

Målet [!DNL HTTP] riktar sig till kunder som behöver exportera XDM-profildata och målgruppssegment till generiska [!DNL HTTP] slutpunkter.

[!DNL HTTP] slutpunkterna kan antingen vara kundernas egna system eller tredjepartslösningar.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL httpEndpoint]**: den  [!DNL URL] av HTTP-slutpunkterna som du vill skicka profildata till.
   * Du kan också lägga till frågeparametrar i [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: den  [!DNL URL] av HTTP-slutpunkten som används för  [!DNL OAuth2] autentisering.
* **[!UICONTROL Client ID]**: den  [!DNL clientID] parameter som används i  [!DNL OAuth2] klientens autentiseringsuppgifter.
* **[!UICONTROL Client Secret]**: den  [!DNL clientSecret] parameter som används i  [!DNL OAuth2] klientens autentiseringsuppgifter.

   >[!NOTE]
   >
   >Endast [!DNL OAuth2] klientautentiseringsuppgifter stöds för närvarande.

* **[!UICONTROL Name]**: Ange ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: Ange en beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Custom Headers]**: Ange eventuella anpassade rubriker som du vill ska ingå i målanropen, enligt följande format:  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >Den aktuella implementeringen kräver minst en anpassad rubrik. Den här begränsningen kommer att åtgärdas i en framtida uppdatering.

## Aktivera segment till den här destinationen {#activate}

Se [Aktivera profiler och segment till ett mål](../ui/activate-destinations.md#select-attributes) för instruktioner om hur du aktiverar målgruppssegment till mål.

## Målattribut {#attributes}

När [aktivera segment](../ui/activate-destinations.md) till ett [!DNL HTTP]-mål i [[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes)-steget rekommenderar Adobe att du väljer en unik identifierare i ditt [unionsschema](../../profile/home.md#profile-fragments-and-union-schemas). Välj den unika identifieraren och eventuella andra XDM-fält som du vill exportera till målet.

## Exporterade data {#exported-data}

Dina exporterade [!DNL Experience Platform]-data anges i ditt [!DNL HTTP]-mål i JSON-format. Händelsen nedan innehåller till exempel e-postadressprofilattributet för en målgrupp som har kvalificerat sig för ett visst segment och avslutat ett annat segment. Identiteterna för den här potentiella kunden är [!DNL ECID] och e-post.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
