---
title: Åsidosättningar av dataströmskonfiguration
description: Lär dig hur du konfigurerar datastream-åsidosättningar via Web SDK.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Konfigurera åsidosättningar av dataström

Med objektet `edgeConfigOverrides` kan du åsidosätta konfigurationsinställningar för kommandon som körs på den aktuella sidan. Det här åsidosättningsobjektet är inte ett kommando, utan ett objekt som du kan inkludera i de flesta Web SDK-kommandon.

Det här objektet är användbart när du har olika webbplatser eller underdomäner för olika länder, eller om du har flera Experience Platform-sandlådor för att lagra data som är specifika för olika affärsenheter.

>[!IMPORTANT]
>
>Detaljerade konfigurationsinstruktioner från början till slut för datastream-åsidosättningar finns i dokumentationen om [åsidosättningar av datastream-konfigurationer](../../datastreams/overrides.md#configure-overrides).

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningen av din datastream-konfiguration på [datastream-konfigurationssidan](../../datastreams/configure.md) i datastreams-gränssnittet. I dokumentationen för [datastream-konfigurationen åsidosätter](../../datastreams/overrides.md#configure-overrides) finns information om hur du konfigurerar åsidosättningar.
2. När du har konfigurerat åsidosättningen av datastream i användargränssnittet måste du skicka åsidosättningarna till Edge Network på något av följande sätt:
   * Via Web SDK-taggtillägget [1.](#tag-extension)
   * Via kommandona [`sendEvent`](../commands/sendevent/overview.md) eller [`configure`](../commands/configure/overview.md) Web SDK.
   * Via Mobile SDK [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network)-kommandot.

Om du anger åsidosättningar både i Web SDK-konfigurationen och i ett specifikt kommando (till exempel [`sendEvent`](sendevent/overview.md)) får åsidosättningarna i det specifika kommandot prioritet.

>[!NOTE]
>
>Om du vill att en konfigurationsåsidosättning ska *inaktivera* en Experience Cloud-tjänst måste du se till att tjänsten först *aktiveras* i datastream-konfigurationen. I dokumentationen om hur du [konfigurerar datastreams](../../datastreams/configure.md#add-services) finns mer information om hur du lägger till tjänster i ett datastream.

## Skicka åsidosättningar av datastream till Edge Network via taggtillägget Web SDK {#tag-extension}

Mer information om konfigurationsinstruktioner finns i dokumentationen om [att konfigurera datastream-åsidosättningar](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) från Web SDK-taggtillägget.

Om du vill konfigurera datastream-åsidosättningar från Web SDK-taggtillägget anger du varje önskat fält under **[!UICONTROL Datastream configuration overrides]** när [du konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Datastream configuration overrides]**. Ange varje önskat åsidosättningsvärde.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

Om du vill ange åsidosättningar bara för ett specifikt kommando anger du varje önskat fält inom åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Send event]**.
1. Bläddra ned till avsnittet **[!UICONTROL Datastream configuration overrides]**.
1. Ställ in det önskade åsidosättningsvärdet för varje fält i det här avsnittet.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

Separata fält tillhandahålls för [!UICONTROL Development]-, [!UICONTROL Staging]- och [!UICONTROL Production]-miljöer. Se till att du fyller i alla önskade fält för varje miljö.

## Skicka åsidosättningarna till Edge Network via Web SDK JavaScript-biblioteket {#library}

När du har [konfigurerat datastream-åsidosättningarna](../../datastreams/overrides.md) i användargränssnittet för datainsamling kan du nu skicka åsidosättningarna till Edge Network via JavaScript-biblioteket för Web SDK.

Om du använder Web SDK är det andra och sista steget i att aktivera åsidosättningar av datastream-konfiguration att skicka åsidosättningar till Edge Network via kommandot `edgeConfigOverrides`.

Åsidosättningar av dataströmskonfigurationer skickas till Edge Network via Web SDK-kommandot `edgeConfigOverrides`. Det här kommandot skapar åsidosättningar av datastream som skickas till [!DNL Edge Network] på nästa kommando. Om du använder kommandot `configure` skickas åsidosättningarna för varje begäran.

Kommandot `edgeConfigOverrides` skapar åsidosättningar av datastream som skickas vidare till [!DNL Edge Network] vid nästa kommando.

När en konfigurationsåsidosättning skickas med kommandot `configure` ingår den i följande Web SDK-kommandon.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [konfigurera](../commands/configure/overview.md)

Alternativ som anges globalt kan åsidosättas av konfigurationsalternativet för enskilda kommandon.

### Skicka konfigurationsåsidosättningar via Web SDK-kommandot `sendEvent` {#send-event}

I exemplet nedan visas alla dynamiska datastream-konfigurationsalternativ som stöds av ett `sendEvent`-anrop.

Om din datastream-konfiguration har alla tjänster som stöds aktiverade, kommer exemplet nedan att åsidosätta den här inställningen och inaktivera alla tjänster (se `enabled: false`-inställningen för varje tjänst).

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
      reportSuites: ["ujslconfigoverrides3"],
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

| Parameter | Beskrivning |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | Använd den här parametern för att tillåta att en enda begäran går till en annan datastream än den som definieras av kommandot `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Definierar den dynamiska datastream-konfigurationen för tjänsten Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definierar om händelsen ska skickas till tjänsten Experience Platform eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definierar de datamängder som används för händelsen. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definierar om händelsen skickas till Offera decisioningen eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definierar om händelsen skickas till kantsegmenteringstjänsten eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definierar om händelsedata skickas till kantmålen eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definierar om händelsedata skickas till Adobe Journey Optimizer-tjänsten eller inte. |
| `com_adobe_analytics.enabled` | Definierar om händelsedata skickas till Adobe Analytics eller inte. |
| `com_adobe_analytics.reportSuites[]` | En array med strängar som avgör till vilka rapportsviter du vill skicka Analytics-data. |
| `com_adobe_identity.idSyncContainerId` | Synkroniseringsbehållaren för tredjeparts-ID som du vill använda i Audience Manager. För att den här ID-synkroniseringsbehållaren ska fungera måste du ange `com_adobe_audience_manager.enabled` till `true`. Annars är tjänsten Audience Manager inaktiverad. |
| `com_adobe_target.enabled` | Definierar om händelsedata skickas till Adobe Target. |
| `com_adobe_target.propertyToken` | Token för Adobe Target-destinationsegenskapen. |
| `com_adobe_audience_manager.enabled` | Definierar om händelsedata skickas till tjänsten Audience Manager. |
| `com_adobe_launch_ssf` | Definierar om händelsedata skickas till vidarebefordran på serversidan. |

### Skicka konfigurationsåsidosättningar via Web SDK-kommandot `configure` {#send-configure}

I exemplet nedan visas hur en konfigurationsåsidosättning kan se ut för ett `configure`-kommando.

Om din datastream-konfiguration har alla tjänster som stöds aktiverade, kommer exemplet nedan att åsidosätta den här inställningen och inaktivera alla tjänster (se `enabled: false`-inställningen för varje tjänst).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| Parameter | Beskrivning |
|---|---|
| `orgId` | Det IMS-organisations-ID som motsvarar ditt Adobe-konto. |
| `edgeConfigOverrides.datastreamId` | Använd den här parametern för att tillåta att en enda begäran går till en annan datastream än den som definieras av kommandot `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Definierar den dynamiska datastream-konfigurationen för tjänsten Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Definierar om händelsen ska skickas till tjänsten Experience Platform eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Definierar de datamängder som används för händelsen. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Definierar om händelsen skickas till Offera decisioningen eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Definierar om händelsen skickas till kantsegmenteringstjänsten eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Definierar om händelsedata skickas till kantmålen eller inte. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Definierar om händelsedata skickas till Adobe Journey Optimizer-tjänsten eller inte. |
| `com_adobe_analytics.enabled` | Definierar om händelsedata skickas till Adobe Analytics eller inte. |
| `com_adobe_analytics.reportSuites[]` | En array med strängar som avgör till vilka rapportsviter du vill skicka Analytics-data. |
| `com_adobe_identity.idSyncContainerId` | Synkroniseringsbehållaren för tredjeparts-ID som du vill använda i Audience Manager. För att den här ID-synkroniseringsbehållaren ska fungera måste du ange `com_adobe_audience_manager.enabled` till `true`. Annars är tjänsten Audience Manager inaktiverad. |
| `com_adobe_target.enabled` | Definierar om händelsedata skickas till Adobe Target. |
| `com_adobe_target.propertyToken` | Token för Adobe Target-destinationsegenskapen. |
| `com_adobe_audience_manager.enabled` | Definierar om händelsedata skickas till tjänsten Audience Manager. |
| `com_adobe_launch_ssf` | Definierar om händelsedata skickas till vidarebefordran på serversidan. |

