---
title: setConsent
description: Används på varje sida för att spåra dina användares medgivandeinställningar.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 83b4745693749c5f50791d6efeb3a7ba02a4cce5
workflow-type: tm+mt
source-wordcount: '1307'
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

När du har använt det här kommandot skriver Web SDK användarens inställningar till en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar SDK dessa beständiga inställningar för att avgöra om händelser kan skickas till Adobe.

Adobe rekommenderar att du lagrar medgivandedialogrutor separat från Web SDK-medgivanden. SDK på webben erbjuder inget sätt att få samtycke. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK kan du anropa kommandot `setConsent` vid varje sidinläsning. Web SDK gör bara ett serveranrop när medgivandet ändras.

## Överväganden om identitetssynkronisering {#identity-considerations}

Kommandot `setConsent` använder bara `ECID` från identitetskartan eftersom kommandot används på enhetsnivå. Andra identiteter från identitetskartan beaktas inte av kommandot `setConsent`.

## Använder `defaultConsent` tillsammans med `setConsent` {#using-consent}

Web SDK har två extra konfigurationskommandon för samtycke:

* [`defaultConsent`](configure/defaultconsent.md): Det här kommandot är avsett att fånga upp medgivandepreferenser för Adobe-kunder med hjälp av Web SDK.
* [`setConsent`](setconsent.md): Det här kommandot är avsett att fånga upp webbplatsbesökarnas medgivandeinställningar.

När de används tillsammans kan de här inställningarna leda till olika resultat för datainsamling och cookie-inställning, beroende på deras konfigurerade värden.

Se tabellen nedan för att förstå när datainsamling sker och när cookies ställs in, baserat på inställningar för samtycke.

| defaultConsent | setConsent | Datainsamling sker | Web SDK anger cookies i webbläsare |
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
| **AMCV_###@AdobeOrg** | 34128000 (395 dagar) | Visas när [`idMigrationEnabled`](configure/idmigrationenabled.md) är aktiverat. Det är till hjälp vid övergång till Web SDK medan vissa delar av webbplatsen fortfarande använder `visitor.js`. |
| **Demdex-cookie** | 15552000 (180 dagar) | Visas om ID-synkronisering är aktiverat. Audience Manager ställer in denna cookie så att en besökare tilldelas ett unikt ID. Demdex-cookie hjälper Audience Manager att utföra grundläggande funktioner som besökaridentifiering, ID-synkronisering, segmentering, modellering, rapportering och så vidare. |
| **kndctr_orgid_Cluster** | 1 800 (30 minuter) | Lagrar den Edge Network-region som betjänar den aktuella användarens begäran. Regionen används i URL-sökvägen så att Edge Network kan dirigera begäran till rätt region. Om en användare ansluter till en annan IP-adress eller i en annan session dirigeras begäran igen till närmaste region. |
| **kndct_orgid_identity** | 34128000 (395 dagar) | Lagrar ECID samt annan information som rör ECID. |
| **kndctr_orgid_medgivande** | 15552000 (180 dagar) | Lagrar användarens medgivandeinställning för webbplatsen. |
| **s_ecid** | 63115200 (två år) | Innehåller en kopia av Experience Cloud-ID ([!DNL ECID]) eller MID. MID lagras i ett nyckel/värde-par som följer syntaxen `s_ecid=MCMID\|<ECID>`. |

## Ange samtycke med hjälp av taggtillägget Web SDK

Inställning av samtycke utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Set consent]**.
1. Ange önskade fält till höger, inklusive **[!UICONTROL Standard]** och **[!UICONTROL General consent]**.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

Du kan inkludera flera objekt för samtycke i den här åtgärden.

## Ange samtycke med hjälp av Web SDK JavaScript-biblioteket

Kör kommandot `setConsent` när du anropar den konfigurerade instansen av Web SDK. Du kan inkludera följande objekt i det här kommandot:

* **`consent[]`**: En array med `consent` objekt. Medgivandeobjektet formateras på olika sätt beroende på vilken standard och version du väljer. Se flikarna nedan för exempel på varje samtyckesobjekt, beroende på medgivandestandarden.
* **`identityMap`**: Ett objekt som styr hur ett ECID genereras och vilka ID:n som godkännandeinformation är knuten till. Adobe rekommenderar att du inkluderar det här objektet när `setConsent` körs före andra kommandon, till exempel [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Ett objekt som innehåller [datastream-konfiguration åsidosätter ](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0-standardobjekt `consent`

Om du använder Adobe Experience Platform måste du inkludera en fältgrupp för sekretessschema i ditt profilschema. Mer information om Adobe 2.0 finns i [Styrning, sekretess och säkerhet i Adobe Experience Platform](../../landing/governance-privacy-security/overview.md). Du kan lägga till data i värdeobjektet nedan som motsvarar schemat för fältet `consents` i profilfältgruppen [!UICONTROL Consents and Preferences].

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

Om du vill skicka information om samtycke i händelser måste du lägga till fältgruppen för sekretess för upplevelsehändelser i ditt [!DNL Profile]-aktiverade [!DNL XDM ExperienceEvent]-schema. I avsnittet [Uppdatera ExperienceEvent-schemat](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) i guiden för datauppsättningsförberedelser finns mer information om hur du konfigurerar det här.

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

När du har skickat användarinställningar till Web SDK med hjälp av kommandot `setConsent`, kommer SDK att behålla användarinställningarna för en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar och använder Web SDK dessa beständiga inställningar för att avgöra om händelser kan skickas till Adobe eller inte.

Du måste lagra användarinställningarna oberoende av varandra för att kunna visa dialogrutan för samtycke med de aktuella inställningarna. Det går inte att hämta användarinställningarna från Web SDK. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK kan du anropa kommandot `setConsent` vid varje sidinläsning. Web SDK gör bara ett serveranrop om inställningarna har ändrats.
