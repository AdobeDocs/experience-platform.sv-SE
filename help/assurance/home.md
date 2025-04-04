---
title: Adobe Experience Platform Assurance - översikt
description: Med Adobe Experience Platform Assurance kan du inspektera, korrekturläsa, simulera och validera hur du samlar in data eller levererar upplevelser i dina mobilapplikationer.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance är en produkt från [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) som hjälper dig att inspektera, verifiera, simulera och validera hur du samlar in data eller levererar upplevelser i din mobilapp.

>[!IMPORTANT]
>
> Project Griffon kallas nu **Assurance**!
>
> Project Griffon är nu allmänt tillgängligt för **alla** Adobe Experience Cloud-kunder som Assurance. Läs [användaråtkomstguiden](./user-access.md) om du vill veta mer om övergången.

>[!INFO]
>
>Assurance publika API:er är tillgängliga!
>
>[Assurance API:er](https://developer.adobe.com/adobe-assurance-public-apis/) är en samling API:er som gör det möjligt för användare att testa och felsöka webb- och mobilappar när de är utrustade med Adobe Assurance Mobile SDK.

## Allmän tillgänglighet

Från och med 15 oktober 2022 är Assurance allmänt tillgängligt för alla Adobe Experience Cloud.

### Vad förändras?

15 oktober - åtkomst till Assurance hanteras via Admin Console. Läs [användaråtkomstguiden](./user-access.md) för att försäkra dig om att du har fortsatt tillgång utan avbrott.

Inga andra förändringar eller avbrott förväntas i befintliga Assurance-integreringar, sessioner och evenemang. Du kan fortfarande få åtkomst till Assurance via [https://griffon.adobe.com](https://griffon.adobe.com) **eller** som du kan använda (och bokmärke) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Vad kan Assurance göra för dig?

### Snabbinställningar

Kom igång snabbt med några rader kod. För mobilappar arbetar Assurance tillsammans med Adobe Experience Platform Mobile SDK för att hjälpa dig inspektera, simulera och validera apphändelser, platssignaler, konfigurationsparametrar, SDK-loggar, enhetsinformation med mera.

### Smidig anslutning

Med Assurance är det enkelt och tillförlitligt att ansluta appen till Experience Platform. Du behöver inte använda nätverksproxies, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) eller andra nätverksgymnaster - det är lika enkelt att ansluta appen till Assurance som att skanna en QR-kod eller trycka på en knapp.

![](./images/index/no-hassle-connection.png)

### Realtidsinspektion, simulering och validering

När du har anslutit till Assurance kan du inspektera live-strömmade programhändelser och -aktiviteter och filtrera och söka för att eliminera brus. Händelser innehåller information om validering, felsökning och felsökning av implementeringen av din mobilapp. Med Assurance kan du även göra skärmdumpar, simulera platssignaler och mycket mer i realtid.

![](./images/index/real-time-insepction.png)

### Integrering med Adobe Experience Cloud

Data och upplevelser på klientsidan sätts i ett sammanhang där användarna skapar rapporteringsregler, aktiviteter och kampanjer utifrån våra marknadsföringsfokuserade användargränssnitt. För att du ska få möjlighet att koppla samman är vi integrerade med Adobe Experience Cloud lösningar som Adobe Experience Platform, Adobe Analytics, Adobe Target, Platstjänst med flera.

![](./images/index/integration.png)

## Funktioner

### Adobe Experience Platform Mobile SDK Events, loggar med mera

Med Assurance kan du inspektera SDK råa-händelser som genererats av Adobe Experience Platform Mobile SDK. Alla evenemang som samlas in av SDK kan granskas. SDK-händelser läses in i en listvy, sorterade efter tid. Varje händelse har en detaljerad vy som ger mer information. Det finns även ytterligare vyer för att bläddra bland SDK-konfigurationer, dataelement, delade lägen och SDK-tilläggsversioner.

### Adobe Analytics

Vyn Adobe Analytics > Analyshändelser är en fokuserad vy som visar händelser relaterade till din mobilimplementering i Adobe Analytics. I listvyn visas livscykeln eller händelse-/tillståndshändelsen, &quot;status&quot; efter bearbetning, tillsammans med nödvändig händelseinformation i en särskilt formaterad vy. Statusen Efterbearbetad visar hur händelsen bearbetades av Adobe Analytics efter att regler för händelsebearbetning har tillämpats.

### Adobe Analytics for Streaming Media

I vyn Adobe Analytics > Media Analytics Events (Media Analytics-händelser) visas händelser för implementeringen av ljud- och videoanalys. Händelsedetaljvyn visar standardmetadata och anpassade metadata som spåras för varje uppspelningssession. Dessutom kan du visa efterbearbetad status och efterbearbetade medieanalysdata, t.ex. hur mycket medietid som spenderas eller den totala buffertlängden.

### Platser (Location Services)

Positioneringstjänstvyn är en vy på enheten som visar användarens plats- och avslutningshändelser för enkel validering. I den här praktiska vyn får du ett praktiskt gränssnitt där du kan se var specifika datapunkter finns för att inspektera klienten för kontextfelsökning.

## Är Assurance säkert?

Assurance har följande säkerhetsåtgärder:

* Både Assurance och Assurance webbgränssnitt har en säker, PIN-baserad handskakning för en anslutning. Användaren måste explicit skapa en handskakning som förhindrar att&quot;oavsiktliga&quot; Assurance-anslutningar skapas av en slutanvändare.
* Endast anslutningar mellan Assurance och Assurance webbgränssnitt som tillhör samma Adobe Experience Cloud Organization ID stöds.
* Adobe Experience Platform Mobile SDKs-händelser överförs via HTTPS.
* Assurance och Adobe Experience Platform Mobile SDK använder TLS 1.2
* Assurance-sessioner tas bort efter 30 dagar.
* Assurance sessionsdata krypteras i vila enligt bästa praxis för lagring.

## Komma igång

Om du vill konfigurera Assurance måste du först installera Assurance-tillägget i ditt program. Om du vill veta hur du gör det läser du självstudiekursen om hur du [implementerar Assurance-tillägget](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

När du har lagt till Assurance i appen kan du skapa en Assurance-session som kan anslutas till din enhet. Läs [handboken om hur du använder Assurance](./tutorials/using-assurance.md) om du vill lära dig hur du använder Assurance.
