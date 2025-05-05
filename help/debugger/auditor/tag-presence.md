---
title: Testreferens för taggnärvaro
description: Lär dig hur granskaren testar taggnärvaro i Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---

# Testreferens för taggnärvaro

Den här referensen innehåller mer information om hur revisionsfunktionen i Adobe Experience Platform Debugger testar taggnärvaro.

>[!NOTE]
>
>Mer information om granskartester i Experience Platform Debugger finns i [funktionsöversikten för granskare](./overview.md).

Taggnärvaro-tester utvärderar om vissa taggar finns på sidan och om de finns på rätt plats i sidkoden.

| Test | Bredd | Kriterier | Rekommendation |
| --- | --- | --- | --- |
| Advertising Cloud - kodnärvaro | 5 | Advertising Cloud-taggen är inte tillgänglig i DOM. | Implementera Advertising Cloud-taggen med [Advertising Cloud-taggtillägget](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - segmentpixel implementerad | 5 | Uppgradera era pixlar i Advertising Cloud-segmentet till de nya taggar som bara används i Advertising Cloud för bilder. Om du använder de föråldrade AMO-segmenttaggarna kan data gå förlorade. | Implementera segmentpixeln i Advertising Cloud med taggtillägget [Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analyser - läses in i DOM | 5 | Det gick inte att identifiera Adobe Analytics-taggen. | Installera den senaste versionen av Analytics. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=sv-SE) |
| Starta - Biblioteket har lästs in | 5 | Det gick inte att hitta ett `global _satellite`-objekt i DOM, vilket innebär att taggbiblioteket inte är installerat eller inte kan köras. | Kontrollera att taggbiblioteket är implementerat på sidan och inte blockeras av efterföljande skriptaktiviteter. |
| Launch - Not have multiple embed scripts | 5 | Produktionsplatser ska bara läsa in en inbäddningskod per sida. | Kontrollera att det bara är produktionsbiblioteket som läses in på sidan. |
| Starta - `pageBottom` återanrop finns i `<body>` | 5 | Det gick inte att hitta det begärda `_satellite.pageBottom()`-återanropet inom `<body>` på sidan. Testet misslyckas om anropet `pageBottom` inte hittas alls på sidan eller om det finns i taggen `<head>` (eller någon annan oväntad plats). Det skickas bara om `pageBottom` hittas någonstans i taggen `<body>`. | Lägg till det infogade skriptet omedelbart före den avslutande `</body>`-taggen för att säkerställa rätt taggfunktionalitet.<br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Starta - `pageBottom` återanrop ska inte finnas när den distribueras asynkront | 5 | Återanropet `_satellite.pageBottom()` hittades på sidan, vilket inte bör vara fallet när taggar distribueras asynkront. | Ta bort skriptet `_satellite.pageBottom()` om du vill aktivera rätt taggfunktioner. <br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID-tjänst - kodnärvaro | 5 | Det gick inte att hitta Experience Cloud ID-tjänstkoden. Vi rekommenderar att du använder Experience Cloud ID (ECID) för att få ut det mesta av dina Experience Cloud-lösningar och för att kunna hantera ID:n i Experience Cloud-lösningar. | Installera den senaste versionen av ECID.<br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=sv-SE) |
| Experience Cloud ID-tjänst - cookie-närvaro | 5 | Det gick inte att hitta cookien `AMCV_`. Du måste instansiera ett besökarobjekt från `VisitorAPI.js`-koden. | Om det här är en taggimplementering kontrollerar du att AdobeOrg-ID:t är korrekt angivet i ECID-verktyget. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=sv-SE) |
| Experience Cloud ID-tjänst - MID-värde finns | 5 | MID-värdet hittades inte i `AMCV_`-cookien. | Testa igen för att kontrollera om det finns någon ECID API-fördröjning. Kontakta Adobe kundtjänst om problemet kvarstår. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=sv-SE) |
| Mål - kod finns | 5 | Adobe Target ska definieras i DOM. | Installera den senaste versionen av Target (at.js). <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=sv-SE) |
| Mål - Biblioteket har lästs in i `<head>` | 4 | Målbiblioteket ska läsas in i taggen `<head>`. | Kontrollera att målbiblioteket har lästs in i taggen `<head>`. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=sv-SE) |

{style="table-layout:auto"}
