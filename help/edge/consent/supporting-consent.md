---
title: Supporting Customer Consent Preferences Using the Adobe Experience Platform Web SDK
description: Lär dig hur du stöder medgivandeinställningar med Adobe Experience Platform Web SDK.
keywords: medgivande;defaultConsent;standard medgivande;setConsent;Profile Privacy field group;Experience Event Privacy field group;Privacy field group;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Stöd för kundernas samtycke

Om du vill respektera användarens sekretess kan du be om användarens samtycke innan du tillåter att SDK använder användarspecifika data för vissa syften. För närvarande tillåter SDK endast användare att välja mellan att inte göra det, men i framtiden hoppas Adobe kunna ge mer exakt kontroll över specifika syften.

Om användaren väljer alla syften får SDK utföra följande uppgifter:

* Skicka data till och från Adobe-servrar.
* Läs och skriv cookies eller webblagringsobjekt.

Om användaren väljer bort alla syften utför SDK inte någon av dessa åtgärder.

## Konfigurera samtycke

Som standard väljs användaren i alla syften. För att förhindra att SDK utför ovanstående uppgifter tills användaren väljer att inte göra det skickar du `"defaultConsent": "pending"` under SDK-konfigurationen enligt följande:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

När standardmedgivandet för det allmänna syftet är inställt på väntande, försöker köra kommandon som är beroende av användarens inställningar för deltagande (till exempel `sendEvent` -kommando) köas kommandot i SDK:n. Dessa kommandon bearbetas inte förrän du har meddelat användarens inställningar för deltagande till SDK.

>[!NOTE]
>
>Kommandon står bara i kö i minnet. De sparas inte över sidinläsningar.

Om du inte vill samla in händelser som inträffat innan användarens inställningar för anmälan har angetts, kan du skicka `"defaultConsent": "out"` under SDK-konfigurationen. Försök att köra kommandon som är beroende av användarens inställningar för deltagande kommer inte att ha någon effekt förrän du har meddelat användarens inställningar för deltagande till SDK.

>[!NOTE]
>
>För närvarande stöder SDK endast ett enda syfte, helt eller ingenting. Även om vi planerar att bygga ut en mer robust uppsättning syften eller kategorier som kommer att motsvara de olika möjligheterna och produkterbjudandena för Adobe, är den nuvarande implementeringen en metod som helt eller inte alls kan användas.  Detta gäller endast Adobe Experience Platform [!DNL Web SDK] och INTE andra JavaScript-bibliotek från Adobe.

Nu kanske du föredrar att be användaren att välja någonstans i användargränssnittet. När användarens inställningar har samlats in kan du meddela SDK:n dessa inställningar.

## Kommunicera medgivandepreferenser via Adobe Experience Platform-standarden

SDK stöder version 1.0 och 2.0 av Adobe Experience Platform medgivandestandard. För närvarande stöder 1.0- och 2.0-standarderna endast automatisk tillämpning av en helt eller inget medgivande. 1.0-standarden fasas ut till förmån för 2.0-standarden. Med standarden 2.0 kan du lägga till ytterligare medgivandeinställningar som kan användas för att manuellt tillämpa medgivandeinställningar.

### Använda Adobe standardversion 2.0

Om du använder Adobe Experience Platform måste du inkludera en fältgrupp för sekretessschema i ditt profilschema. Se [Styrning, integritet och säkerhet i Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) om du vill ha mer information om Adobe standardversion 2.0. Du kan lägga till data i värdeobjektet nedan som motsvarar schemat för `consents` fält för [!UICONTROL Consents and Preferences] profilfältgrupp.

Kör `setConsent` med inställningen för att samla in `y` enligt följande:

```javascript
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
    }]
});
```

Tidsfältet ska ange när användaren senast uppdaterade sina medgivandeinställningar. Om användaren väljer att avanmäla sig kör du `setConsent` med inställningen för att samla in `n` enligt följande:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### Använda Adobe standardversion 1.0

Kör `setConsent` med `general` alternativ inställt på `in` enligt följande:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

Om användaren väljer att avanmäla sig kör du `setConsent` med `general` alternativ inställt på `out` enligt följande:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

## Kommunicera medgivandepreferenser via IAB TCF-standarden

SDK har stöd för inspelning av en användares medgivandepreferenser via IAB-standarden (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF). Medgivandesträngen kan anges med samma `setConsent` så här:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

När medgivandet har ställts in på det här sättet uppdateras kundprofilen i realtid med medgivandeinformationen. För att detta ska fungera måste profilen i XDM-schemat innehålla [Fältgrupp för profilsekretesschema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). När händelser skickas måste IAB:s medgivandeinformation läggas till manuellt i händelsens XDM-objekt. SDK inkluderar inte automatiskt information om samtycke i händelserna. Om du vill skicka information om samtycke i händelser, [Fältgruppen Experience Event Privacy](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) måste läggas till i Experience Event-schemat.

## Skicka flera standarder i en begäran

SDK har även stöd för att skicka fler än ett medgivandeobjekt i en begäran.

```javascript
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
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Upprätthållande av medgivandeinställningar

När du har skickat användarinställningar till SDK med `setConsent` SDK-kommandot behåller användarens inställningar för en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar och använder SDK de beständiga inställningarna för att avgöra om händelser kan skickas till Adobe eller inte.

Du måste lagra användarinställningarna oberoende av varandra för att kunna visa dialogrutan för samtycke med de aktuella inställningarna. Det finns inget sätt att hämta användarinställningar från SDK:n. Om du vill vara säker på att användarinställningarna är synkroniserade med SDK:n kan du anropa `setConsent` på varje sida som läses in. SDK:n gör bara ett serveranrop om inställningarna har ändrats.

## Synkronisera identiteter när du ställer in samtycke

När standardmedgivandet väntar eller dras ut, `setConsent` kan vara den första begäran som skickas ut och fastställer identitet. På grund av detta kan det vara viktigt att synkronisera identiteter på den första begäran. Identitetskartan kan läggas till i `setConsent` på samma sätt som på `sendEvent` -kommando. Se [Hämtar Experience Cloud ID](../identity/overview.md)
