---
title: Översikt över användningsfall i Personalization
description: Lär dig implementera användningsexempel för personalisering med Adobe Experience Platform Web SDK, inklusive mönster för återgivning av innehåll och spårning av displayannonser.
keywords: personalisering;sendEvent;renderDecision;applyPropositions;DecisionScopes;display events;flimmer;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Översikt över användningsfall i Personalization

Adobe Experience Platform Web SDK har ett stort antal användningsområden för webbsidor. Den har stöd för flexibla arkitekturer (klient, server och hybridteknik) så att du kan begära beslut och återge innehåll på ett sätt som passar behoven på platsen.

## Återge personaliserat innehåll

SDK på webben kan hämta personaliseringsbeslut (kallas även _propositioner_) och hjälpa dig att återge dem på sidan. Återgivning är asynkront, så undvik att anta en viss tidpunkt för när innehåll används.

Välj det mönster som matchar de förslagsobjekt du får:

1. **Återge automatiskt DOM-åtgärdsförslag**: Använd när dispositioner innehåller `dom-action` objekt med väljare och åtgärdstyper som kan användas automatiskt i Web SDK. Se [Återge automatiskt förslag på DOM-åtgärder](render-auto-pers-content.md).
1. **Återge HTML erbjuder utan väljare med applyPropositions**: Använd när du tar emot HTML-innehåll, men du måste ange var och hur det ska användas (väljare + åtgärdstyp) via metadata. Se [Återge HTML-erbjudanden utan väljare](render-html-offers.md).
1. **Återge utkast manuellt**: Använd när du behöver fullständig kontroll över återgivningslogiken (till exempel disposition av användargränssnitt från JSON eller tillämpning av anpassade affärsregler). Se [Återge utkast manuellt](render-manual-propositions.md).

>[!TIP]
>
>Dessa mönster kan kombineras. Du kan till exempel aktivera automatisk DOM-åtgärdsåtergivning samtidigt som du manuellt återger innehåll från specifika beslutsomfattningar.

## Vanliga kompletterande ämnen

De flesta personaliseringsimplementeringar omfattar följande vanliga ämnen:

* **Förhindra flimmer** (valfritt): Dölj och visa behållare under personalisering. Se [Hantera flimmer](manage-flicker.md).
* **Spåra vad som visades**: Spela in visningshändelser för återgivet innehåll. Se [Hantera visningshändelser](display-events.md).
* **Hämtning överst på sidan/mätvärden underst på sidan**: Begär beslut tidigt och ta sedan med mätningen. Se [Konfigurera sidans övre och nedre del](top-bottom-page-events.md).

## SDK-exempel

Förutom dokumentsidorna i den här mappen har Adobe en databas med exempelprogram som du kan referera till. Se [Web SDK-exempel](https://github.com/adobe/alloy-samples/) på GitHub för ytterligare personaliseringsscenarier, bland annat:

* Personalisering på klientsidan
* Personalisering på serversidan
* Hybrid-personalisering
* Personalization i ensidiga program
