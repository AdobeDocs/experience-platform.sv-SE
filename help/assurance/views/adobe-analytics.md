---
title: Adobe Analytics View in Assurance
description: Den här guiden förklarar hur du använder Adobe Analytics med Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Adobe Analytics-vy i Assurance

Integreringen av Adobe Experience Platform Assurance med Adobe Analytics ger en mer detaljerad bild av SDK-händelser som användare kan felsöka och validera sin Adobe Analytics-implementering. I vyn visas nu livscykel och händelse-/tillståndshändelser som skickats till Adobe Analytics från [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). Vyn innehåller även information om svar som ger information om hur händelserna bearbetades efter att de olika rapportsvitens bearbetningsregler har tillämpats.

![](./images/adobe-analytics/overview.png)

## Komma igång

Kontrollera att du har följande tjänster innan du fortsätter:

- Användargränssnittet för [Adobe Experience Platform-datainsamling](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Läs [implementeringsguiden](../tutorials/implement-assurance.md) om du vill lära dig hur du installerar Assurance i ditt program.

## Post-bearbetad status

När SDK har gjort en nätverksbegäran med Adobe Analytics får du veta om Assurance kunde hämta efterbearbetningsinformationen för Adobe Analytics-begäran.

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

## Vyn Händelseinformation

För en Analytics-spårningshändelse innehåller den detaljerade vyn följande värdefulla delar:

- En SDK Analytics-begärandehändelse som har sitt ursprung.
- OOTB-metadata och kontextdata från begäran, till exempel rapportsviter-ID, SDK-tilläggsversioner, OOTB-kontextdata osv.
- Post bearbetade information om Analytics-händelsen som innehåller mappningen av varv, varv, props och så vidare.
