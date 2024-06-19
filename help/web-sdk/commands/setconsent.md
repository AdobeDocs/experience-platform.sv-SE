---
title: setConsent
description: Används på varje sida för att spåra dina användares medgivandeinställningar.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---


# `setConsent`

The `setConsent` anger för Web SDK om det ska skicka data (opt in), ta bort data (opt out) eller använda [`defaultConsent`](configure/defaultconsent.md) (okänt samtycke).

Web SDK stöder följande standarder:

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Både 1.0- och 2.0-standarder stöds.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Om du använder den här standarden uppdateras besökarens kundprofil i realtid med medgivandeinformationen om implementeringen är korrekt konfigurerad:
   1. Det enskilda XDM-profilschemat innehåller [Fältgruppen IAB TCF 2.0-samtycke](/help/xdm/field-groups/profile/iab.md).
   1. Experience Event-schemat innehåller [Fältgruppen IAB TCF 2.0-samtycke](/help/xdm/field-groups/event/iab.md).
   1. Du inkluderar IAB-medgivandeinformationen i händelsen [XDM-objekt](sendevent/xdm.md). Web SDK inkluderar inte automatiskt medgivandeinformationen när händelsedata skickas.

När du har använt det här kommandot skriver Web SDK användarens inställningar till en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar SDK dessa beständiga inställningar för att avgöra om händelser kan skickas till Adobe.

Adobe rekommenderar att du lagrar medgivandedialogrutor separat från Web SDK-medgivandet. Web SDK erbjuder inte ett sätt att få samtycke. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK:n kan du anropa `setConsent` på varje sida som läses in. Web SDK gör bara ett serveranrop när medgivandet ändras.

## Använda `defaultConsent` tillsammans med `setConsent` {#using-consent}

Web SDK har två extra konfigurationskommandon för samtycke:

* [`defaultConsent`](configure/defaultconsent.md): Det här kommandot är avsett att fånga upp medgivandepreferenser för Adobe-kunder med hjälp av Web SDK.
* [`setConsent`](setconsent.md): Det här kommandot är avsett att fånga upp webbplatsbesökarnas medgivandepreferenser.

När de används tillsammans kan de här inställningarna leda till olika resultat för datainsamling och cookie-inställning, beroende på deras konfigurerade värden.

Se tabellen nedan för att förstå när datainsamling sker och när cookies ställs in, baserat på inställningar för samtycke.

| defaultConsent | setConsent | Datainsamling sker | Webb-SDK anger webbläsarcookies |
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

Följande cookies anges när medgivandekonfigurationen tillåter:

| Namn | Maximal ålder | Beskrivning |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 dagar) | Visas när [`idMigrationEnabled`](configure/idmigrationenabled.md) är aktiverat. Det hjälper när du går över till Web SDK medan vissa delar av webbplatsen fortfarande använder `visitor.js`. |
| **Demdex cookie** | 15552000 (180 dagar) | Visas om ID-synkronisering är aktiverat. Audience Manager ställer in denna cookie så att den tilldelar ett unikt ID till en besökare. Demdex-cookie hjälper Audience Manager att utföra grundläggande funktioner som besökaridentifiering, ID-synkronisering, segmentering, modellering, rapportering och så vidare. |
| **kndctr_orgid_Cluster** | 1 800 (30 minuter) | Lagrar det Edge Network-område som betjänar den aktuella användarens begäran. Regionen används i URL-sökvägen så att Edge Network kan dirigera begäran till rätt region. Om en användare ansluter till en annan IP-adress eller i en annan session dirigeras begäran igen till närmaste region. |
| **kndct_orgid_identity** | 34128000 (395 dagar) | Lagrar ECID samt annan information som rör ECID. |
| **kndctr_orgid_medgivande** | 15552000 (180 dagar) | Lagrar användarens medgivandeinställning för webbplatsen. |
| **s_ecid** | 63115200 (två år) | Innehåller en kopia av Experience Cloud-ID ([!DNL ECID]) eller MID MID lagras i ett nyckelvärdepar som följer syntaxen, `s_ecid=MCMID\|<ECID>`. |

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

* **`consent[]`**: En array med `consent` objekt. Medgivandeobjektet formateras på olika sätt beroende på vilken standard och version du väljer. Se flikarna nedan för exempel på varje samtyckesobjekt, beroende på medgivandestandarden.
* **`identityMap`**: Ett objekt som styr hur ett ECID genereras och vilka ID:n som godkännandeinformation är knuten till. Adobe rekommenderar att du tar med det här objektet när `setConsent` körs före andra kommandon, till exempel [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Ett objekt som innehåller [åsidosättningar av konfiguration av datastream](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 standard `consent` object

Om du använder Adobe Experience Platform måste du inkludera en fältgrupp för sekretessschema i ditt profilschema. Se [Styrning, integritet och säkerhet i Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) för mer information om Adobe 2.0-standarden. Du kan lägga till data i värdeobjektet nedan som motsvarar schemat för `consents` fält för [!UICONTROL Consents and Preferences] profilfältgrupp.

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"Adobe"` för standarden Adobe 2.0.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"2.0"` för standarden Adobe 2.0.
* **`value`**: Ett objekt som innehåller medgivandevärden.
   * **`value.collect.val`**: Medgivandevärdet. Ställ in den här till `"y"` när användare väljer att delta och `"n"` när användare avanmäler sig.
   * **`value.metadata.time`**: Tidsstämpeln när användarna senast uppdaterade sina inställningar för samtycke.

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

### IAB TCF 2.0-standard `consent` object

Om du vill registrera inställningar för användargodkännande som tillhandahålls via standarden IAB (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF) anger du medgivandesträngen enligt nedan.

När medgivandet har ställts in på det här sättet uppdateras kundprofilen i realtid med medgivandeinformationen. För att detta ska fungera måste profilen i XDM-schemat innehålla [Fältgrupp för profilsekretesschema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). När händelser skickas måste IAB:s medgivandeinformation läggas till manuellt i händelsens XDM-objekt. Web SDK inkluderar inte automatiskt medgivandeinformationen i händelserna.

Om du vill skicka information om samtycke i händelser måste du lägga till fältgruppen Sekretess för händelser i din [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] schema. Se avsnittet om [uppdatera ExperienceEvent-schemat](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) i guiden för datauppsättningsförberedelse för att få information om hur du konfigurerar detta.

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"IAB TCF"` för IAB TCF 2.0-standarden.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"2.0"` för IAB TCF 2.0-standarden.
* **`value`**: En sträng som innehåller medgivandevärdet.
* **`gdprApplies`**: Ett booleskt värde som avgör om GDPR gäller för det här medgivandevärdet. Standardvärdet är `true`.
* **`gdprContainsPersonalData`**: Ett booleskt värde som avgör om de händelsedata som är associerade med den här användaren innehåller personuppgifter. Standardvärdet är `false`.

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

>[!TAB Adobe 1.0]

### Adobe 1.0 standard `consent` object

* **`standard`**: Den standard för samtycke som du väljer. Ange den här egenskapen som `"Adobe"` för standarden Adobe 1.0.
* **`version`**: En sträng som representerar versionen av medgivandestandarden. Ange den här egenskapen som `"1.0"` för standarden Adobe 1.0.
* **`value.general`**: Medgivandevärdet. Ställ in den här till `"in"` när användare väljer att delta och `"out"` när användare avanmäler sig.

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
                time: "2021-03-17T15:48:42-07:00"
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

När du har skickat användarinställningar till Web SDK med `setConsent` SDK-kommandot behåller användarinställningarna för en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar och använder Web SDK dessa beständiga inställningar för att avgöra om händelser kan skickas till Adobe eller inte.

Du måste lagra användarinställningarna oberoende av varandra för att kunna visa dialogrutan för samtycke med de aktuella inställningarna. Det finns inget sätt att hämta användarinställningar från Web SDK. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK:n kan du anropa `setConsent` på varje sida som läses in. Web SDK gör bara ett serveranrop om inställningarna har ändrats.

## Synkronisera identiteter när du ställer in samtycke {#sync-identities}

När standardsamtycke (anges via [defaultConsent](configure/defaultconsent.md) parameter) är inställd på `pending` eller `out`, `setConsent` inställningen kan vara den första begäran som skickas ut och fastställer identitet. På grund av detta kan det vara viktigt att synkronisera identiteter på den första begäran. Du kan lägga till identitetskartan i `setConsent` på samma sätt som på `sendEvent` -kommando. Se [med identityMap](../identity/overview.md#using-identitymap) om du vill ha ett exempel på hur du inkluderar identitetskartan i kommandot.
