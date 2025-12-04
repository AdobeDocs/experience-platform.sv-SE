---
title: edgeConfigOverrides
description: Konfigurera åsidosättningar av datastream för bara kommandot sendEvent.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` (`sendEvent` kommando)

Med objektet `edgeConfigOverrides` kan du åsidosätta konfigurationsinställningar bara för det aktuella `sendEvent`-kommandot. Det här objektet är användbart när du har specifika kommandon på samma sida som du vill köra med andra konfigurationsinställningar än den övriga Web SDK-implementeringen. Om du vill åsidosätta konfigurationsinställningarna för alla kommandon på en viss sida bör du överväga att använda objektet [`edgeConfigOverrides` i `configure` command](../configure/edgeconfigoverrides.md) .

Åsidosättningsprocessen för datastream-konfigurationen består av två huvudsteg:

1. Först måste du definiera åsidosättningen av datastream-konfigurationen när [en datastream](/help/datastreams/configure.md) konfigureras i datastreams-gränssnittet. Mer information om hur du konfigurerar åsidosättningar finns i [Åsidosättningar av dataströmskonfigurationer](/help/datastreams/overrides.md) i dokumentationen för datastreams.
1. När du har konfigurerat åsidosättningen av datastream i användargränssnittet för datastreams kan du konfigurera objektet `edgeConfigOverrides`.

Observera att kommandot `configure` även har stöd för ett `edgeConfigOverrides` -objekt. Se [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) under kommandot `configure`. Objektet `edgeConfigOverrides` i kommandot `sendEvent` har företräde framför objektet `edgeConfigOverrides` i kommandot `configure` om båda har angetts.

## Exempel

Om din datastream-konfiguration har alla tjänster som stöds aktiverade åsidosätter exemplet nedan den här inställningen och inaktiverar alla tjänster (se `enabled: false`-inställningen för varje tjänst). Det här objektet stöder samma egenskaper som objektet [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) i kommandot `configure`.

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## Åsidosättningar av dataströmskonfiguration med hjälp av taggtillägget Web SDK

SDK-taggtilläggets motsvarighet för det här objektet är avsnittet [Åsidosättningar av dataströmskonfiguration](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) när åtgärden [!UICONTROL Send event] konfigureras.
