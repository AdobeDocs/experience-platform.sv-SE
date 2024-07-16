---
title: Konfigurera åsidosättningar av dataström
description: Lär dig hur du konfigurerar åsidosättningar av dataströmmar i användargränssnittet för dataströmmar och aktiverar dem via Web SDK eller Mobile SDK.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 17ed5f3c14d4787352f72d3d7721cbb6416d533e
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Konfigurera åsidosättningar av dataström

Med åsidosättningar av dataströmmar kan du definiera ytterligare konfigurationer för dina dataströmmar, som skickas till Edge Network via Web SDK eller Mobile SDK.

Detta hjälper dig att utlösa andra datastream-beteenden än standardbeteendena, utan att skapa ett datastream eller ändra befintliga inställningar.

Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först måste du definiera åsidosättningen av din datastream-konfiguration på [datastream-konfigurationssidan](configure.md).
2. Sedan måste du skicka åsidosättningarna till Edge Network på något av följande sätt:
   * Via kommandona `sendEvent` eller `configure` [Web SDK](#send-overrides).
   * Via Web SDK-taggtillägget [1.](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)
   * Via Mobile SDK [sendEvent](#send-overrides)-API:t eller genom att använda [Regler](#send-overrides).

I den här artikeln förklaras den kompletta processen för åsidosättning av datastream-konfigurationen för alla typer av åsidosättningar som stöds.

>[!IMPORTANT]
>
>Åsidosättningar av dataström stöds bara för [Web SDK](../web-sdk/home.md)- och [Mobile SDK](https://developer.adobe.com/client-sdks/home/)-integreringar. [Server-API](../server-api/overview.md)-integreringar stöder för närvarande inte datastream-åsidosättningar.
><br>
>Åsidosättningar av datastream bör användas när du behöver olika data som skickas till olika datastreams. Använd inte åsidosättningar av datastream för personaliseringsanvändningsfall eller för medgivandedata.

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda åsidosättningar av datastream finns det några användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här funktionen.

**Datainsamling för flera regioner**

Ett företag har olika webbplatser eller underdomäner för olika länder där de är verksamma. De har [konfigurerat](configure.md) separata datastreams med motsvarande analysspecifika rapportsviter, landsspecifika Adobe Target-egenskapstoken, landsspecifika scheman, datamängder, Journey Optimizer-konfigurationer och så vidare. Företaget har också en global uppsättning konfigurationer där alla landsspecifika data sammanställs.

Genom att använda åsidosättningar av datastream kan företaget dynamiskt växla dataflödet till olika datastreams, i stället för standardbeteendet att skicka data till en datastream.

Ett vanligt användningsexempel kan vara att skicka data till ett landspecifikt datastream och även till ett globalt datastream där kunderna utför en viktig åtgärd, som att göra en beställning eller uppdatera användarprofilen.

**Differentierar profiler och identiteter för olika affärsenheter**

Ett företag med flera affärsenheter vill använda flera Experience Platform sandlådor för att lagra data som är specifika för varje affärsenhet.

I stället för att skicka data till en standarddatastream kan företaget använda åsidosättningar av datastream för att se till att varje affärsenhet har sin egen datastream för att ta emot data.

## Konfigurera åsidosättningar av datastream i användargränssnittet för datastreams {#configure-overrides}

Åsidosättningar av dataströmskonfigurationer gör att du kan ändra följande datastream-konfigurationer:

* Data för händelsen Experience Platform
* Adobe Target egenskapstoken
* Synkroniseringsbehållare för Audience Manager ID
* Adobe Analytics rapporteringsprogram

### Datastream overrides for Adobe Target {#target-overrides}

Om du vill konfigurera datastream-åsidosättningar för en Adobe Target-datastream måste du först skapa en Adobe Target datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med tjänsten [Adobe Target](configure.md#target).

När du har skapat datastream redigerar du [Adobe Target](configure.md#target)-tjänsten som du har lagt till och använder **[!UICONTROL Property Token Overrides]** -avsnittet för att lägga till önskade datastream-åsidosättningar, vilket visas i bilden nedan. Lägg till en egenskapstoken per rad.

![Användargränssnittsskärmbild för datastreams visar Adobe Target tjänstinställningar, med åsidosättningar av egenskapstoken markerade.](assets/overrides/override-target.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Target datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK eller Mobile SDK](#send-overrides).

### Datastream overrides for Adobe Analytics {#analytics-overrides}

Om du vill konfigurera datastream-åsidosättningar för ett Adobe Analytics-datastream måste du först skapa ett [Adobe Analytics](configure.md#analytics)-datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med tjänsten [Adobe Analytics](configure.md#analytics).

När du har skapat datastream redigerar du [Adobe Analytics](configure.md#target)-tjänsten som du har lagt till och använder **[!UICONTROL Report Suite Overrides]** -avsnittet för att lägga till önskade datastream-åsidosättningar, vilket visas i bilden nedan.

Välj **[!UICONTROL Show Batch Mode]** om du vill aktivera gruppredigering av rapportsvitens åsidosättningar. Du kan kopiera och klistra in en lista över åsidosättningar av rapportsviter och ange en rapportsvit per rad.

![Användargränssnittsbild för datastreams visar Adobe Analytics tjänstinställningar, med åsidosättningar av rapportsviten markerade.](assets/overrides/override-analytics.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Analytics datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK eller Mobile SDK](#send-overrides).

### Datastream overrides for Experience Platform event datasets {#event-dataset-overrides}

Om du vill konfigurera datastream-åsidosättningar för händelsedatamängder i Experience Platform måste du först skapa ett [Adobe Experience Platform](configure.md#aep)-datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) med tjänsten [Adobe Experience Platform](configure.md#aep).

När du har skapat dataströmmen redigerar du den [Adobe Experience Platform](configure.md#aep)-tjänst som du har lagt till och väljer alternativet **[!UICONTROL Add Event Dataset]** för att lägga till en eller flera händelsedatamängder för åsidosättning, vilket visas i bilden nedan.

![Användargränssnittsskärmbild för datastreams visar Adobe Experience Platform tjänstinställningar, med åsidosättningar av händelsedatamängd markerade.](assets/overrides/override-aep.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör du konfigurera Adobe Experience Platform datastream-åsidosättningar. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK eller Mobile SDK](#send-overrides).

### Åsidosättningar av dataström för synkroniseringsbehållare för ID från tredje part {#container-overrides}

Om du vill konfigurera datastream-åsidosättningar för synkroniseringsbehållare för ID från tredje part måste du först skapa ett datastream. Följ instruktionerna för att [konfigurera ett datastream](configure.md) för att skapa ett.

När du har skapat datastream går du till **[!UICONTROL Advanced Options]** och aktiverar alternativet **[!UICONTROL Third Party ID Sync]**.

Använd sedan avsnittet **[!UICONTROL Container ID Overrides]** för att lägga till behållar-ID:n som du vill åsidosätta standardinställningen, vilket visas i bilden nedan.

>[!IMPORTANT]
>
>Behållar-ID:n måste vara numeriska värden, som `1234567`, och inte strängar, som `"1234567"`. Om du skickar ett strängvärde via Web SDK som åsidosättning av behållar-ID:n visas ett fel.

![Användargränssnittsskärmbild för datastreams visar datastream-inställningarna, med åsidosättningar av synkroniseringsbehållaren för tredjeparts-ID markerade.](assets/overrides/override-container.png)

När du har lagt till önskade åsidosättningar sparar du datastream-inställningarna.

Nu bör åsidosättningar av ID-synkroniseringsbehållare konfigureras. Nu kan du [skicka åsidosättningarna till Edge Network via Web SDK eller Mobile SDK](#send-overrides).

## Skicka åsidosättningarna till Edge Network {#send-overrides}

När du har konfigurerat åsidosättningar av datastream i användargränssnittet för datainsamling kan du skicka åsidosättningarna till Edge Network via Web SDK eller Mobile SDK.

* **Web SDK**: Mer information om taggtillägg och exempel på JavaScript-bibliotekskod finns i [åsidosättningar av dataströmskonfiguration](../web-sdk/commands/datastream-overrides.md#library).
* **Mobile SDK**: Du kan skicka åsidosättningar av dataström-ID:n med [sendEvent-API:t](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) eller med [Regler](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

## Exempel på nyttolast {#payload-example}

Exemplen ovan genererar en [!DNL Edge Network]-nyttolast som liknar den nedan.

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
