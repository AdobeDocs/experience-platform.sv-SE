---
title: Godkännande
seo-title: Stöd för Adobe Experience Platform Web SDK-medgivandeinställning
description: Lär dig hur du stöder medgivandeinställningar med Experience Platform Web SDK
seo-description: Lär dig hur du stöder medgivandeinställningar med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Stöd för samtycke

Om du vill respektera användarens sekretess kan du be om användarens samtycke innan du tillåter att SDK använder användarspecifika data för vissa syften. För närvarande tillåter SDK endast användare att välja mellan att inte göra det, men i framtiden hoppas Adobe kunna ge mer exakt kontroll över specifika syften.

Om användaren väljer alla syften får SDK utföra följande uppgifter:

* Skicka data till och från Adobe-servrar.
* Läs och skriv cookies eller webblagringsobjekt (förutom för att behålla användarens inställningar för deltagande).

Om användaren väljer bort alla syften utför SDK inte någon av dessa åtgärder.

## Konfigurerar samtycke

Som standard väljs användaren i alla syften. För att förhindra att SDK utför ovanstående uppgifter tills användaren väljer att delta skickar du SDK-konfigurationen enligt följande `"defaultConsent": { "general": "pending" }` :

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

När standardmedgivandet för det allmänna syftet har angetts till väntande, och du försöker köra kommandon som är beroende av användarens inställningar för deltagande (till exempel kommandot `event` ), kommer kommandot att ställas i kö i SDK. Dessa kommandon bearbetas inte förrän du har meddelat användarens inställningar för deltagande till SDK.

Nu kanske du föredrar att be användaren att välja någonstans i användargränssnittet. När användarens inställningar har samlats in kan du meddela SDK:n dessa inställningar.

## Kommunicera med medgivandeinställningar

Om användaren väljer att gå in kör du `setConsent` kommandot med `general` alternativet inställt på `in` följande:

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

Eftersom användaren nu har valt att gå in, kör SDK alla kommandon som tidigare placerats i kö. Framtida kommandon som är beroende av att användaren väljer att logga in kommer _inte_ att ställas i kö, utan i stället köras direkt.

Om användaren väljer att avanmäla sig kör du `setConsent` kommandot med `general` alternativet inställt på `out` följande:

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
>När en användare har avanmält sig kan du inte ange användarens samtycke i SDK `in`.

Eftersom användaren valde att avanmäla sig avvisas löften som returnerats från tidigare köade kommandon. Framtida kommandon som är beroende av att användaren väljer att logga in returnerar löften som avvisas på liknande sätt. Mer information om hur du hanterar eller inaktiverar fel finns i [Körningskommandon](executing-commands.md).

>[!NOTE]
>
>För närvarande stöder SDK bara `general` syftet. Även om vi planerar att bygga ut en mer robust uppsättning syften eller kategorier som kommer att motsvara de olika möjligheterna och produkterbjudandena för Adobe, är den nuvarande implementeringen en metod som helt eller inte alls kan användas.  Detta gäller endast JavaScript-biblioteken Adobe Experience Platform [!DNL Web SDK] och INTE andra Adobe.

## Upprätthållande av medgivandeinställningar

När du har skickat användarinställningar till SDK med hjälp av `setConsent` kommandot, behåller SDK användarens inställningar till en cookie. Nästa gång användaren läser in webbplatsen i webbläsaren hämtar och använder SDK de beständiga inställningarna. Du behöver inte köra `setConsent` kommandot igen, förutom att meddela en ändring i användarens inställningar som du kan göra när som helst.