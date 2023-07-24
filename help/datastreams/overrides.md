---
title: Konfigurera åsidosättningar av datastream
description: Lär dig hur du konfigurerar datastream-åsidosättningar i användargränssnittet för datastreams och aktiverar dem via Web SDK.
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 0%

---

# Konfigurera åsidosättningar av datastream

Med åsidosättningar av dataströmmar kan du definiera ytterligare konfigurationer för dina dataströmmar, som skickas till Edge Network via Web SDK.

Detta hjälper dig att utlösa andra datastream-beteenden än standardbeteendena, utan att du behöver skapa ett nytt datastream eller ändra dina befintliga inställningar.

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningar av dataströmskonfigurationer i [konfigurationssida för datastream](configure.md).
2. Sedan måste du skicka åsidosättningarna till Edge Network antingen via ett Web SDK-kommando eller via Web SDK [taggtillägg](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

I den här artikeln förklaras den kompletta processen för åsidosättning av datastream-konfigurationen för alla typer av åsidosättningar som stöds.

## Konfigurera åsidosättningar av datastream i användargränssnittet för datastreams {#configure-overrides}

Åsidosättningar av dataströmskonfigurationer gör att du kan ändra följande datastream-konfigurationer:

* Data för händelsen Experience Platform
* Adobe Target egenskapstoken
* Synkroniseringsbehållare för Audience Manager ID
* Adobe Analytics rapporteringsprogram

### Datastream overrides for Adobe Target {#target-overrides}

Om du vill konfigurera datastream-åsidosättningar för en Adobe Target-datastream måste du först skapa en Adobe Target datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med [Adobe Target](configure.md#target) service.

När du har skapat datastream redigerar du [Adobe Target](configure.md#target) som du har lagt till och använder **[!UICONTROL Property Token Overrides]** för att lägga till önskade datastream-åsidosättningar, vilket visas i bilden nedan. Lägg till en egenskapstoken per rad.

![Skärmbilden Datastreams UI som visar Adobe Target tjänstinställningar, med åsidosättningar av egenskapstoken markerade.](assets/overrides/override-target.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Target datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

### Datastream overrides for Adobe Analytics {#analytics-overrides}

Om du vill konfigurera datastream-åsidosättningar för en Adobe Analytics-datastream måste du först ha en [Adobe Analytics](configure.md#analytics) datastream har skapats. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med [Adobe Analytics](configure.md#analytics) service.

När du har skapat datastream redigerar du [Adobe Analytics](configure.md#target) som du har lagt till och använder **[!UICONTROL Report Suite Overrides]** för att lägga till önskade datastream-åsidosättningar, vilket visas i bilden nedan.

Välj **[!UICONTROL Show Batch Mode]** om du vill aktivera gruppredigering av åsidosättningar av rapportsviten. Du kan kopiera och klistra in en lista över åsidosättningar av rapportsviter och ange en rapportsvit per rad.

![Skärmbilden Datastreams UI som visar Adobe Analytics tjänstinställningar, med rapportsvitens åsidosättningar markerade.](assets/overrides/override-analytics.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Analytics datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

### Datastream overrides for Experience Platform event datasets {#event-dataset-overrides}

Om du vill konfigurera datastream-åsidosättningar för händelsedatamängder i Experience Platform måste du först ha en [Adobe Experience Platform](configure.md#aep) datastream har skapats. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med [Adobe Experience Platform](configure.md#aep) service.

När du har skapat datastream redigerar du [Adobe Experience Platform](configure.md#aep) som du har lagt till och väljer **[!UICONTROL Add Event Dataset]** alternativ för att lägga till en eller flera åsidosatta händelsedatamängder, vilket visas i bilden nedan.

![Skärmbilden Datastreams UI som visar Adobe Experience Platform tjänstinställningar, med åsidosättningar av händelsedatamängd markerade.](assets/overrides/override-aep.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Experience Platform datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

### Åsidosättningar av dataström för synkroniseringsbehållare för ID från tredje part {#container-overrides}

Om du vill konfigurera datastream-åsidosättningar för synkroniseringsbehållare för ID från tredje part måste du först skapa ett datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) för att skapa en.

När du har skapat datastream går du till **[!UICONTROL Advanced Options]** och aktivera **[!UICONTROL Third Party ID Sync]** alternativ.

Använd sedan **[!UICONTROL Container ID Overrides]** för att lägga till behållar-ID:n som du vill åsidosätta standardinställningen, vilket visas i bilden nedan.

>[!IMPORTANT]
>
>Behållar-ID:n måste vara numeriska värden, som `1234567`och inte strängar, som `"1234567"`. Om du skickar ett strängvärde via Web SDK som åsidosättning av behållar-ID:n visas ett fel.

![Datastreams-gränssnittets skärmbild visar datastream-inställningarna, med åsidosättningar av synkroniseringsbehållaren för tredjeparts-ID markerade.](assets/overrides/override-container.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör åsidosättningar av ID-synkroniseringsbehållare konfigureras. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

## Skicka åsidosättningarna till Edge Network via Web SDK {#send-overrides}

>[!NOTE]
>
>Som ett alternativ till att skicka konfigurationsåsidosättningar via Web SDK-kommandon kan du lägga till konfigurationsåsidosättningar i Web SDK [taggtillägg](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

Efter [konfigurera åsidosättningar av datastream](#configure-overrides) i användargränssnittet för datainsamling kan du nu skicka åsidosättningarna till Edge Network via Web SDK.

Att skicka åsidosättningar till Edge Network via Web SDK är det andra och sista steget i att aktivera åsidosättningar av datastream-konfiguration.

Åsidosättningar av dataströmskonfigurationer skickas till Edge-nätverket via `edgeConfigOverrides` Web SDK, kommando. Det här kommandot skapar åsidosättningar av datastream som skickas till [!DNL Edge Network] på nästa kommando eller, om `configure` kommando, för varje begäran.

The `edgeConfigOverrides` kommandot skapar åsidosättningar av datastream som skickas vidare till [!DNL Edge Network] på nästa kommando eller, om `configure`, för varje förfrågan.

När en konfigurationsåsidosättning skickas med `configure` finns det i följande Web SDK-kommandon.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [konfigurera](../edge/fundamentals/configuring-the-sdk.md)

Alternativ som anges globalt kan åsidosättas av konfigurationsalternativet för enskilda kommandon.

### Skicka konfigurationsåsidosättningar via `sendEvent` kommando {#send-event}

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
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
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

### Skicka konfigurationsåsidosättningar via `configure` kommando {#send-configure}

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
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
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

### Exempel på nyttolast {#payload-example}

Exemplen ovan genererar ett [!DNL Edge Network] nyttolast som ser ut så här:

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
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
    "state": {  }
  },
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```
