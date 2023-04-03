---
title: Adobe Analytics View in Assurance
description: Den här guiden förklarar hur du använder Adobe Analytics med Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Adobe Analytics-vy i Assurance

Integreringen av Adobe Experience Platform Assurance med Adobe Analytics ger en mer detaljerad bild av SDK-händelser som användare kan felsöka och validera sin Adobe Analytics-implementering. Vyn visar nu livscykeln och händelse-/tillståndshändelser som skickats till Adobe Analytics från [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). Vyn innehåller även information om svar som ger information om hur händelserna bearbetades efter att de olika rapportsvitens bearbetningsregler har tillämpats.

![](./images/adobe-analytics/overview.png)

## Komma igång

Kontrollera att du har följande tjänster innan du fortsätter:

- The [Adobe Experience Platform Data Collection UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Läs mer om hur du installerar Assurance i programmet i [implementera Assurance-guide](../tutorials/implement-assurance.md).

## Efterbearbetad status

När SDK har gjort en nätverksbegäran med Adobe Analytics får du veta om Assurance kunde hämta efterbearbetningsinformationen för Adobe Analytics-begäran.

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

## Vyn Händelseinformation

För en Analytics-spårningshändelse innehåller den detaljerade vyn följande värdefulla delar:

- En SDK Analytics-begärandehändelse som har sitt ursprung.
- OOTB-metadata och kontextdata från begäran, till exempel rapportsviter-ID, SDK-tilläggsversioner, OOTB-kontextdata osv.
- Efterbearbetad information om Analytics-händelsen som innehåller mappningen av varv, varv, props o.s.v.
