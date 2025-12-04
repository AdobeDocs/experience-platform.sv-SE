---
title: defaultConsent
description: Ange standardmetoden för insamling av samtycke för din webbegenskap.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 1e272eb18fac2f59f9737756d48947a25573d772
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# `defaultConsent`

Egenskapen `defaultConsent` avgör hur du hanterar datainsamlingssamtycke innan du anropar kommandot [`setConsent`](../setconsent.md). Den här egenskapen är värdefull när du inte av misstag vill samla in data från personer som bor i områden där samtycke krävs innan data samlas in.

Om du har en besökare som inte omfattas av den allmänna dataskyddsförordningen (GDPR) kan standardmedgivandet anges till `in`. Besökare inom GDPR:s jurisdiktion kan ha sitt standardsamtycke inställt på `pending`. Din CMP (Consent Management Platform) kan identifiera kundens region och ange flaggan `gdprApplies` till IAB TCF 2.0. Den här flaggan kan användas för att ange standardsamtycke.

Ange strängegenskapen `defaultConsent` till önskad medgivandenivå när du kör kommandot `configure`. Den här egenskapen är skiftlägeskänslig och stöder endast följande tre värden: `"in"`, `"out"` och `"pending"`. Om du försöker använda något annat värde genereras ett fel i biblioteket. Om det inte anges i kommandot `configure` är standardvärdet **`in`**.

>[!IMPORTANT]
>
>Värdet `defaultConsent` finns inte kvar mellan sidinläsningar. Se till att du anger önskat standardsamtycke varje gång du anropar kommandot `configure`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**: Datainsamlingen fungerar normalt tills användaren väljer bort.
* **`out`**: Data ignoreras permanent tills användaren väljer att gå in.
* **`pending`**: Data lagras lokalt tills användaren väljer att använda kommandot [`setConsent`](../setconsent.md).

>[!NOTE]
>
>Även om Adobe planerar att bygga en mer robust uppsättning syften eller kategorier som motsvarar Adobe funktioner och produkterbjudanden är den nuvarande implementeringen en strategi där man väljer att inte ta del av någonting. Den här begränsningen gäller endast för Web SDK och inte andra Adobe JavaScript-bibliotek.

## Använder `defaultConsent` tillsammans med `setConsent` {#using-consent}

SDK på webben har två alternativ:

* `defaultConsent` (den här sidan): Anger standardinställningar för samtycke.
* [`setConsent`](../setconsent.md): Fånga besökarnas samtycke.

När de används tillsammans kan de här inställningarna leda till olika resultat för datainsamling och cookie-inställning, beroende på deras konfigurerade värden.

Se tabellen nedan för att förstå när datainsamling sker och när cookies ställs in, baserat på inställningar för samtycke.

| `defaultConsent` | `setConsent` | Datainsamling sker | Web SDK anger cookies i webbläsare |
|---------|----------|---------|---------|
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nej | Ja |
| `in` | Ej angiven | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nej | Ja |
| `pending` | Ej angiven | Nej | Nej |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nej | Ja |
| `out` | Ej angiven | Nej | Nej |

Se [Adobe Experience Platform Web SDK-cookies](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/cookies/web-sdk) för en lista över cookies som biblioteket anger.

>[!NOTE]
>
>Identitets- och medgivandecookies anges även om en besökare avanmäler sig från spårning. Dessa cookies är nödvändiga för att uppfylla deras inställningar för datainsamling.

## Ange standardsamtycke baserat på `gdprApplies`

Vissa datahanteringsplattformar gör det möjligt att avgöra om den allmänna dataskyddsförordningen (GDPR) gäller för kunden. Om du vill anta samtycke för kunder där GDPR inte gäller kan du använda flaggan `gdprApplies` i ett TCF API-anrop. Exempel:

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

I ovanstående kodblock anropas kommandot `configure` efter att `tcData` har hämtats från TCF API. Om `gdprApplies` är true anges standardmedgivande till `pending`. Om `gdprApplies` är falskt anges standardsamtycke till `in`. Se till att du fyller i variabeln `alloyConfiguration` med din konfiguration.

## Standardsamtycke med hjälp av taggtillägget Web SDK

Se [Inställningar för samtycke](/help/tags/extensions/client/web-sdk/configure/consent.md) i dokumentationen för SDK-taggtillägget för webben om du vill veta hur du utför de här åtgärderna med hjälp av taggar.
