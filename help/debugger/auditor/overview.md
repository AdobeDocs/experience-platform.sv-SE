---
title: Fliken Granskare
description: Lär dig hur du använder fliken Granskare i Adobe Experience Platform Debugger för att testa dina Adobe Experience Cloud-implementeringar.
keywords: felsökare;felsökningstillägg för upplevelseplattform;krom;tillägg;revisor;dtm;target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 10%

---

# Fliken Granskare

I Adobe Experience Platform Debugger kan du använda fliken **[!UICONTROL Auditor]** för att köra en serie granskningstester på din sida.

Så här använder du funktionen:

1. Välj **[!UICONTROL Auditor]** i den vänstra navigeringen.
1. Välj **[!UICONTROL Run Auditor Tests]**.  När testerna är klara visas resultaten nedan.

![Skärmbild av testresultat på fliken Granskare](../images/auditor-results.png)

I resultatlistan visas testet och dess resultat, och förslag på hur du kan lösa eventuella problem.

## Tolka testresultat

Varje test viktas och din testpoäng är lika med den tilldelade vikten. Om du har klarat ett test med en vikt på 5 får du fem poäng.

| Poäng | Beskrivning |
| --- | --- |
| 0 | Aviserar dig om problem som du bör vara medveten om, men som inte påverkar ditt resultat. |
| 1 | Rekommenderar en optimering. Ingen påverkan på datakvaliteten. |
| 2 | Om du inte gör det här testet får du inte tillgång till de senaste funktionerna och korrigeringarna i Adobe Experience Cloud. |
| 3 | Testar effektiviteten och huruvida implementeringen följer bästa praxis. |
| 4 | Misslyckandet innebär att ni kanske samlar in otillförlitliga data. |
| 5 | Fel innebär att du kan se dataförlust. |

Alla tester antingen godkänns eller misslyckas. De kontrollerar om testvillkoren är uppfyllda eller inte, så det finns inga partiella poängvärden för partiell överensstämmelse. Om testet till exempel söker efter den senaste versionen av en Adobe-lösning och du bara är en version efter, får du samma resultat som om du är fem versioner tillbaka. De senaste versionerna innehåller prestandaförbättringar och felkorrigeringar, så vi rekommenderar att du använder den senaste versionen.

Vi **rekommenderar** att du korrigerar alla resultat för nivå 4 till 5.

Vi **rekommenderar** att du korrigerar alla resultat för nivå 1 till 3.

## Adobe-tekniker som stöds

Revisorfunktionen kan betygsätta följande Adobe-tekniker:

* Adobe Advertising Cloud DSP
* Adobe Advertising Cloud Search
* Adobe Analytics
* Adobe Experience Cloud Identity Service
* Adobe Target
* Taggar (tidigare Adobe Experience Platform Launch)

## Testa streck

Mer information om testrubrikerna i den här funktionen finns i följande dokument:

* [Konsekvens för taggar](./tag-consistency.md)
* [Tagg presence](./tag-presence.md)
* [Konfiguration](./configuration.md)
* [Larm](./alerts.md)
