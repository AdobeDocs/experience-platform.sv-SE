---
title: Supporting Customer Consent Preferences Using the Adobe Experience Platform Web SDK
description: Lär dig hur du stöder medgivandeinställningar med Adobe Experience Platform Web SDK.
keywords: medgivande;defaultConsent;default medgivande;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---


# Stöd för kundernas samtycke

Om du vill respektera användarens sekretess kan du be om användarens samtycke innan du tillåter att SDK använder användarspecifika data för vissa syften. För närvarande tillåter SDK endast användare att välja mellan att inte göra det, men i framtiden hoppas Adobe kunna ge mer exakt kontroll över specifika syften.

Om användaren väljer alla syften får SDK utföra följande uppgifter:

* Skicka data till och från Adobe-servrar.
* Läs och skriv cookies eller webblagringsobjekt (förutom för att behålla användarens inställningar för deltagande).

Om användaren väljer bort alla syften utför SDK inte någon av dessa åtgärder.

## Konfigurera samtycke

Som standard väljs användaren i alla syften. För att förhindra att SDK utför ovanstående uppgifter tills användaren väljer att delta skickar du `"defaultConsent": "pending"` under SDK-konfigurationen enligt följande:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

När standardmedgivandet för det allmänna syftet har angetts till väntande, och du försöker köra kommandon som är beroende av användarens inställningar för deltagande (till exempel kommandot `event`), kommer kommandot att ställas i kö i SDK. Dessa kommandon bearbetas inte förrän du har meddelat användarens inställningar för deltagande till SDK.

Nu kanske du föredrar att be användaren att välja någonstans i användargränssnittet. När användarens inställningar har samlats in kan du meddela SDK:n dessa inställningar.

## Kommunicera med samtyckespreferenser via Adobe-standarden

Om användaren väljer att gå in kör du kommandot `setConsent` med alternativet `general` inställt på `in` enligt följande:

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

Eftersom användaren nu har valt att gå in, kör SDK alla kommandon som tidigare placerats i kö. Framtida kommandon som är beroende av att användaren väljer att gå in kommer inte att ställas i kö och i stället köras direkt.

Om användaren väljer att avanmäla sig kör du kommandot `setConsent` med alternativet `general` inställt på `out` enligt följande:

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

>[!NOTE]
>
>När en användare har avanmält sig kan du inte ange användarens samtycke till `in`.

Eftersom användaren valde att avanmäla sig avvisas löften som returnerats från tidigare köade kommandon. Framtida kommandon som är beroende av att användaren väljer att logga in returnerar löften som avvisas på liknande sätt. Mer information om hur du hanterar eller inaktiverar fel finns i [Kör kommandon](../fundamentals/executing-commands.md).

>[!NOTE]
>
>För närvarande stöder SDK endast `general`-syftet. Även om vi planerar att bygga ut en mer robust uppsättning syften eller kategorier som kommer att motsvara de olika möjligheterna och produkterbjudandena för Adobe, är den nuvarande implementeringen en metod som helt eller inte alls kan användas.  Detta gäller endast Adobe Experience Platform [!DNL Web SDK] och INTE andra Adobe JavaScript-bibliotek.

## Kommunicera medgivandepreferenser via IAB TCF-standarden

SDK har stöd för inspelning av en användares medgivandepreferenser via IAB-standarden (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF). Medgivandesträngen kan anges med samma `setConsent`-kommando som ovan så här:

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

När medgivandet har ställts in på det här sättet uppdateras kundprofilen i realtid med medgivandeinformationen. För att detta ska fungera måste profilens XDM-schema innehålla [mixen för profilsekretess](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). När händelser skickas måste IAB:s medgivandeinformation läggas till manuellt i händelsens XDM-objekt. SDK inkluderar inte automatiskt information om samtycke i händelserna. Om du vill skicka medgivandeinformationen i händelser måste [Experience Event Privacy Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) läggas till i Experience Event-schemat.

## Skicka båda standarderna i en begäran

SDK har även stöd för att skicka fler än ett medgivandeobjekt i en begäran.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
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

När du har skickat användarinställningar till SDK med kommandot `setConsent` kvarstår användarens inställningar i SDK som en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar och använder SDK de beständiga inställningarna för att avgöra om händelser kan skickas till Adobe eller inte. Du behöver inte köra kommandot `setConsent` igen, förutom att meddela en ändring i användarens inställningar som du kan göra när som helst.

## Synkronisera identiteter när du ställer in samtycke

När standardmedgivandet är väntande kan `setConsent` vara den första begäran som skickas och upprättar identitet. På grund av detta kan det vara viktigt att synkronisera identiteter på den första begäran. Identitetskartan kan läggas till i kommandot `setConsent` precis som i kommandot `sendEvent`. Se [Hämta Experience Cloud ID](../identity/overview.md)

