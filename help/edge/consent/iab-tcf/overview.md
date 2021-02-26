---
title: Stöd för IAB TCF 2.0 i Adobe Experience Platform Web SDK
description: Lär dig hur du kan använda IAB TCF 2.0-medgivandeinställningar med Adobe Experience Platform Web SDK
keywords: samtycke;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: 1c6238a0cf72230e019fd10d9a72f30444bd9fb9
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---


# Stöd för IAB TCF 2.0 i Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK har stöd för Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). Den här guiden visar kraven för stöd av IAB TCF 2.0 via Adobe Experience Platform Web SDK som är integrerat med kunddataplattformen, Audience Manager, Experience Events, Adobe Analytics och Experience Edge i realtid.

Dessutom finns följande handledningar som kan användas för att lära sig hur man integrerar IAB TCF 2.0 med och utan Adobe Experience Platform Launch.

- [Med Adobe Experience Platform Launch](./with-launch.md)
- [Utan Adobe Experience Platform Launch](./without-launch.md)

## Komma igång

För att kunna implementera Web SDK med IAB TCF 2.0 måste du ha en fungerande förståelse för Experience Data Model (XDM) och Experience Events. Läs följande dokument innan du börjar:

- [Experience Data Model (XDM) - systemöversikt](../../../xdm/home.md): Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [!DNL Experience Data Model (XDM)]som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

## Integrering med Experience Platform

Om du vill skicka data om samtycke till Adobe Experience Platform med hjälp av SDK krävs följande:

- En datauppsättning vars schema baseras på klassen [!DNL XDM Individual Profile] och innehåller TCF 2.0-tillståndsfält, som är aktiverade för användning i [!DNL Real-time Customer Profile].
- En edge-konfiguration som har konfigurerats med Platform och den profilaktiverade datauppsättning som nämns ovan.

Se guiden [TCF 2.0-kompatibilitet](../../../landing/governance-privacy-security/consent/iab/overview.md) för instruktioner om hur du skapar de nödvändiga datauppsättningarna och edge-konfigurationen.

## Integrering med Audience Manager

Adobe Audience Manager (AAM) har stöd för IAB TCF 2.0, som gör att du kan utvärdera, följa och vidarebefordra kundsekretessval till partners i senare led. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Om du vill integrera med Audience Manager via Adobe Experience Platform Web SDK måste du ha en edge-konfiguration som är konfigurerad att vidarebefordra till Adobe Audience Manager.

## Experience Events och integrering med Adobe Analytics

Medan CDP och Audience Manager-målgrupperna i realtid håller reda på en kunds nuvarande medgivandepreferenser, kan Experience Events behålla en kunds medgivandepreferenser som var aktiva när händelsen samlades in.

Följande krävs för att samla in information om samtycke vid händelser:

- En datauppsättning som baseras på klassen [!DNL XDM Experience Event] med [!DNL Experience Event]-integritetsmixin.
- En edge-konfiguration konfigurerad med [!DNL XDM Experience Event]-datauppsättningen ovan.

Mer information om hur du konverterar en XDM Experience Event till en Analytics-träff får du om du börjar med att läsa dokumentationen till [Analytics overview](../../data-collection/adobe-analytics/analytics-overview.md).

## Integrering med Adobe Experience Platform Web SDK

Avsnitten nedan beskriver de viktigaste integrationspunkterna mellan IAB TCF 2.0 och Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Även om du inte har konfigurerat CDP eller Audience Manager i realtid kan du ändå integrera IAB TCF 2.0 med Web SDK. Medgivandeinställningarna kan användas för att styra samlingen av upplevelsehändelser och för att ange en identitetscookie.

### Standardsamtycke

Standardsamtycke används när det inte finns någon inställning för samtycke som redan har sparats för en kund. Det innebär att standardalternativen för samtycke kan styra Adobe Experience Platform Web SDK:s beteende och ändra baserat på kundens region.

Om du till exempel har en kund som inte omfattas av den allmänna dataskyddsförordningen (GDPR), kan standardmedgivandet anges till `in`, men inom GDPR:s jurisdiktion, kan standardmedgivandet anges till `pending`. Din CMP (Consent Management Platform) kan identifiera kundens region och ange flaggan `gdprApplies` till IAB TCF 2.0. Den här flaggan kan användas för att ange standardsamtycke.

Mer information om standardsamtycke finns i [standardavsnittet för samtycke](../../fundamentals/configuring-the-sdk.md#default-consent) i SDK-konfigurationsdokumentationen.

### Ange samtycke när det ändras

Adobe Experience Platform Web SDK har ett `setConsent`-kommando som meddelar dina kunders medgivandepreferenser till alla Adobe-tjänster med IAB TCF 2.0. Om du integrerar med CDP i realtid uppdateras kundens profil. Om du integrerar med Audience Manager uppdateras kundinformationen. Om du anropar detta anges även en cookie med en medgivandeinställning som helt eller inte alls som kontrollerar om framtida Experience Events får skickas. Den här åtgärden anropas när medgivandet ändras. Vid framtida sidinläsningar läses cookien för Experience Edge-medgivande in för att avgöra om Experience Events kan skickas och om en identitetscookie kan anges.

På samma sätt som för integreringen med Audience Manager IAB TCF 2.0 ger Experience Edge sitt medgivande när en kund har gett sitt uttryckliga medgivande för följande syften:

- **Syfte 1:** Lagra och/eller få åtkomst till information på en enhet
- **Syfte 10:** Utveckla och förbättra produkter
- **Särskilt syfte 1:** Säkerställ säkerhet, förhindra bedrägeri och felsökning. (Enligt reglerna för IAB TCF godkänner detta alltid)
- **Adobe leverantörstillstånd:** samtycke för Adobe (leverantör 565)

Mer information om kommandot `setConsent` finns i dokumentationen om [Supporting Consent](../../consent/supporting-consent.md).

### Lägga till samtycke till upplevelsehändelser

Adobe Experience Platform Web SDK har ett `sendEvent`-kommando som samlar in en Experience Event. Om du integrerar med Experience Events eller Adobe Analytics och vill ha medgivandeinställningarna för varje Experience Event bör du lägga till medgivandeinformationen för varje `sendEvent`-kommando.

Mer information om kommandot `sendEvent` finns i dokumentationen om [spårningshändelser](../../fundamentals/tracking-events.md).

## Nästa steg

Nu när du har en grundläggande förståelse för IAB Transparency &amp; Consent Framework 2.0 kan du läsa någon av guiderna för användning av IAB TCF 2.0 [med Adobe Experience Platform Launch](./with-launch.md) eller [utan Adobe Experience Platform Launch](./without-launch.md).
