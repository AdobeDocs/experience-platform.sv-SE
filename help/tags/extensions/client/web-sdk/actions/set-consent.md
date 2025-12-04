---
title: Ange samtycke
description: Anger önskat samtycke för besökaren.
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Ange samtycke

Åtgärden **[!UICONTROL Set consent]** avgör om taggtillägget ska skicka data (anmälan), ta bort data (avanmälan) eller använda [standardmedgivande](../configure/consent.md) (samtycke okänt). När en användare tillåter eller nekar samtycke på din webbplats kan du använda den här åtgärden för att synkronisera deras inställningar med taggtillägget. JavaScript-biblioteksekvivalenten för den här åtgärden är kommandot [`setConsent`](/help/collection/js/commands/setconsent.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ sedan in [!UICONTROL Action type] på **[!UICONTROL Set consent]**.

Taggtillägget stöder följande standarder:

* **[Adobe-standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Både 1.0- och 2.0-standarder stöds.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Om du använder den här standarden uppdateras besökarens kundprofil i realtid med medgivandeinformationen om implementeringen är korrekt konfigurerad:
   1. Det enskilda XDM-profilschemat innehåller fältgruppen [IAB TCF 2.0-samtycke](/help/xdm/field-groups/profile/iab.md).
   1. Experience Event-schemat innehåller fältgruppen [IAB TCF 2.0-samtycke](/help/xdm/field-groups/event/iab.md).

Adobe rekommenderar att du lagrar eventuella inställningar för dialogrutan för samtycke separat, t.ex. i ett dataelement. Taggtillägget erbjuder inte ett sätt att få samtycke. Om du vill vara säker på att användarinställningarna är synkroniserade med taggtillägget kan du utföra den här åtgärden på varje sida som läses in.

## Tillgängliga fält

Den här åtgärdstypen stöder följande konfigurationsalternativ:

* **[!UICONTROL Instance]**: Den SDK-instans som åtgärden gäller för. Den här nedrullningsbara menyn är inaktiverad om implementeringen använder en enda SDK-instans.
* **[!UICONTROL Identity map]**: Ett dataelement som styr hur ett ECID genereras och vilka ID:n som godkännandeinformation är knuten till.
* **[!UICONTROL Consent information]**: Avgör om du vill fylla i ett formulär eller ange ett dataelement som innehåller information om samtycke.
* **[!UICONTROL Standard]**: Den standard för samtycke som du vill använda. De tillgängliga alternativen är [!UICONTROL Adobe] och [!UICONTROL IAB TCF].
* **[!UICONTROL Version]**: Den version av medgivandestandarden som du vill använda.
* **[!UICONTROL Datastream configuration overrides]**: Det här kommandot har stöd för åsidosättningar av dataströmskonfigurationer, vilket ger dig kontroll över vilka program och tjänster som tar emot dessa data. När du anger en åsidosättning av en datastream-konfiguration i både ett enskilt kommando och i inställningarna för taggtilläggskonfigurationen, prioriteras det enskilda kommandot. Mer information finns i [Åsidosättningar av dataströmskonfiguration](../configure/configuration-overrides.md).

## Skapa en regel som uppdaterar medgivandeinformation

Ett idealiskt tillfälle att använda den här åtgärden är när en kunds medgivandeinställningar har ändrats. Du kan skapa en taggregel som lyssnar efter den här ändringen.

1. Navigera till **[!UICONTROL Rules]** i en taggegenskap och välj **[!UICONTROL Add rule]**.
1. Ge regeln ett önskat namn och välj sedan ikonen `+` bredvid **[!UICONTROL Events]**.
1. Ange följande egenskaper till vänster:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. Öppna redigeraren till höger och använd följande kod som mall:

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

1. Välj **[!UICONTROL Keep changes]**.

Ovanstående anpassade kodblock gör två saker:

* Startar regeln när medgivandeinställningarna har ändrats.
* Anger två dataelement: **IAB TCF-medgivandesträng** och **IAB TCF-samtycke GDPR**.

Dessa dataelement är användbara när du ställer in åtgärden [!UICONTROL Set Consent]:

1. Välj ikonen `+` bredvid **[!UICONTROL Actions]**.
1. Ange följande egenskaper till vänster:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. Ange följande egenskaper till höger:
   * **[!UICONTROL Standard]**: [!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**: [!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**: [!UICONTROL Provide a data element], med värdet `%IAB TCF Consent GDPR%`

![IAB - ange medarbetaråtgärd](../assets/iab-action.png)

>[!NOTE]
>
>Du kan inte välja dessa dataelement med hjälp av dataelementväljaren eftersom de skapades med anpassad kod. Du måste ange ett procenttecken i dataelementnamnet.
