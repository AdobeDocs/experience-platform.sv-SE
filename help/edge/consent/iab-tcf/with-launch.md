---
title: Integrera stödet för IAB TCF 2.0 med hjälp av taggar och Platform Web SDK Extension
description: Lär dig hur du ställer in IAB TCF 2.0-godkännande med taggar och Adobe Experience Platform Web SDK-tillägget.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---

# Integrera stödet för IAB TCF 2.0 med hjälp av taggar och Platform Web SDK-tillägget

Adobe Experience Platform Web SDK stöder Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). I den här handboken visas hur du ställer in en taggegenskap för att skicka IAB TCF 2.0-medgivandeinformation till Adobe med hjälp av taggtillägget Adobe Experience Platform Web SDK.

Om du inte vill använda taggar, se guiden på [med IAB TCF 2.0 utan taggar](./without-launch.md).

## Komma igång

Om du vill använda IAB TCF 2.0 med taggar och Platform Web SDK-tillägget måste du ha ett XDM-schema och en XDM-datauppsättning tillgänglig.

Den här guiden kräver dessutom att du har en fungerande förståelse för Adobe Experience Platform Web SDK. Läs mer i [Adobe Experience Platform Web SDK - översikt](../../home.md) och [Frågor och svar](../../web-sdk-faq.md) dokumentation.

## Ange standardsamtycke

I tilläggskonfigurationen finns en inställning för standardsamtycke. Detta styr beteendet för kunder som inte har någon cookie för samtycke. Om du vill placera Experience Events i kö för kunder som inte har någon cookie för samtycke ska du ange det här till `pending`. Om du vill ignorera Experience Events för kunder som inte har någon cookie för samtycke anger du det här till `out`. Du kan också använda ett dataelement för att dynamiskt ange standardvärdet för samtycke.

Mer information om hur du konfigurerar standardsamtycke finns i [standardsektion för samtycke](../../fundamentals/configuring-the-sdk.md#default-consent) i SDK-konfigurationsguiden.

## Uppdatera profil med medgivandeinformation {#consent-code-1}

För att ringa `setConsent` när dina kunders medgivandeinställningar har ändrats måste du skapa en ny taggregel. Börja med att lägga till en ny händelse och välj händelsetypen för Core-tillägget&quot;Custom Code&quot;.

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

* Anger två dataelement, ett med strängen för samtycke och ett med `gdprApplies` flagga. Detta är användbart senare när du fyller i åtgärden Ange samtycke.

* Startar regeln när medgivandeinställningarna har ändrats. Åtgärden Ange samtycke ska användas när medgivandeinställningarna har ändrats. Lägg till en&quot;Ange samtycke&quot;-åtgärd i tillägget och fyll i formuläret enligt följande:

* Standard: &quot;IAB TCF&quot;
* Version: &quot;2.0&quot;
* Värde: &quot;%IAB TCF Consent String%&quot;
* GDPR gäller: &quot;%IAB TCF Consent GDPR%&quot;

![IAB - ange medarbetaråtgärd](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Du kan inte välja dessa dataelement med hjälp av dataelementväljaren eftersom de skapades med anpassad kod. Du måste ange ett procenttecken i dataelementnamnet. Den här koden uppdaterar kundens profil med de nya medgivandeinställningarna så snart de ändras. Dessutom returnerar servern ett cookie-värde som kan förhindra att Adobe Experience Platform Web SDK spelar in Experience Events.

## Skapa ett XDM-dataelement för Experience Events

Medgivandesträngen ska inkluderas i XDM Experience Event. Använd XDM-objektets dataelement för att göra detta. Börja med att skapa ett nytt XDM-objektdataelement, eller använd ett som du redan har skapat för att skicka händelser. Om du har lagt till fältgruppen Experience Event Privacy i ditt schema bör du ha en `consentStrings` i XDM-objektet.

1. Välj **[!UICONTROL consentStrings]**.

1. Välj **[!UICONTROL Provide individual items]** och markera **[!UICONTROL Add Item]**.

1. Expandera **[!UICONTROL consentString]** rubrik och expandera det första objektet och fyll sedan i följande värden:

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

Den här koden är identisk med den tidigare anpassade koden, förutom att både `useractioncomplete` och `tcloaded` -händelser hanteras. The [föregående egen kod](#consent-code-1) aktiveras bara när kunden väljer sina inställningar för första gången. Den här koden utlöses också när kunden redan har valt sina inställningar. På den andra sidan laddas till exempel.

Lägg till en&quot;Skicka händelse&quot;-åtgärd från plattformens SDK-tillägg. I XDM-fältet väljer du XDM-dataelementet som du skapade i föregående avsnitt.

## Skicka andra händelser med IAB TCF 2.0-medgivandeinformation

När händelser utlöses efter den första Experience Event-händelsen definieras de två dataelementen fortfarande och kan användas för att skicka IAB:s medgivandeinformation. Använd samma XDM-dataelement för att skicka framtida händelser. Information om IAB TCF 2.0 ingår.

## Nästa steg

Nu när du har lärt dig att använda IAB TCF 2.0 med Platform Web SDK-tillägget kan du även integrera med andra Adobe-lösningar som Adobe Analytics eller kunddataplattformen i realtid. Se [Översikt över IAB Transparency &amp; Consent Framework 2.0](./overview.md) för mer information.
