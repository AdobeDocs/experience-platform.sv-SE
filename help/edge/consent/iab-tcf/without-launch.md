---
title: Använda IAB TCF 2.0 utan Experience Platform Launch
seo-title: Konfigurera IAB TCF 2.0-samtycke med Adobe Experience Platform Web SDK
description: Lär dig hur du ställer in IAB TCF 2.0-samtycke med Adobe Experience Platform Web SDK
seo-description: Lär dig hur du ställer in IAB TCF 2.0-samtycke med Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---


# Använda IAB TCF 2.0 med AEP Web SDK-tillägget

Den här guiden visar hur du integrerar Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0) med Adobe Experience Platform Web SDK utan att använda Experience Platform Launch. En översikt över integrationen med IAB TCF 2.0 finns i [översikten](./overview.md). En guide om hur du integrerar med Experience Platform Launch finns i [IAB TCF 2.0 guide for Experience Platform Launch](./with-launch.md).

## Komma igång

Den här guiden använder gränssnittet för att få åtkomst till informationen om samtycke. `__tcfapi` Det kan vara enklare för er att integrera direkt med ert molnhanteringsföretag (CMP). Informationen i den här handboken kan dock fortfarande vara användbar eftersom CMP i allmänhet har funktioner som liknar TCF API.

>[!NOTE]
>
>Exemplen förutsätter att koden har definierats på sidan när den körs `window.__tcfapi` . CMP kan tillhandahålla en krok där du kan köra dessa funktioner när `__tcfapi` objektet är klart.

Om du vill använda IAB TCF 2.0 med Experience Platform Launch och AEP Web SDK-tillägget måste du ha ett XDM-schema tillgängligt. Om du inte har konfigurerat något av dessa kan du börja med att visa den här sidan innan du fortsätter.

Den här guiden kräver dessutom att du har en fungerande förståelse för Adobe Experience Platform Web SDK. Läs översikten [för](../../home.md) Adobe Experience Platform Web SDK och dokumentationen med [vanliga frågor och svar](../../web-sdk-faq.md) om en snabb uppdatering.

## Aktivera standardmedgivande

Om du vill behandla alla okända användare på samma sätt, kan du ställa in standardmedgivandet till `pending`. Detta köar Experience Events tills medgivandeinställningarna har tagits emot.

Mer information om standardmedgivande finns i avsnittet [om](../../fundamentals/configuring-the-sdk.md#default-consent) standardmedgivande i konfigurationsdokumentationen för Platform Web SDK.

### Ange standardsamtycke baserat på `gdprApplies`

Vissa datahanteringsplattformar gör det möjligt att avgöra om den allmänna dataskyddsförordningen (GDPR) gäller för kunden. Om du vill anta samtycke för kunder där GDPR inte gäller, kan du använda flaggan `gdprApplies` i TCF API-anropet.

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

I det här exemplet anropas `configure` kommandot efter att `tcData` det har hämtats från TCF API. Om `gdprApplies` är true anges standardsamtycke till `pending`. Om `gdprApplies` är false anges standardsamtycke till `in`. Var noga med att fylla i `alloyConfiguration` variabeln med din konfiguration.

>[!NOTE]
>
>När standardinställningen för samtycke är `in`tillgänglig kan `setConsent` kommandot fortfarande användas för att registrera dina kunders medgivandeinställningar.

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

Det här kodblocket lyssnar efter `useractioncomplete` händelsen och anger sedan medgivandet och skickar strängen och `gdprApplies` flaggan. Om du har anpassade identiteter för dina kunder måste du fylla i `identityMap` variabeln. Mer information om hur du ringer finns i guiden om [stöd för samtycke](../../consent/supporting-consent.md) `setConsent`.

## Inkludera medgivandeinformation i sendEvent

Inom XDM-scheman kan du lagra information om medgivandeinställningar från Experience Events. Det finns två sätt att lägga till den här informationen i varje händelse.

Först kan du tillhandahålla relevant XDM-schema vid varje `sendEvent` samtal. I följande exempel visas ett sätt att göra detta:

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

Det här exemplet hämtar medgivandeinformationen för TCF API och skickar sedan en händelse med medgivandeinformationen som lagts till i XDM-schemat. I guiden [Spåra händelser](../../fundamentals/tracking-events.md) finns information om vad som ska finnas i `sendEvent` kommandoalternativen.

Det andra sättet att lägga till medgivandeinformationen i varje begäran är med `onBeforeEventSend` callback-funktionen. Mer information om hur du gör detta finns i avsnittet om att [ändra händelser globalt](../../fundamentals/tracking-events.md#modifying-events-globally) i dokumentationen för spårningshändelser.

## Nästa steg

Nu när du har lärt dig att använda IAB TCF 2.0 med AEP Web SDK-tillägget kan du även integrera med andra Adobe-lösningar som Adobe Analytics eller kunddataplattformen i realtid. Mer information finns i [IAB Transparency &amp; Consent Framework 2.0-översikten](./overview.md) .
