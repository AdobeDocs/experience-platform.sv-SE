---
title: Analyshändelser 2.0 i Assurance
description: Den här guiden förklarar hur du använder Adobe Analytics- och Analytics Edge-vyn med Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
source-git-commit: f707554ea89731fbd3f013d6065fde27ba7fa811
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Analyshändelser 2.0 i Assurance

Med Analytics Events 2.0 får du en bättre bild av SDK-händelser som användare kan felsöka och validera sin Adobe Analytics-implementering. Vyn visar händelser som skickats till Adobe Analytics från [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) och [Adobe Experience Platform Edge Network SDK](https://developer.adobe.com/client-sdks/edge/edge-network/). Vyn innehåller även en informationspanel, som innehåller en kontext om hur händelsen bearbetades av klient-SDK samt av de överordnade tjänsterna efter att den lämnat enheten.

## Komma igång

Om du vill använda den här vyn utför du följande steg:

1. [Konfigurera Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Skapa och ansluta till en Assurance-session](../tutorials/using-assurance.md).
3. I Assurance-gränssnittet från vänster navigering **Startsida** visa-menyn, välja **Analyshändelser 2.0 (beta)**. Om du inte ser det här alternativet väljer du **Konfigurera** i fönstrets nedre vänstra hörn lägger du till **Analyshändelser 2.0 (beta)** och markera **Spara**.

## Vy för analyshändelser

Använd händelsevyn i Analytics om du använder **Adobe Analytics** mobiltillägg. I den här vyn kan du enkelt visa Analytics-händelser som skickas från en ansluten klient, inklusive Track Action-, Track State- och Lifecycle-händelser. Genom att välja en av Analytics-händelserna i tabellen kan du visa information om hur händelsen bearbetades på den högra panelen.

![En bild som visar olika komponenter i händelsevyn i Analytics.](./images/adobe-analytics-edge/analytics-events.png)

### Efterbearbetad status

När SDK har gjort en nätverksbegäran med Adobe Analytics får du veta om Assurance kunde hämta efterbearbetningsinformationen för Adobe Analytics-begäran. Vyn Analyshändelser måste förbli aktiv medan efterbearbetningsstatusen är aktiv efter att begäran har utlösts.

Observera att den inloggade användaren måste ha tillgång till motsvarande rapportserie för att kunna hämta efterbearbetningsinformation.

| Status | Beskrivning |
| :----- | :---------- |
| `Queued` | Nätverksbegäran hämtar efterbearbetningsinformationen. |
| `Processed` | Nätverksbegäran har slutförts och efterbearbetningsinformationen har tagits emot. |
| `Delayed` | Maximalt antal begäranden om hämtning av efterbearbetningsinformation har överskridits. |
| `Error` | Ett fel gjorde att nätverksbegäran misslyckades. Mer information om felet visas i vyn med händelseinformation. |
| `Unauthorized` | Användaren har inte åtkomst till Adobe Analytics rapportserie. |
| `Unavailable` | Adobe Analytics-begäran saknar motsvarande `AnalyticsResponse` -händelse. |
| `No Debug Flag` | Den aktuella Adobe Analytics- eller Assurance SDK-versionen kanske inte har stöd för analysfelsökningsfunktionen. Mer information finns i [Felsökningsguide](../troubleshooting.md). |
| `Expired` | The `AnalyticsTrack` eller `LifecycleStart` händelsen är äldre än 24 timmar. |

### Vyn Händelseinformation

För en Analytics-spårningshändelse innehåller den detaljerade vyn följande delar:

- En SDK Analytics-begärandehändelse som har sitt ursprung.
- Metadata och kontextdata från begäran, till exempel rapportsviter-ID, SDK-tilläggsversioner och kontextdata.
- Efterbearbetad information om Analytics-händelsen som innehåller mappningen av varv, evar och props.

### Analysvyvalidering

I valideringsvyn kan du enkelt visa resultaten för valideringsskript som hör till Analytics (Analyser). Fel som visas av validerare kan innehålla länkar till den plats där de ska korrigeras eller visa händelser som är i feltillstånd.

![En bild som visar fliken Validerare i analysvyn.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Analyskantvyn

Använd Analytics Edge-vyn om du använder **Edge Network** eller **Edge Bridge** mobiltillägg. Om du vill aktivera den här vyn väljer du knappen&quot;Analytics Edge (Beta)&quot; längst upp till höger för att visa de Analytics-händelser som skickas via Edge-nätverket i den aktuella sessionen. Detta omfattar alla händelser som har utlösts av Lifecycle-tillägget, Edge-begäranden och/eller Edge Bridge-händelser baserade på Track Action och Track State.

![En bild som visar vilka som används för att växla mellan Analytics View och Analytics Edge View.](./images/adobe-analytics-edge/analytics-view-toggle.png)

Edge-vyn i Analytics innehåller information om Analytics-relaterade Edge-begäranden och Lifecycle-metoder som skickas av klienten. Genom att välja en händelse i listan, visar den högra panelen de händelser som har bearbetats av klient-SDK samt av den överordnade tjänsten efter att de har lämnat enheten, så att du enkelt kan se händelsekedjan som har uppstått efter ett anrop.

![En bild som visar olika komponenter i Analytics Edge View.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Kantvalidering av Analytics

I valideringsvyn för Analytics Edge kan du enkelt visa resultaten för valideringsskript som hör till Analytics Edge. Fel som visas av validerare kan innehålla länkar till den plats där de ska korrigeras eller visa händelser som är i feltillstånd.

![En bild som visar fliken Validerare i Analytics Edge-vyn.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
