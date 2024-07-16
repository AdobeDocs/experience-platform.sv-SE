---
title: Referens för aviseringstest
description: Lär dig hur granskaren testar varningar i Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# Referens för aviseringstest

Denna referens innehåller mer information om hur revisionsfunktionen i Adobe Experience Platform Debugger utför varningstester.

>[!NOTE]
>
>Mer information om granskartester i Platform Debugger finns i [översikten över funktionen ](./overview.md) hos revisorn.

Varningar visar problem som du bör vara medveten om, men som inte påverkar ditt poängtal. Det här är rekommendationer om god praxis som i vissa fall kanske inte gäller din implementering.

| Test | Bredd | Kriterier | Rekommendation |
| --- | --- | --- | --- |
| Advertising Cloud - Korrigera konverteringstagg har implementerats | 0 | Kontrollera om rätt konverteringstagg används.<br><br>**Varning**: Om du använder de föråldrade konverteringstaggarna för TubeMogul kan data gå förlorade. | Uppgradera dina konverteringspixlar till de nya konverteringstaggarna för Advertising Cloud-bilder. Det är enklast att göra detta med [Advertising Cloud-taggtillägget](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - korrigera JS-tagg som används | 0 | Advertising Cloud bör använda de senaste JavaScript-taggarna. | Uppgradera din Advertising Cloud JavaScript till den senaste versionen. Om du använder de föråldrade JavaScript-versionerna kan du förlora funktionalitet. Detta kan göras enklare med [Advertising Cloud-taggtillägget](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Tagg för endast bild | 0 | Advertising Cloud bildpixelformat bör matcha något av följande rekommenderade format: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Uppgradera dina Advertising Cloud-pixlar till de nya Advertising Cloud-taggar som säkerställer att du utnyttjar alla funktioner i Advertising Cloud. Det är enklast att göra detta med [Advertising Cloud-taggtillägget](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Synkronisering av pixlar DSP segment aktiverat | 0 | Kontrollera om TubeMogul-segmentpixeln innehåller en DSP synkroniseringsinställning och rekommendera att inställningen läggs till i pixeln. Inställningen DSP synkronisering bestäms av användningen av en frågesträngsparameter. Sammanfattning: <ul><li>OM taggen aktiveras för något av följande:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>OCH taggen innehåller URL-parametern `sid=`</li><li>Kontrollera sedan om URL-parametern `cs=0` eller `cs=1` finns och om inte `cs=1` bör läggas till i pixlarna så att målgruppens matchningsfrekvens kan förbättras.</li></ul> | Lägg till URL-parametern `cs=1` i dina Advertising Cloud-pixlar så att DSP kan synkroniseras, vilket ökar målgruppens matchningsfrekvens. Det är enklast att göra detta med [Advertising Cloud-taggtillägget](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID-tjänst - använd endast en AdobeOrg | 0 | Vid en normal ECID-implementering ska en enda AdobeOrg användas. | Verifiera att det finns flera AdobeOrg ID:n för den här implementeringen. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Starta - `pageBottom` återanropsplacering | 0 | Funktionen `_satellite.pageBottom()` måste finnas för att taggar ska fungera. Lägg till det infogade skriptet omedelbart före den avslutande `</body>`-taggen för att säkerställa korrekt DTM-funktionalitet. Obs! Det är bäst att använda taggen som sista tagg i `<body>`. Om det hittas i taggen `<body>` kan det fungera, men eftersom det inte är en bra metod kan det fungera felaktigt eller med oväntade eller oönskade resultat. | Lägg till det infogade skriptet omedelbart före den avslutande `</body>`-taggen för att säkerställa korrekt DTM-funktionalitet. <br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - Self-Hosted | 0 | Taggbiblioteket finns på Adobe Akamai-instansen på `assets.adobedtm.com`. Självvärdande är det rekommenderade sättet att läsa in taggar eftersom det ger bättre kontroll över webbplatsens prestanda genom cachekontroll, minskar beroenden av skript från tredje part och ger större kontroll över publiceringsprocessen. Taggbibliotek kan hanteras via din egen webbhosting eller CDN. | Byt till en värdtjänst är ett sätt att läsa in taggar på en sida. Även om värdtjänster via Akamai CDN fungerar i de flesta fall förbättras sidprestanda av självvärdande tjänster. <br><br>Ytterligare information:<ul><li>[Snabbstartsguide för taggar](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Asynkron distribution](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - ska distribueras asynkront | 0 | Taggar ska distribueras asynkront för optimala prestanda. | Inkludera parametern `async` i det infogade skriptet för att säkerställa rätt taggfunktionalitet <br><br>[Ytterligare information](../../tags/ui/client-side/asynchronous-deployment.md) |
| Mål - Innehåll i `mboxDefault` | 0 | Innehållet ska finnas i `mboxDefault` när `at.js` används. | Kontrollera att innehållet är tillgängligt. <br><br>[Ytterligare information](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
