---
title: Åsidosättningar av dataströmskonfiguration
description: Lär dig hur du konfigurerar datastream-åsidosättningar via Web SDK.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '842'
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
   * Via kommandona `sendEvent` eller `configure` Web SDK.
   * Via Mobile SDK `sendEvent`-kommandot.

Om du anger åsidosättningar både i Web SDK-konfigurationen och i ett specifikt kommando (till exempel [`sendEvent`](sendevent/overview.md)) får åsidosättningarna i det specifika kommandot prioritet.

## Objektegenskaper

Följande egenskaper är tillgängliga i det här objektet:

* **Åsidosättning av dataström**: Skicka anrop till en annan dataström. Om du anger det här värdet måste andra åsidosättningar som kräver en datastream-konfiguration konfigureras i den datastream som anges här.
* **Synkroniseringsbehållare för ID från tredje part**: ID:t för målets synkroniseringsbehållare för ID från tredje part i Adobe Audience Manager. Du måste konfigurera åsidosättning av en ID-behållare från tredje part i datastreams-inställningarna innan du kan använda det här fältet.
* **Målegenskapstoken**: Token för målegenskapen i Adobe Target. Du måste konfigurera åsidosättning av en token för Target-egenskap i datastreams-inställningarna innan du kan använda det här fältet.
* **Rapportsviter**: ID:n för rapportsviten som ska åsidosättas i Adobe Analytics. Du måste konfigurera åsidosättningar av rapportsviten i datastreams inställningar innan du kan använda det här fältet.

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

I exemplet nedan visas hur en konfigurationsåsidosättning kan se ut för ett `sendEvent`-kommando.

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
| `edgeConfigOverrides.datastreamId` | Använd den här parametern för att tillåta att en enda begäran går till en annan datastream än den som definieras av kommandot `configure`. |
| `com_adobe_analytics.reportSuites[]` | En array med strängar som avgör till vilka rapportsviter som vill skicka Analytics-data. |
| `com_adobe_identity.idSyncContainerId` | Synkroniseringsbehållaren för tredjeparts-ID som du vill använda i Audience Manager. |
| `com_adobe_target.propertyToken` | Token för Adobe Target-destinationsegenskapen. |

### Skicka konfigurationsåsidosättningar via Web SDK-kommandot `configure` {#send-configure}

I exemplet nedan visas hur en konfigurationsåsidosättning kan se ut för ett `configure`-kommando.

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
| `edgeConfigOverrides.datastreamId` | Använd den här parametern för att tillåta att en enda begäran går till en annan datastream än den som definieras av kommandot `configure`. |
| `com_adobe_analytics.reportSuites[]` | En array med strängar som avgör till vilka rapportsviter som vill skicka Analytics-data. |
| `com_adobe_identity.idSyncContainerId` | Synkroniseringsbehållaren för tredjeparts-ID som du vill använda i Audience Manager. |
| `com_adobe_target.propertyToken` | Token för Adobe Target-destinationsegenskapen. |
