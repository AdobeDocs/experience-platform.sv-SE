---
title: Testreferens för taggnärvaro
description: Lär dig hur granskaren testar taggnärvaro i Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 5%

---

# Testreferens för taggnärvaro

Den här referensen innehåller mer information om hur revisionsfunktionen i Adobe Experience Platform Debugger testar taggnärvaro.

>[!NOTE]
>
>Mer information om granskartester i Platform Debugger finns i [översikt över funktioner](./overview.md).

Taggnärvaro-tester utvärderar om vissa taggar finns på sidan och om de finns på rätt plats i sidkoden.

| Test | Bredd | Kriterier | Rekommendation |
| --- | --- | --- | --- |
| Advertising Cloud - kodnärvaro | 5 | Advertising Cloud-taggen är inte tillgänglig i DOM. | Implementera Advertising Cloud-taggen med [Advertising Cloud-taggtillägg](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - segmentpixel implementerad | 5 | Uppgradera dina Advertising Cloud-segmentpixlar till de nya Advertising Cloud-taggar som bara innehåller bilder. Om du använder de föråldrade AMO-segmenttaggarna kan data gå förlorade. | Implementera Advertising Cloud-segmentpixeln med [Advertising Cloud-taggtillägg](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analyser - läses in i DOM | 5 | Det gick inte att identifiera Adobe Analytics-taggen. | Installera den senaste versionen av Analytics. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Starta - Biblioteket har lästs in | 5 | A `global _satellite` det gick inte att hitta objektet i DOM, vilket innebär att taggbiblioteket inte är installerat eller inte kan köras. | Kontrollera att taggbiblioteket är implementerat på sidan och inte blockeras av efterföljande skriptaktiviteter. |
| Launch - Not have multiple embed scripts | 5 | Produktionsplatser ska bara läsa in en inbäddningskod per sida. | Kontrollera att det bara är produktionsbiblioteket som läses in på sidan. |
| Starta - `pageBottom` callback finns i `<body>` | 5 | Obligatoriskt `_satellite.pageBottom()` callback-funktionen hittades inte i `<body>` på sidan. Testet misslyckas om `pageBottom` anropet inte finns alls på sidan, eller om det finns på sidan `<head>` -tagg (eller någon annan oväntad plats). Det går bara om `pageBottom` finns någonstans i `<body>` -tagg. | Lägg till det infogade skriptet omedelbart före stängningen `</body>` för att säkerställa att taggarna fungerar som de ska.<br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Starta - `pageBottom` callback ska inte finnas när asynkront distribueras | 5 | The `_satellite.pageBottom()` återanrop hittades på sidan, vilket inte bör vara fallet när taggar distribueras asynkront. | Ta bort `_satellite.pageBottom()` för att aktivera rätt taggfunktioner. <br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID-tjänst - kodnärvaro | 5 | Det gick inte att hitta Experience Cloud ID-tjänstkoden. Vi rekommenderar att du använder Experience Cloud ID:n (ECID:n) för att få ut så mycket som möjligt av dina Experience Cloud-lösningar och är viktigt för ID-hantering i olika Experience Cloud-lösningar. | Installera den senaste versionen av ECID.<br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud ID-tjänst - cookie-närvaro | 5 | The `AMCV_` Det gick inte att hitta cookie. Du måste instansiera ett besökarobjekt från `VisitorAPI.js` kod. | Om det här är en taggimplementering kontrollerar du att AdobeOrg-ID:t är korrekt angivet i ECID-verktyget. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud ID-tjänst - MID-värde finns | 5 | MID-värdet hittades inte i `AMCV_` cookie. | Testa igen för att kontrollera om det finns någon ECID API-fördröjning. Kontakta Adobe kundtjänst om problemet kvarstår. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Mål - kod finns | 5 | Adobe Target ska definieras i DOM. | Installera den senaste versionen av Target (at.js). <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Mål - Biblioteket har lästs in i `<head>` | 4 | Målbiblioteket ska läsas in i `<head>` -tagg. | Kontrollera att målbiblioteket har lästs in i `<head>` -tagg. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
