---
title: Åsidosättningar av dataströmskonfiguration
description: Lär dig hur du konfigurerar datastream-åsidosättningar via Web SDK.
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---


# Konfigurera åsidosättningar av dataström

The `edgeConfigOverrides` kan du åsidosätta konfigurationsinställningar för kommandon som körs på den aktuella sidan. Det här åsidosättningsobjektet är inte ett kommando, utan ett objekt som du kan inkludera i de flesta Web SDK-kommandon.

Det här objektet är användbart när du har olika webbplatser eller underdomäner för olika länder, eller om du har flera Experience Platform-sandlådor för att lagra data som är specifika för olika affärsenheter.

>[!IMPORTANT]
>
>Detaljerade konfigurationsinstruktioner från början till slut för åsidosättningar av datastream finns i [åsidosättningar av konfiguration av datastream](../../datastreams/overrides.md#configure-overrides) dokumentation.

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningen av din datastream-konfiguration i dialogrutan [konfigurationssida för datastream](../../datastreams/configure.md)i användargränssnittet för datastreams. Se [åsidosättningar av konfiguration av datastream](../../datastreams/overrides.md#configure-overrides) dokumentation för instruktioner om hur du konfigurerar åsidosättningar.
2. När du har konfigurerat åsidosättningen av datastream i användargränssnittet måste du skicka åsidosättningarna till Edge Network på något av följande sätt:
   * Via Web SDK [taggtillägg](#tag-extension).
   * Via `sendEvent` eller `configure` Web SDK-kommandon.
   * Via Mobile SDK `sendEvent` -kommando.

Om du anger åsidosättningar både i Web SDK-konfigurationen och i ett specifikt kommando (till exempel [`sendEvent`](sendevent/overview.md)) prioriteras åsidosättningarna i det specifika kommandot.

## Objektegenskaper

Följande egenskaper är tillgängliga i det här objektet:

* **Åsidosättning av datastam**: Skicka samtal till en annan datastream. Om du anger det här värdet måste andra åsidosättningar som kräver en datastream-konfiguration konfigureras i den datastream som anges här.
* **Synkroniseringsbehållare för ID från tredje part**: ID för målets synkroniseringsbehållare för tredjeparts-ID i Adobe Audience Manager. Du måste konfigurera åsidosättning av en ID-behållare från tredje part i datastreams-inställningarna innan du kan använda det här fältet.
* **Målegenskapstoken**: Token för egenskapen destination i Adobe Target. Du måste konfigurera åsidosättning av en token för Target-egenskap i datastreams-inställningarna innan du kan använda det här fältet.
* **Rapportsviter**: Det rapportsvit-ID som ska åsidosättas i Adobe Analytics. Du måste konfigurera åsidosättningar av rapportsviten i datastreams inställningar innan du kan använda det här fältet.

## Skicka datastream-åsidosättningar till Edge Network via taggtillägget Web SDK {#tag-extension}

Läs dokumentationen om [konfigurera åsidosättningar av datastream](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) från taggtillägget Web SDK om du vill ha detaljerade konfigurationsinstruktioner.

Om du vill konfigurera åsidosättningar av dataström från taggtillägget Web SDK anger du önskade fält under **[!UICONTROL Datastream configuration overrides]** när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till **[!UICONTROL Datastream configuration overrides]** -avsnitt. Ange varje önskat åsidosättningsvärde.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

Om du vill ange åsidosättningar bara för ett specifikt kommando anger du varje önskat fält inom åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Bläddra ned till avsnittet med etiketten **[!UICONTROL Datastream configuration overrides]**.
1. Ställ in det önskade åsidosättningsvärdet för varje fält i det här avsnittet.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

Det finns separata fält [!UICONTROL Development], [!UICONTROL Staging]och [!UICONTROL Production] miljöer. Se till att du fyller i alla önskade fält för varje miljö.

## Skicka åsidosättningarna till Edge Network via JavaScript-biblioteket för Web SDK {#library}

Efter [konfigurera åsidosättningar av datastream](../../datastreams/overrides.md) i användargränssnittet för datainsamling kan du nu skicka åsidosättningarna till Edge Network via JavaScript-biblioteket för Web SDK.

Om du använder Web SDK skickar du åsidosättningarna till Edge Network via `edgeConfigOverrides` -kommandot är det andra och sista steget i att aktivera åsidosättningar av dataströmskonfigurationer.

Åsidosättningar av dataströmskonfigurationer skickas till Edge-nätverket via `edgeConfigOverrides` Web SDK, kommando. Det här kommandot skapar åsidosättningar av datastream som skickas till [!DNL Edge Network] på nästa kommando. Om du använder `configure` -kommandot skickas åsidosättningarna för varje begäran.

The `edgeConfigOverrides` kommandot skapar åsidosättningar av datastream som skickas vidare till [!DNL Edge Network] på nästa kommando.

När en konfigurationsåsidosättning skickas med `configure` finns det i följande Web SDK-kommandon.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [konfigurera](../commands/configure/overview.md)

Alternativ som anges globalt kan åsidosättas av konfigurationsalternativet för enskilda kommandon.

### Skicka konfigurationsåsidosättningar via Web SDK `sendEvent` kommando {#send-event}

Exemplet nedan visar hur en konfigurationsåsidosättning kan se ut på en `sendEvent` -kommando.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Parameter | Beskrivning |
|---|---|
| `edgeConfigOverrides.datastreamId` | Använd den här parametern för att tillåta att en enda begäran går till en annan datastream än den som definieras av `configure` -kommando. |
| `com_adobe_analytics.reportSuites[]` | En array med strängar som avgör till vilka rapportsviter som vill skicka Analytics-data. |
| `com_adobe_identity.idSyncContainerId` | Synkroniseringsbehållaren för tredjeparts-ID som du vill använda i Audience Manager. |
| `com_adobe_target.propertyToken` | Token för Adobe Target-destinationsegenskapen. |

### Skicka konfigurationsåsidosättningar via Web SDK `configure` kommando {#send-configure}

Exemplet nedan visar hur en konfigurationsåsidosättning kan se ut på en `configure` -kommando.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

| Parameter | Beskrivning |
|---|---|
| `edgeConfigOverrides.datastreamId` | Använd den här parametern för att tillåta att en enda begäran går till en annan datastream än den som definieras av `configure` -kommando. |
| `com_adobe_analytics.reportSuites[]` | En array med strängar som avgör till vilka rapportsviter som vill skicka Analytics-data. |
| `com_adobe_identity.idSyncContainerId` | Synkroniseringsbehållaren för tredjeparts-ID som du vill använda i Audience Manager. |
| `com_adobe_target.propertyToken` | Token för Adobe Target-destinationsegenskapen. |