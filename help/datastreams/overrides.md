---
title: Konfigurera åsidosättningar av dataström
description: Lär dig hur du konfigurerar datastream-åsidosättningar i användargränssnittet för datastreams och aktiverar dem via Web SDK.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: b9b6320b15ee93807ebf8b48f31be7386a6f4a19
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%

---

# Konfigurera åsidosättningar av dataström

Med åsidosättningar av dataström kan du definiera ytterligare konfigurationer för dina dataströmmar, som skickas till Edge Network via Web SDK.

Detta hjälper dig att utlösa andra datastream-beteenden än standardbeteendena, utan att skapa ett datastream eller ändra befintliga inställningar.

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningen av din datastream-konfiguration i dialogrutan [konfigurationssida för datastream](configure.md).
2. Sedan måste du skicka åsidosättningarna till Edge Network på något av följande sätt:
   * Via `sendEvent` eller `configure` [Web SDK](#send-overrides) kommandon.
   * Via Web SDK [taggtillägg](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Via Mobile SDK [sendEvent](#send-overrides) API eller genom att använda [Regler](#send-overrides).

I den här artikeln förklaras den kompletta processen för åsidosättning av datastream-konfigurationen för alla typer av åsidosättningar som stöds.

>[!IMPORTANT]
>
>Åsidosättningar av dataström stöds endast för [Web SDK](../web-sdk/home.md) och [Mobile SDK](https://developer.adobe.com/client-sdks/home/) integreringar. [Server-API](../server-api/overview.md) integreringar stöder för närvarande inte datastream-åsidosättningar.
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

## Skicka åsidosättningarna till Edge Network via Web SDK {#send-overrides}

När du har konfigurerat åsidosättningar av datastream i användargränssnittet för datainsamling kan du skicka åsidosättningarna till Edge Network via Web SDK eller Mobile SDK.

* **Web SDK**: Se [åsidosättningar av konfiguration av datastream](../web-sdk/commands/datastream-overrides.md#library) för instruktioner för taggtillägg och exempel på JavaScript-bibliotekskoder.
* **Mobile SDK**: Du kan skicka åsidosättningar av dataStream ID med [sendEvent API](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) eller genom att använda [Regler](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

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
