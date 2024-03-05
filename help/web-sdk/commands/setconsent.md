---
title: setConsent
description: Används på varje sida för att spåra användarens samtycke.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# setConsent

The `setConsent` anger för Web SDK om det ska skicka data (opt in), ta bort data (opt out) eller använda [`defaultConsent`](configure/defaultconsent.md) (okänt samtycke).

Web SDK stöder följande standarder:

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Både 1.0- och 2.0-standarder stöds.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Om du använder den här standarden uppdateras besökarens kundprofil i realtid med medgivandeinformationen om implementeringen är korrekt konfigurerad:
   1. Det enskilda XDM-profilschemat innehåller [Fältgruppen IAB TCF 2.0-samtycke](/help/xdm/field-groups/profile/iab.md).
   1. Experience Event-schemat innehåller [Fältgruppen IAB TCF 2.0-samtycke](/help/xdm/field-groups/event/iab.md).
   1. Du inkluderar IAB-medgivandeinformationen i händelsen [XDM-objekt](sendevent/xdm.md). Web SDK inkluderar inte automatiskt medgivandeinformationen när händelsedata skickas.

När du har använt det här kommandot skriver Web SDK användarens inställningar till en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar SDK dessa beständiga inställningar för att avgöra om händelser kan skickas till Adobe.

Adobe rekommenderar att du lagrar medgivandedialogrutor separat från Web SDK-medgivandet. Web SDK erbjuder inte ett sätt att få samtycke. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK:n kan du anropa `setConsent` på varje sida som läses in. Web SDK gör bara ett serveranrop när medgivandet ändras.

## Ange samtycke med hjälp av taggtillägget Web SDK

Inställning av samtycke utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Set consent]**.
1. Ange önskade fält till höger, inklusive **[!UICONTROL Standard]** och **[!UICONTROL General consent]**.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

Du kan inkludera flera objekt för samtycke i den här åtgärden.

## Ange samtycke med hjälp av JavaScript-biblioteket för Web SDK

Kör `setConsent` när du anropar den konfigurerade instansen av Web SDK. Du kan inkludera följande objekt i det här kommandot:

* **`consent[]`**: En array med `consent` objekt. Medgivandeobjektet formateras på olika sätt beroende på vilken standard och version du väljer.
* **`identityMap`**: Ett objekt som styr hur ett ECID genereras och vilka ID:n som godkännandeinformation är knuten till. Adobe rekommenderar att du tar med det här objektet när `setConsent` körs före andra kommandon, till exempel [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Ett objekt som innehåller [åsidosättningar av konfiguration av datastream](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 standard `consent` object

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"Adobe"` för standarden Adobe 2.0.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"2.0"` för standarden Adobe 2.0.
* **`value`**: Ett objekt som innehåller medgivandevärden.
   * **`value.collect.val`**: Medgivandevärdet. Giltiga värden är `"y"` (opt in) och `"n"` (avanmäl dig)
   * **`value.metadata.time`**: Den tidsstämpel som användaren anger medgivandevärdet för.

```js
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### IAB TCF 2.0-standard `consent` object

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"IAB TCF"` för IAB TCF 2.0-standarden.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"2.0"` för IAB TCF 2.0-standarden.
* **`value`**: En sträng som innehåller medgivandevärdet.
* **`gdprApplies`**: Ett booleskt värde som avgör om GDPR gäller för det här medgivandevärdet. Standardvärdet är `true`.
* **`gdprContainsPersonalData`**: Ett booleskt värde som avgör om de händelsedata som är associerade med den här användaren innehåller personuppgifter. Standardvärdet är `false`.

```js
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

>[!TAB Adobe 1.0]

### Adobe 1.0 standard `consent` object

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"Adobe"` för standarden Adobe 1.0.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"1.0"` för standarden Adobe 1.0.
* **`value.general`**: Medgivandevärdet. Giltiga värden är `"in"` (opt in) och `"out"` (avanmäl dig)

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]
