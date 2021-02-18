---
title: Integrera stödet för IAB TCF 2.0 med hjälp av Platform Launch och Platform Web SDK Extension
description: Lär dig hur du ställer in godkännande för IAB TCF 2.0 med Adobe Experience Platform Launch och tillägget Adobe Experience Platform Web SDK.
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---


# Integrera stödet för IAB TCF 2.0 med hjälp av Platform Launch och Platform Web SDK-tillägget

Adobe Experience Platform Web SDK stöder Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). Den här guiden visar hur du ställer in en Adobe Experience Platform Launch-egenskap för att skicka IAB TCF 2.0-medgivandeinformation till Adobe med hjälp av AEP Web SDK-tillägget för Experience Platform Launch.

Om du inte vill använda Experience Platform Launch, se guiden [med IAB TCF 2.0 utan Experience Platform Launch](./without-launch.md).

## Komma igång

Om du vill använda IAB TCF 2.0 med Experience Platform Launch och AEP Web SDK-tillägget måste du ha ett XDM-schema och en datauppsättning tillgänglig.

Den här guiden kräver dessutom att du har en fungerande förståelse för Adobe Experience Platform Web SDK. Läs översikten [Adobe Experience Platform Web SDK](../../home.md) och dokumentationen [Vanliga frågor](../../web-sdk-faq.md) om du vill få en snabb uppdatering.

## Ange standardsamtycke

I tilläggskonfigurationen finns en inställning för standardsamtycke. Detta styr beteendet för kunder som inte har någon cookie för samtycke. Om du vill placera Experience Events i kö för kunder som inte har någon cookie för samtycke anger du `pending`.

>[!NOTE]
>
>För närvarande går det inte att ställa in detta dynamiskt via tillägget Experience Platform Launch.

Mer information om standardsamtycke finns i [standardavsnittet för samtycke](../../fundamentals/configuring-the-sdk.md#default-consent) i SDK-konfigurationsdokumentationen.

## Uppdaterar profil med medgivandeinformation {#consent-code-1}

Om du vill anropa åtgärden `setConsent` när dina kunders medgivandeinställningar har ändrats måste du skapa en ny Experience Platform Launch-regel. Börja med att lägga till en ny händelse och välj händelsetypen för Core-tillägget&quot;Custom Code&quot;.

Använd följande kodexempel för den nya händelsen:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Den här anpassade koden gör två saker:

* Ställer in två dataelement, ett med medgivandesträngen och ett med flaggan `gdprApplies`. Detta är användbart senare när du fyller i åtgärden Ange samtycke.

* Startar regeln när medgivandeinställningarna har ändrats. Åtgärden Ange samtycke ska användas när medgivandeinställningarna har ändrats. Lägg till en&quot;Ange samtycke&quot;-åtgärd i tillägget och fyll i formuläret enligt följande:

* Standard: &quot;IAB TCF&quot;
* Version: &quot;2.0&quot;
* Värde: &quot;%IAB TCF Consent String%&quot;
* GDPR gäller: &quot;%IAB TCF Consent GDPR%&quot;

![IAB - ange medarbetaråtgärd](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>Du kan inte välja dessa dataelement med hjälp av dataelementväljaren eftersom de skapades med anpassad kod. Du måste ange ett procenttecken i dataelementnamnet. Den här koden uppdaterar kundens profil med de nya medgivandeinställningarna så snart de ändras. Dessutom returnerar servern ett cookie-värde som kan förhindra att Adobe Experience Platform Web SDK spelar in Experience Events.

## Skapa ett XDM-dataelement för Experience Events

Medgivandesträngen ska inkluderas i XDM Experience Event. Använd XDM-objektets dataelement för att göra detta. Börja med att skapa ett nytt XDM-objektdataelement, eller använd ett som du redan har skapat för att skicka händelser. Om du har lagt till mixen Experience Event Privacy i ditt schema bör du ha en `consentStrings`-nyckel i XDM-objektet.

1. Välj **[!UICONTROL consentStrings]**.

1. Välj **[!UICONTROL Provide individual items]** och välj **[!UICONTROL Add Item]**.

1. Expandera rubriken **[!UICONTROL consentString]** och expandera det första objektet och fyll sedan i följande värden:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %IAB TCF Consent String%
* `gdprApplies`: %IAB TCF-medgivande GDPR%

>[!IMPORTANT]
>
>Du kan inte välja dessa dataelement med hjälp av dataelementväljaren eftersom de skapades med anpassad kod. Du måste ange ett procenttecken i dataelementnamnet.

## Skicka en inledande Experience Event med IAB TCF 2.0-medgivandeinformation

Om den inledande Experience Event-händelsen på sidan utlöses med en sidinläsningshändelse, har medgivandesträngen kanske inte lästs in ännu. Den här regeln är avsedd att ersätta den aktuella sidans inläsningshändelse. Om du vill vara säker på att godkännandeinformationen först läses in skapar du en ny regel och lägger till följande kod som en anpassad kodhändelse:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Den här koden är identisk med den tidigare anpassade koden förutom att både `useractioncomplete`- och `tcloaded`-händelser hanteras. Den [tidigare anpassade koden](#consent-code-1) aktiveras bara när kunden väljer sina inställningar för första gången. Den här koden utlöses också när kunden redan har valt sina inställningar. På den andra sidan laddas till exempel.

Lägg till en&quot;Skicka händelse&quot;-åtgärd från AEP Web SDK-tillägget. I XDM-fältet väljer du XDM-dataelementet som du skapade i föregående avsnitt.

## Skicka andra händelser med IAB TCF 2.0-medgivandeinformation

När händelser utlöses efter den första Experience Event-händelsen definieras de två dataelementen fortfarande och kan användas för att skicka IAB:s medgivandeinformation. Använd samma XDM-dataelement för att skicka framtida händelser. Information om IAB TCF 2.0 ingår.

## Nästa steg

Nu när du har lärt dig att använda IAB TCF 2.0 med AEP Web SDK-tillägget kan du även integrera med andra Adobe-lösningar som Adobe Analytics eller kunddataplattformen i realtid. Mer information finns i översikten [IAB Transparency &amp; Consent Framework 2.0](./overview.md).
