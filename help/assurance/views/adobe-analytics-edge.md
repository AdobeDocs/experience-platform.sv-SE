---
title: Analyshändelser 2.0 i Assurance
description: Den här guiden förklarar hur du använder Edge-vyn Adobe Analytics och Analytics med Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
exl-id: faaa2c1d-3471-4d86-9a25-03265b996e31
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Analyshändelser 2.0 i Assurance

Med Analytics Events 2.0 får du en bättre bild av SDK-händelser som användare kan felsöka och validera sin Adobe Analytics-implementering. I vyn visas händelser som skickats till Adobe Analytics från [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) samt [Adobe Experience Platform Edge Network SDK](https://developer.adobe.com/client-sdks/edge/edge-network/). Vyn innehåller även en informationspanel, som innehåller en kontext om hur händelsen bearbetades av klient-SDK samt av de överordnade tjänsterna efter att den lämnat enheten.

## Komma igång

Om du vill använda den här vyn utför du följande steg:

1. [Konfigurera Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Skapa och anslut till en Assurance-session](../tutorials/using-assurance.md).
3. Välj **Analyshändelser 2.0 (Beta)** i kontrollgränssnittet **Hem** till vänster. Om du inte ser det här alternativet väljer du **Konfigurera** längst ned till vänster i fönstret, lägger till **Analyshändelser 2.0 (Beta)** och väljer **Spara**.

## Vy för analyshändelser

Använd Analytics-händelseläget om du använder mobiltillägget **Adobe Analytics** . I den här vyn kan du enkelt visa Analytics-händelser som skickas från en ansluten klient, inklusive Track Action-, Track State- och Lifecycle-händelser. Genom att välja en av Analytics-händelserna i tabellen kan du visa information om hur händelsen bearbetades på den högra panelen.

![En bild som visar olika komponenter i vyn Analyshändelser.](./images/adobe-analytics-edge/analytics-events.png)

### Post-bearbetad status

När SDK har gjort en nätverksbegäran med Adobe Analytics får du veta om Assurance kunde hämta efterbearbetningsinformationen för Adobe Analytics-begäran. Vyn Analyshändelser måste förbli aktiv medan efterbearbetningsstatusen är aktiv efter att begäran har utlösts.

Observera att den inloggade användaren måste ha tillgång till motsvarande rapportserie för att kunna hämta efterbearbetningsinformation.

| Status | Beskrivning |
| :----- | :---------- |
| `Queued` | Nätverksbegäran hämtar efterbearbetningsinformationen. |
| `Processed` | Nätverksbegäran har slutförts och efterbearbetningsinformationen har tagits emot. |
| `Delayed` | Maximalt antal begäranden om hämtning av efterbearbetningsinformation har överskridits. |
| `Error` | Ett fel gjorde att nätverksbegäran misslyckades. Mer information om felet visas i vyn med händelseinformation. |
| `Unauthorized` | Användaren har inte åtkomst till Adobe Analytics rapportserie. |
| `Unavailable` | Adobe Analytics-begäran har ingen motsvarande `AnalyticsResponse`-händelse. |
| `No Debug Flag` | Den aktuella Adobe Analytics- eller Assurance SDK-versionen kanske inte har stöd för analysfelsökningsfunktionen. Mer information finns i [felsökningsguiden](../troubleshooting.md). |
| `Expired` | Händelsen `AnalyticsTrack` eller `LifecycleStart` är äldre än 24 timmar. |

### Vyn Händelseinformation

För en Analytics-spårningshändelse innehåller den detaljerade vyn följande delar:

- En SDK Analytics-begärandehändelse som har sitt ursprung.
- Metadata och kontextdata från begäran, till exempel rapportsviter-ID, SDK-tilläggsversioner och kontextdata.
- Post bearbetade information om Analytics-händelsen som innehåller mappningen av varv, evar och props.

### Analysvyvalidering

I valideringsvyn kan du enkelt visa resultaten för valideringsskript som hör till Analytics (Analyser). Fel som visas av validerare kan innehålla länkar till den plats där de ska korrigeras eller visa händelser som är i feltillstånd.

![En bild som visar fliken Validerare i analysvyn.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Analytics Edge view

Använd Analytics Edge-vyn om du använder mobiltilläggen **Edge Network** eller **Edge Bridge** . Om du vill aktivera den här vyn väljer du knappen Analytics Edge (Beta) längst upp till höger för att visa Analytics-händelser som skickas via Edge-nätverk i den aktuella sessionen. Detta omfattar alla händelser som har utlösts av Lifecycle-tillägget, Edge-förfrågningar och/eller Edge Bridge-händelser baserade på Track Action och Track State.

![En bild som visar vilka som används för att växla mellan Analytics-vyn och Analytics-vyn i Edge.](./images/adobe-analytics-edge/analytics-view-toggle.png)

Analytics-vyn i Edge innehåller information om Analytics-relaterade Edge-begäranden och Lifecycle-metoder som skickas av klienten. Genom att välja en händelse i listan, visar den högra panelen de händelser som har bearbetats av klient-SDK samt av den överordnade tjänsten efter att de har lämnat enheten, så att du enkelt kan se händelsekedjan som har uppstått efter ett anrop.

![En bild som visar olika komponenter i Analytics Edge View.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Analytics Edge Validation

Med valideringsvyn i Analytics Edge kan du enkelt visa resultaten för valideringsskript som hör till Analytics Edge. Fel som visas av validerare kan innehålla länkar till den plats där de ska korrigeras eller visa händelser som är i feltillstånd.

![En bild som visar fliken Validerare i vyn Analytics Edge.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
