---
title: setConsent
description: Används på varje sida för att spåra dina användares medgivandeinställningar.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# `setConsent`

Kommandot `setConsent` talar om för Web SDK om det ska skicka data (opt in), ta bort data (opt out) eller använda [`defaultConsent`](configure/defaultconsent.md) (samtycke okänt).

Web SDK stöder följande standarder:

* **[Adobe-standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Både 1.0- och 2.0-standarder stöds.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Om du använder den här standarden uppdateras besökarens kundprofil i realtid med medgivandeinformationen om implementeringen är korrekt konfigurerad:
   1. Det enskilda XDM-profilschemat innehåller fältgruppen [IAB TCF 2.0-samtycke](/help/xdm/field-groups/profile/iab.md).
   1. Experience Event-schemat innehåller fältgruppen [IAB TCF 2.0-samtycke](/help/xdm/field-groups/event/iab.md).
   1. Du inkluderar IAB-medgivandeinformationen i händelsen [XDM-objekt](sendevent/xdm.md). Web SDK inkluderar inte information om samtycke automatiskt när händelsedata skickas.

När du använder det här kommandot skriver Web SDK användarens inställningar till [`kndctr_<orgId>_consent`](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/cookies/web-sdk)-cookien. Den här cookien anges oavsett besökarens medgivandeinställningar, eftersom den lagrar besökarens medgivandeinställningar. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar SDK dessa beständiga inställningar för att avgöra om händelser kan skickas till Adobe.

Adobe rekommenderar att du lagrar medgivandedialogrutor separat från Web SDK-medgivanden. SDK på webben erbjuder inget sätt att få samtycke. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK kan du anropa kommandot `setConsent` vid varje sidinläsning. Web SDK gör bara ett serveranrop när medgivandet ändras.

## Överväganden om identitetssynkronisering {#identity-considerations}

Kommandot `setConsent` använder bara `ECID` från identitetskartan eftersom kommandot används på enhetsnivå. Andra identiteter från identitetskartan beaktas inte av kommandot `setConsent`.

## Använder `defaultConsent` tillsammans med `setConsent` {#using-consent}

Web SDK har två extra konfigurationskommandon för samtycke:

* [`defaultConsent`](configure/defaultconsent.md): Det här kommandot anger automatiskt besökarens standardinställning för samtycke innan `setConsent` anropas.
* `setConsent` (aktuell sida): Det här kommandot anger uttryckligen besökarens inställning för samtycke.

När de används tillsammans kan de här inställningarna leda till olika resultat för datainsamling och cookie-inställning, beroende på deras konfigurerade värden:

| `defaultConsent` | `setConsent` | Datainsamling sker | Web SDK anger cookies i webbläsare |
| --- | --- | --- | --- |
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nej | Ja |
| `in` | Ej angiven | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nej | Ja |
| `pending` | Ej angiven | Nej | Nej |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nej | Ja |
| `out` | Ej angiven | Nej | Nej |

Se [Adobe Experience Platform Web SDK-cookies](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/cookies/web-sdk) i guiden för bastjänster för en fullständig lista över cookies som kan anges.

## Använda kommandot `setConsent`

Kör kommandot `setConsent` när du anropar den konfigurerade instansen av Web SDK. Du kan inkludera följande objekt i det här kommandot:

* **`consent[]`**: En array med `consent` objekt. Medgivandeobjektet formateras på olika sätt beroende på vilken standard och version du väljer. Se flikarna nedan för exempel på varje samtyckesobjekt, beroende på medgivandestandarden.
* **`identityMap`**: Ett objekt som styr hur ett ECID genereras och vilka ID:n som godkännandeinformation är knuten till. Adobe rekommenderar att du inkluderar det här objektet när `setConsent` körs före andra kommandon, till exempel [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Ett objekt som innehåller [datastream-konfiguration åsidosätter &#x200B;](configure/edgeconfigoverrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0-standardobjekt `consent`

Om du skickar data till Adobe Experience Platform bör du inkludera en fältgrupp för sekretessschema i ditt profilschema. Mer information om Adobe 2.0 finns i [Styrning, sekretess och säkerhet i Adobe Experience Platform](/help/landing/governance-privacy-security/overview.md). Du kan lägga till data i värdeobjektet nedan som motsvarar schemat för fältet `consents` i profilfältgruppen [!UICONTROL Consents and Preferences].

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"Adobe"` för Adobe 2.0-standarden.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"2.0"` för Adobe 2.0-standarden.
* **`value`**: Ett objekt som innehåller medgivandevärden.
   * **`value.collect.val`**: Medgivandevärdet. Ange detta till `"y"` när användare väljer att delta och till `"n"` när användare avanmäler sig.
   * **`value.metadata.time`**: Tidsstämpeln när användarna senast uppdaterade sina inställningar för godkännande.

```js
// Set consent using the Adobe 2.0 standard
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

### IAB TCF 2.0-standardobjekt `consent`

Om du vill registrera inställningar för användargodkännande som tillhandahålls via Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF) anger du medgivandesträngen enligt nedan.

När medgivandet har ställts in på det här sättet uppdateras kundprofilen i realtid med medgivandeinformationen. För att detta ska fungera måste profilens XDM-schema innehålla [schemafältgruppen för profilsekretess](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). När händelser skickas måste IAB:s medgivandeinformation läggas till manuellt i händelsens XDM-objekt. Webb-SDK inkluderar inte automatiskt medgivandeinformationen i händelserna.

Om du vill skicka information om samtycke i händelser måste du lägga till fältgruppen för sekretess för upplevelsehändelser i ditt [!DNL Profile]-aktiverade [!DNL XDM ExperienceEvent]-schema. I avsnittet [Uppdatera ExperienceEvent-schemat](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema) i guiden för datauppsättningsförberedelser finns mer information om hur du konfigurerar det här.

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"IAB TCF"` för IAB TCF 2.0-standarden.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"2.0"` för IAB TCF 2.0-standarden.
* **`value`**: En sträng som innehåller medgivandevärdet.
* **`gdprApplies`**: Ett booleskt värde som avgör om GDPR gäller för det här medgivandevärdet. Dess standardvärde är `true`.
* **`gdprContainsPersonalData`**: Ett booleskt värde som avgör om händelsedata som är associerade med den här användaren innehåller personuppgifter. Dess standardvärde är `false`.

```js
// Set consent using the IAB TCF 2.0 standard
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

API:t IAB TCF 2.0 innehåller en händelse för när kunden uppdaterar medgivandet. Detta inträffar när kunden från början ställer in sina inställningar och när kunden uppdaterar sina inställningar. Du kan lägga till en händelseavlyssnare för att köra kommandot `setConsent`:

```js
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

Ovanstående kodblock lyssnar efter `useractioncomplete`-händelsen och anger sedan medgivandet och skickar medgivandesträngen och `gdprApplies`-flaggan. Om du har anpassade identiteter för dina kunder måste du fylla i variabeln `identityMap`.

>[!TAB Adobe 1.0]

### Adobe 1.0-standardobjekt `consent`

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"Adobe"` för Adobe 1.0-standarden.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"1.0"` för Adobe 1.0-standarden.
* **`value.general`**: Medgivandevärdet. Ange detta till `"in"` när användare väljer att delta och till `"out"` när användare avanmäler sig.

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

### Skicka flera standarder i en begäran {#multiple-standards}

Web SDK har också stöd för att skicka fler än ett medgivandeobjekt i en begäran, vilket visas i exemplet nedan.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "YYYY-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## Förhållanden för samtycke {#persistence}

När du har skickat användarinställningar till Web SDK med hjälp av kommandot `setConsent`, kommer SDK att behålla användarinställningarna för en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar och använder Web SDK dessa beständiga inställningar för att avgöra om händelser kan skickas till Adobe eller inte.

Lagra användarens inställningar oberoende av varandra så att du kan visa medgivandedialogrutan med de aktuella inställningarna. Det går inte att hämta användarinställningarna från Web SDK. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK kan du anropa kommandot `setConsent` vid varje sidinläsning. Web SDK gör bara ett serveranrop om inställningarna ändras.

## Ange samtycke med hjälp av taggtillägget Web SDK

Webbtaggtillägget för SDK som är ekvivalent med det här kommandot är åtgärden [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md).
