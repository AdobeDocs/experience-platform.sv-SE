---
title: Konfigurera åsidosättningar av dataström
description: Lär dig hur du konfigurerar datastream-åsidosättningar i användargränssnittet för datastreams och aktiverar dem via Web SDK.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 0%

---

# Konfigurera åsidosättningar av dataström

Med åsidosättningar av dataströmmar kan du definiera ytterligare konfigurationer för dina dataströmmar, som skickas till Edge Network via Web SDK.

Detta hjälper dig att utlösa andra datastream-beteenden än standardbeteendena, utan att skapa ett datastream eller ändra befintliga inställningar.

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningen av din datastream-konfiguration i dialogrutan [konfigurationssida för datastream](configure.md).
2. Sedan måste du skicka åsidosättningarna till Edge Network på något av följande sätt:
   * Via `sendEvent` eller `configure` [Web SDK](#send-overrides-web-sdk) kommandon.
   * Via Web SDK [taggtillägg](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Via Mobile SDK [sendEvent](#send-overrides-mobile-sdk) -kommando.

I den här artikeln förklaras den kompletta processen för åsidosättning av datastream-konfigurationen för alla typer av åsidosättningar som stöds.

>[!IMPORTANT]
>
>Åsidosättningar av dataström stöds endast för [Web SDK](../edge/home.md) och [Mobile SDK](https://developer.adobe.com/client-sdks/home/) integreringar. [Server-API](../server-api/overview.md) integreringar stöder för närvarande inte datastream-åsidosättningar.
><br>
>Åsidosättningar av datastream bör användas när du behöver olika data som skickas till olika datastreams. Använd inte åsidosättningar av datastream för personaliseringsanvändningsfall eller för medgivandedata.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda åsidosättningar av datastream finns det några användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

**Datainsamling för flera regioner**

Ett företag har olika webbplatser eller underdomäner för olika länder där de är verksamma. De har [konfigurerad](configure.md) separata datastreams med motsvarande analysspecifika rapportsviter, landspecifika Adobe Target-egenskapstoken, landsspecifika scheman, datamängder, Journey Optimizer-konfigurationer osv. Företaget har också en global uppsättning konfigurationer där alla landsspecifika data sammanställs.

Genom att använda åsidosättningar av datastream kan företaget dynamiskt växla dataflödet till olika datastreams, i stället för standardbeteendet att skicka data till en datastream.

Ett vanligt användningsexempel kan vara att skicka data till ett landspecifikt datastream och även till ett globalt datastream där kunderna utför en viktig åtgärd, som att göra en beställning eller uppdatera användarprofilen.

**Differentiera profiler och identiteter för olika affärsenheter**

Ett företag med flera affärsenheter vill använda flera Experience Platform sandlådor för att lagra data som är specifika för varje affärsenhet.

I stället för att skicka data till en standarddatastream kan företaget använda åsidosättningar av datastream för att se till att varje affärsenhet har sin egen datastream för att ta emot data.

## Konfigurera åsidosättningar av datastream i användargränssnittet för datastreams {#configure-overrides}

Åsidosättningar av dataströmskonfigurationer gör att du kan ändra följande datastream-konfigurationer:

* Data för händelsen Experience Platform
* Adobe Target egenskapstoken
* Synkroniseringsbehållare för Audience Manager ID
* Adobe Analytics rapporteringsprogram

### Datastream overrides for Adobe Target {#target-overrides}

Om du vill konfigurera datastream-åsidosättningar för en Adobe Target-datastream måste du först skapa en Adobe Target datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med [Adobe Target](configure.md#target) service.

När du har skapat dataströmmen kan du redigera [Adobe Target](configure.md#target) tjänster som du har lagt till och använder **[!UICONTROL Property Token Overrides]** för att lägga till önskade datastream-åsidosättningar, vilket visas i bilden nedan. Lägg till en egenskapstoken per rad.

![Skärmbilden Datastreams UI som visar Adobe Target tjänstinställningar, med åsidosättningar av egenskapstoken markerade.](assets/overrides/override-target.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Target datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

### Datastream overrides for Adobe Analytics {#analytics-overrides}

Om du vill konfigurera datastream-åsidosättningar för en Adobe Analytics-datastream måste du först ha en [Adobe Analytics](configure.md#analytics) datastream har skapats. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med [Adobe Analytics](configure.md#analytics) service.

När du har skapat dataströmmen kan du redigera [Adobe Analytics](configure.md#target) tjänster som du har lagt till och använder **[!UICONTROL Report Suite Overrides]** för att lägga till önskade datastream-åsidosättningar, vilket visas i bilden nedan.

Välj **[!UICONTROL Show Batch Mode]** om du vill aktivera gruppredigering av åsidosättningar av rapportsviten. Du kan kopiera och klistra in en lista över åsidosättningar av rapportsviter och ange en rapportsvit per rad.

![Skärmbilden Datastreams UI som visar Adobe Analytics tjänstinställningar, med rapportsvitens åsidosättningar markerade.](assets/overrides/override-analytics.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Analytics datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

### Datastream overrides for Experience Platform event datasets {#event-dataset-overrides}

Om du vill konfigurera datastream-åsidosättningar för händelsedatamängder i Experience Platform måste du först ha en [Adobe Experience Platform](configure.md#aep) datastream har skapats. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med [Adobe Experience Platform](configure.md#aep) service.

När du har skapat dataströmmen kan du redigera [Adobe Experience Platform](configure.md#aep) som du har lagt till och väljer **[!UICONTROL Add Event Dataset]** alternativ för att lägga till en eller flera åsidosatta händelsedatamängder, vilket visas i bilden nedan.

![Skärmbilden Datastreams UI som visar Adobe Experience Platform tjänstinställningar, med åsidosättningar av händelsedatamängd markerade.](assets/overrides/override-aep.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Experience Platform datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

### Åsidosättningar av dataström för synkroniseringsbehållare för ID från tredje part {#container-overrides}

Om du vill konfigurera datastream-åsidosättningar för synkroniseringsbehållare för ID från tredje part måste du först skapa ett datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) för att skapa en.

När du har skapat datastream går du till **[!UICONTROL Advanced Options]** och aktivera **[!UICONTROL Third Party ID Sync]** alternativ.

Använd sedan **[!UICONTROL Container ID Overrides]** för att lägga till behållar-ID:n som du vill åsidosätta standardinställningen, vilket visas i bilden nedan.

>[!IMPORTANT]
>
>Behållar-ID måste vara numeriska värden, som `1234567`och inte strängar, som `"1234567"`. Om du skickar ett strängvärde via Web SDK som åsidosättning av behållar-ID:n visas ett fel.

![Användargränssnittsbild för datastreams visar datastream-inställningarna, med åsidosättningar av synkroniseringsbehållare för ID från tredje part markerade.](assets/overrides/override-container.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör åsidosättningar av ID-synkroniseringsbehållare konfigureras. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK](#send-overrides).

## Skicka åsidosättningarna till Edge Network via Web SDK {#send-overrides-web-sdk}

>[!NOTE]
>
>Som ett alternativ till att skicka konfigurationsåsidosättningar via Web SDK-kommandon kan du lägga till konfigurationsåsidosättningar i Web SDK [taggtillägg](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

Efter [konfigurera åsidosättningar av datastream](#configure-overrides) i användargränssnittet för datainsamling kan du nu skicka åsidosättningarna till Edge Network via Web SDK.

Om du använder Web SDK skickar du åsidosättningarna till Edge Network via `edgeConfigOverrides` -kommandot är det andra och sista steget i att aktivera åsidosättningar av dataströmskonfigurationer.

Åsidosättningar av dataströmskonfigurationer skickas till Edge-nätverket via `edgeConfigOverrides` Web SDK, kommando. Det här kommandot skapar åsidosättningar av datastream som skickas till [!DNL Edge Network] på nästa kommando. Om du använder `configure` -kommandot skickas åsidosättningarna för varje begäran.

The `edgeConfigOverrides` kommandot skapar åsidosättningar av datastream som skickas vidare till [!DNL Edge Network] på nästa kommando.

När en konfigurationsåsidosättning skickas med `configure` finns det i följande Web SDK-kommandon.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [konfigurera](../edge/fundamentals/configuring-the-sdk.md)

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

## Skicka åsidosättningarna till Edge Network via Mobile SDK {#send-overrides-mobile-sdk}

Efter [konfigurera åsidosättningar av datastream](#configure-overrides) i användargränssnittet för datainsamling kan du nu skicka åsidosättningarna till Edge Network via Mobile SDK.

Om du använder Mobile SDK skickar du åsidosättningarna till Edge Network via `sendEvent` API är det andra och sista steget för att aktivera åsidosättningar av datastream-konfiguration.

Mer information om Experience Platform Mobile SDK finns i [Mobile SDK-dokumentation](https://developer.adobe.com/client-sdks/edge/edge-network/).

### Åsidosättning av dataström-ID via Mobile SDK {#id-override-mobile}

Exemplen nedan visar hur en åsidosättning av ett datastream-ID kan se ut i en Mobile SDK-integrering. Välj flikarna nedan för att visa [!DNL iOS] och [!DNL Android] exempel.

>[!BEGINTABS]

>[!TAB iOS (Skift)]

I det här exemplet visas hur en åsidosättning av ett dataström-ID ser ut i en Mobile SDK [!DNL iOS] integrering.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]
let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamIdOverride: "SampleDatastreamId")

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android™ (Kotlin)]

I det här exemplet visas hur en åsidosättning av ett dataström-ID ser ut i en Mobile SDK [!DNL Android] integrering.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamIdOverride("SampleDatastreamId")
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

### Åsidosättning av dataströmskonfiguration via Mobile SDK {#config-override-mobile}

Exemplen nedan visar hur en åsidosättning av en datastream-konfiguration kan se ut i en Mobile SDK-integrering. Välj flikarna nedan för att visa [!DNL iOS] och [!DNL Android] exempel.

>[!BEGINTABS]

>[!TAB iOS (Skift)]

I det här exemplet visas hur en åsidosättning av en dataströmskonfiguration ser ut i en Mobile SDK [!DNL iOS] integrering.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]

let configOverrides: [String: Any] = [
  "com_adobe_experience_platform": [
    "datasets": [
      "event": [
        "datasetId": "SampleEventDatasetIdOverride"
      ]
    ]
  ],
  "com_adobe_analytics": [
  "reportSuites": [
        "MyFirstOverrideReportSuite",
          "MySecondOverrideReportSuite",
          "MyThirdOverrideReportSuite"
      ]
  ],
  "com_adobe_identity": [
    "idSyncContainerId": "1234567"
  ],
  "com_adobe_target": [
    "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
 ],
]

let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamConfigOverride: configOverrides)

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android (Kotlin)]

I det här exemplet visas hur en åsidosättning av en dataströmskonfiguration ser ut i en Mobile SDK [!DNL Android] integrering.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val configOverrides = mapOf(
    "com_adobe_experience_platform"
    to mapOf(
        "datasets"
        to mapOf(
            "event"
            to mapOf("datasetId"
                to "SampleEventDatasetIdOverride")
        )
    ),
    "com_adobe_analytics"
    to mapOf(
        "reportSuites"
        to listOf(
            "MyFirstOverrideReportSuite",
            "MySecondOverrideReportSuite",
            "MyThirdOverrideReportSuite"
        )
    ),
    "com_adobe_identity"
    to mapOf(
        "idSyncContainerId"
        to "1234567"
    ),
    "com_adobe_target"
    to mapOf(
        "propertyToken"
        to "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    )
)

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamConfigOverride(configOverrides)
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

## Exempel på nyttolast {#payload-example}

Exemplen ovan genererar ett [!DNL Edge Network] nyttolast som liknar den nedan.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
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
  "events": [  ]
}
```
