---
title: Referens för aviseringstest
description: Lär dig hur granskaren testar varningar i Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# Referens för aviseringstest

Här finns mer information om hur revisionsfunktionen i Adobe Experience Platform Debugger kör varningstester.

>[!NOTE]
>
>Mer information om granskartester i Experience Platform Debugger finns i [funktionsöversikten för granskare](./overview.md).

Varningar visar problem som du bör vara medveten om, men som inte påverkar ditt poängtal. Det här är rekommendationer om god praxis som i vissa fall kanske inte gäller din implementering.

| Test | Bredd | Kriterier | Rekommendation |
| --- | --- | --- | --- |
| Advertising Cloud - Korrigera konverteringstagg implementerad | 0 | Kontrollera om rätt konverteringstagg används.<br><br>**Varning**: Om du använder de föråldrade konverteringstaggarna för TubeMogul kan data gå förlorade. | Uppgradera dina konverteringspixlar till de nya konverteringstaggarna för endast Advertising Cloud-bilder. Det är enklast att göra detta med taggtillägget [Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Korrigera JS-tagg som används | 0 | Advertising Cloud bör använda de senaste JavaScript-taggarna. | Uppgradera din Advertising Cloud JavaScript till den senaste versionen. Om du använder de föråldrade JavaScript-versionerna kan du förlora funktionalitet. Detta kan göras enklare med [Advertising Cloud-taggtillägget](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Tagg för endast bilder | 0 | Advertising Cloud-bildens pixelformat bör matcha något av följande rekommenderade format: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Uppgradera dina Advertising Cloud-pixlar till de nya Advertising Cloud-taggarna som säkerställer att du drar nytta av den fullständiga funktionen i Advertising Cloud. Det är enklast att göra detta med taggtillägget [Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Segmentera pixlar DSP Syncing Enabled | 0 | Kontrollera om TubeMogul-segmentpixeln innehåller en DSP Syncing-inställning och rekommendera att inställningen läggs till i pixeln. Inställningen för DSP Syncing bestäms av användningen av en frågesträngsparameter. Sammanfattning: <ul><li>OM taggen aktiveras för något av följande:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>OCH taggen innehåller URL-parametern `sid=`</li><li>Kontrollera sedan om URL-parametern `cs=0` eller `cs=1` finns och om inte `cs=1` bör läggas till i pixlarna så att målgruppens matchningsfrekvens kan förbättras.</li></ul> | Lägg till URL-parametern `cs=1` i dina Advertising Cloud-pixlar så att DSP Syncing kan utföras, vilket ökar målgruppsmatchningen. Det är enklast att göra detta med taggtillägget [Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID-tjänst - använd endast en AdobeOrg | 0 | Vid en normal ECID-implementering ska en enda AdobeOrg användas. | Verifiera att det finns flera AdobeOrg ID:n för den här implementeringen. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html?lang=sv-SE) |
| Starta - `pageBottom` återanropsplacering | 0 | Funktionen `_satellite.pageBottom()` måste finnas för att taggar ska fungera. Lägg till det infogade skriptet omedelbart före den avslutande `</body>`-taggen för att säkerställa korrekt DTM-funktionalitet. Obs! Det är bäst att använda taggen som sista tagg i `<body>`. Om det hittas i taggen `<body>` kan det fungera, men eftersom det inte är en bra metod kan det fungera felaktigt eller med oväntade eller oönskade resultat. | Lägg till det infogade skriptet omedelbart före den avslutande `</body>`-taggen för att säkerställa korrekt DTM-funktionalitet. <br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - Self-Hosted | 0 | Taggbiblioteket finns på Adobe Akamai-instansen på `assets.adobedtm.com`. Självvärdande är det rekommenderade sättet att läsa in taggar eftersom det ger bättre kontroll över webbplatsens prestanda genom cachekontroll, minskar beroenden av skript från tredje part och ger större kontroll över publiceringsprocessen. Taggbibliotek kan hanteras via din egen webbhosting eller CDN. | Byt till en värdtjänst är ett sätt att läsa in taggar på en sida. Även om värdtjänster via Akamai CDN fungerar i de flesta fall förbättras sidprestanda av självvärdande tjänster. <br><br>Ytterligare information:<ul><li>[Snabbstartsguide för taggar](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Asynkron distribution](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - ska distribueras asynkront | 0 | Taggar ska distribueras asynkront för optimala prestanda. | Inkludera parametern `async` i det infogade skriptet för att säkerställa rätt taggfunktionalitet <br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Mål - Innehåll i `mboxDefault` | 0 | Innehållet ska finnas i `mboxDefault` när `at.js` används. | Kontrollera att innehållet är tillgängligt. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=sv-SE) |

{style="table-layout:auto"}
