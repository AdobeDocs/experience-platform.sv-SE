---
title: Integrera stödet för IAB TCF 2.0 med Adobe Experience Platform Web SDK
description: Lär dig hur du ställer in stöd för IAB TCF 2.0 för din webbplats utan att använda taggar.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Integrera stödet för IAB TCF 2.0 med Platform Web SDK

Den här guiden visar hur du integrerar Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0) med Adobe Experience Platform Web SDK utan att använda taggar. En översikt över integrationen med IAB TCF 2.0 finns i [översikt](./overview.md). En guide om hur du integrerar med taggar finns i [Guiden IAB TCF 2.0 för taggar](./with-tags.md).

## Komma igång

Den här guiden använder `__tcfapi` gränssnittet för att få tillgång till information om samtycke. Det kan vara enklare för er att integrera direkt med ert molnhanteringsföretag (CMP). Informationen i den här handboken kan dock fortfarande vara användbar eftersom CMP i allmänhet har funktioner som liknar TCF API.

>[!NOTE]
>
>Exemplen förutsätter att koden körs innan `window.__tcfapi` är definierad på sidan. CMP kan tillhandahålla en krok där du kan köra dessa funktioner när `__tcfapi` objektet är klart.

Om du vill använda IAB TCF 2.0 med taggar och Adobe Experience Platform Web SDK-tillägget måste du ha ett XDM-schema tillgängligt. Om du inte har konfigurerat något av dessa kan du börja med att visa den här sidan innan du fortsätter.

Den här guiden kräver dessutom att du har en fungerande förståelse för Adobe Experience Platform Web SDK. Om du vill ha en snabb uppdatering kan du läsa [Adobe Experience Platform Web SDK - översikt](../../home.md) och [Frågor och svar](../../faq.md) dokumentation.

## Aktivera standardmedgivande

Om du vill behandla alla okända användare på samma sätt kan du ange [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) till `pending` eller `out`. Detta köar eller tar bort Experience Events tills du får medgivandeinställningarna.

### Ange standardsamtycke baserat på `gdprApplies`

Vissa datahanteringsplattformar gör det möjligt att avgöra om den allmänna dataskyddsförordningen (GDPR) gäller för kunden. Om du vill anta samtycke för kunder där GDPR inte gäller kan du använda `gdprApplies` -flaggan i TCF API-anropet.

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

I det här exemplet `configure` anropas efter `tcData` hämtas från TCF API. If `gdprApplies` är true, standardsamtycke är inställt på `pending`. If `gdprApplies` är falskt, standardsamtycke är inställt på `in`. Var noga med att fylla i `alloyConfiguration` med din konfiguration.

>[!NOTE]
>
>När standardsamtycke är inställt på `in`, `setConsent` kan fortfarande användas för att registrera dina kunders medgivandeinställningar.

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

Det här kodblocket lyssnar efter `useractioncomplete` -händelsen och anger sedan medgivandet, skickar medgivandesträngen och `gdprApplies` flagga. Om ni har anpassade identiteter för era kunder måste ni fylla i `identityMap` variabel. Se guiden på [stödjande samtycke](../../consent/supporting-consent.md) för mer information om telefonsamtal `setConsent`.

## Inkludera medgivandeinformation i sendEvent

Inom XDM-scheman kan du lagra information om medgivandeinställningar från Experience Events. Det finns två sätt att lägga till den här informationen i varje händelse.

Först kan du ange relevant XDM-schema för varje `sendEvent` ring. I följande exempel visas ett sätt att göra detta:

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

Det andra sättet att lägga till medgivandeinformationen i varje begäran är med [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) återanrop.

## Nästa steg

Nu när du har lärt dig att använda IAB TCF 2.0 med Platform Web SDK-tillägget kan du även integrera med andra Adobe-lösningar som Adobe Analytics eller Adobe Real-time Customer Data Platform. Se [Översikt över IAB Transparency &amp; Consent Framework 2.0](./overview.md) för mer information.
