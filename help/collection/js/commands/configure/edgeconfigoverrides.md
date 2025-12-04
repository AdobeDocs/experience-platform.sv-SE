---
title: edgeConfigOverrides
description: Konfigurera datastream-åsidosättningar för implementeringen.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` (`configure` kommando)

Med objektet `edgeConfigOverrides` kan du åsidosätta konfigurationsinställningar för kommandon som körs på den aktuella sidan. Det här objektet är användbart när du har olika webbplatser eller underdomäner för olika länder, eller om du har flera Experience Platform-sandlådor för att lagra data som är specifika för olika affärsenheter. Om du bara vill åsidosätta konfigurationsinställningarna för ett enda kommando på sidan kan du använda objektet [`edgeConfigOverrides` i `sendEvent` command](../sendevent/edgeconfigoverrides.md) .

Åsidosättningsprocessen för datastream-konfigurationen består av två huvudsteg:

1. Först måste du definiera åsidosättningen av datastream-konfigurationen när [en datastream](/help/datastreams/configure.md) konfigureras i datastreams-gränssnittet. Mer information om hur du konfigurerar åsidosättningar finns i [Åsidosättningar av dataströmskonfigurationer](/help/datastreams/overrides.md) i dokumentationen för datastreams.
1. När du har konfigurerat åsidosättningen av datastream i användargränssnittet för datastreams kan du konfigurera objektet `edgeConfigOverrides`.

När du anger objektet `edgeConfigOverrides` i kommandot `configure` gäller det alla data som skickas till Adobe. Följande kommandon _stöder även_ objektet `edgeConfigOverrides`:

* [`sendEvent`](../sendevent/edgeconfigoverrides.md)
* [`setConsent`](../setconsent.md)
* [`getIdentity`](../getidentity.md)
* [`appendIdentityToUrl`](../appendidentitytourl.md)

Inställningen `edgeConfigOverrides` i något av ovanstående kommandon har företräde framför objektet `edgeConfigOverrides` i kommandot `configure` om båda är angivna. Om något av dessa kommandon inte innehåller något `edgeConfigOverrides`-objekt används `edgeConfigOverrides`-objektet i kommandot `configure`.

## Exempel

Om alla tjänster som stöds är aktiverade i din datastream-konfiguration, åsidosätts den här inställningen av exemplet nedan och alla tjänster inaktiveras.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| Parameter | Typ | Beskrivning |
| --- | --- | --- |
| **`orgId`** | `string` | Ditt företags IMS-organisationsnummer. |
| **`datastreamId`** | `string` | Det datastream-ID som data ska skickas till. |
| **`com_adobe_experience_platform`** | `object` | Definierar den dynamiska datastream-konfigurationen för Adobe Experience Platform-tjänster. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | Anger om händelsen skickas till Adobe Experience Platform. |
| **`com_adobe_experience_platform.datasets`** | `object` | Definierar de datamängder som används för händelsen. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | Anger om händelsen skickas till Offer Decisioning. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | Avgör om händelsen skickas till Edge Segmentation. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | Anger om händelsen skickas till Edge Destinations. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | Avgör om händelsen skickas till Adobe Journey Optimizer. |
| **`com_adobe_analytics.enabled`** | `boolean` | Anger om händelsen skickas till Adobe Analytics. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | En array med strängar som avgör vilka rapportsviter som Analytics-data ska skickas till. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | Anger om händelsen skickas till Adobe Audience Manager. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | Synkroniseringsbehållaren för tredjeparts-ID som du vill använda i Audience Manager. Kräver `com_adobe_audience_manager.enabled` inställd på `true`. Annars är Audience Manager-tjänsten inaktiverad. |
| **`com_adobe_target.enabled`** | `boolean` | Anger om händelsen skickas till Adobe Target. |
| **`com_adobe_target.propertyToken`** | `string` | Token för Adobe Target-destinationsegenskapen. |
| **`com_adobe_launch_ssf`** | `boolean` | Anger om händelsen skickas till vidarebefordran på serversidan. |

## Konfigurationsåsidosättningar med hjälp av taggtillägget Web SDK

SDK-taggtilläggets motsvarighet för det här fältet finns under [Konfigurationsåsidosättningar](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) när du konfigurerar taggtillägget.
