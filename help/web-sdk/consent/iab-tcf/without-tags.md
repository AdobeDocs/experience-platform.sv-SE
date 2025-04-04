---
title: Integrera stödet för IAB TCF 2.0 med Adobe Experience Platform Web SDK
description: Lär dig hur du ställer in stöd för IAB TCF 2.0 för din webbplats utan att använda taggar.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Integrera stödet för IAB TCF 2.0 med Experience Platform Web SDK

Den här guiden visar hur du integrerar den interaktiva Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0) med Adobe Experience Platform Web SDK utan att använda taggar. En översikt över integrationen med IAB TCF 2.0 finns i [översikten](./overview.md). En guide om hur du integrerar med taggar finns i guiden [IAB TCF 2.0 för taggar](./with-tags.md).

## Komma igång

Den här guiden använder gränssnittet `__tcfapi` för att komma åt medgivandeinformationen. Det kan vara enklare för er att integrera direkt med ert molnhanteringsföretag (CMP). Informationen i den här handboken kan dock fortfarande vara användbar eftersom CMP i allmänhet har funktioner som liknar TCF API.

>[!NOTE]
>
>Exemplen förutsätter att `window.__tcfapi` har definierats på sidan när koden körs. CMP:er kan tillhandahålla en krok där du kan köra dessa funktioner när `__tcfapi`-objektet är klart.

Om du vill använda IAB TCF 2.0 med taggar och Adobe Experience Platform Web SDK-tillägget måste du ha ett XDM-schema tillgängligt. Om du inte har konfigurerat något av dessa kan du börja med att visa den här sidan innan du fortsätter.

Dessutom krävs det att du har en fungerande förståelse för Adobe Experience Platform Web SDK. Läs [Adobe Experience Platform Web SDK overview](../../home.md) och [Vanliga frågor och svar](../../faq.md) om du vill få en snabb uppdatering.

## Aktivera standardmedgivande

Om du vill behandla alla okända användare på samma sätt kan du ange [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) till `pending` eller `out`. Detta köar eller tar bort Experience Events tills du får medgivandeinställningarna.

### Ange standardsamtycke baserat på `gdprApplies`

Vissa datahanteringsplattformar gör det möjligt att avgöra om den allmänna dataskyddsförordningen (GDPR) gäller för kunden. Om du vill anta samtycke för kunder där GDPR inte gäller kan du använda flaggan `gdprApplies` i TCF API-anropet.

I följande exempel visas ett sätt att göra detta:

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

I det här exemplet anropas kommandot `configure` efter att `tcData` har hämtats från TCF API. Om `gdprApplies` är true anges standardmedgivande till `pending`. Om `gdprApplies` är falskt anges standardsamtycke till `in`. Se till att du fyller i variabeln `alloyConfiguration` med din konfiguration.

>[!NOTE]
>
>När standardmedgivandet är inställt på `in` kan kommandot `setConsent` fortfarande användas för att registrera dina kunders medgivandeinställningar.

## Använda händelsen setConsent

IAB TCF 2.0 API innehåller en händelse för när kunden uppdaterar medgivandet. Detta inträffar när kunden från början ställer in sina inställningar och när kunden uppdaterar sina inställningar.

I följande exempel visas ett sätt att göra detta:

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Det här kodblocket lyssnar efter `useractioncomplete`-händelsen och anger sedan medgivandet och skickar medgivandesträngen och `gdprApplies`-flaggan. Om du har anpassade identiteter för dina kunder måste du fylla i variabeln `identityMap`. Mer information finns i guiden för [setConsent](../../../web-sdk/commands/setconsent.md).

## Inkludera medgivandeinformation i sendEvent

Inom XDM-scheman kan du lagra information om medgivandeinställningar från Experience Events. Det finns två sätt att lägga till den här informationen i varje händelse.

Först kan du tillhandahålla relevant XDM-schema för varje `sendEvent`-anrop. I följande exempel visas ett sätt att göra detta:

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

Det här exemplet hämtar medgivandeinformationen för TCF API och skickar sedan en händelse med medgivandeinformationen som lagts till i XDM-schemat.

Det andra sättet att lägga till medgivandeinformationen i varje begäran är med återanropet [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md).

## Nästa steg

Nu när du har lärt dig att använda IAB TCF 2.0 med Experience Platform Web SDK kan du även integrera med andra Adobe-lösningar som Adobe Analytics och Adobe Real-Time Customer Data Platform. Mer information finns i [Översikt över IAB Transparency &amp; Consent Framework 2.0](./overview.md).
