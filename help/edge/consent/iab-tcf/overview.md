---
title: Översikt över IAB Transparency & Consent Framework 2.0
seo-title: Stöd för Adobe Experience Platform Web SDK-medgivanden från Interactive Advertising Bureau Transparency & Consent Framework 2.0
description: Lär dig hur du stöder IAB TCF 2.0-medgivanden med Experience Platform Web SDK
seo-description: Lär dig hur du stöder IAB TCF 2.0-medgivanden med Experience Platform Web SDK
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---


# Översikt över IAB Transparency &amp; Consent Framework 2.0

Adobe Experience Platform Web SDK (AEP Web SDK) har stöd för Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). Den här guiden visar kraven för stöd av IAB TCF 2.0 via AEP Web SDK som integreras med kunddataplattformen, Audience Manager, Experience Events, Adobe Analytics och Experience Edge i realtid.

Dessutom finns följande handledningar som kan användas för att lära sig hur man integrerar IAB TCF 2.0 med och utan Adobe Experience Platform Launch.

- [Med Adobe Experience Platform Launch](./with-launch.md)
- [Utan Adobe Experience Platform Launch](./without-launch.md)

## Komma igång

För att kunna implementera AEP Web SDK med IAB TCF 2.0 måste du ha en fungerande förståelse för Experience Data Model (XDM) och Experience Events. Läs följande dokument innan du börjar:

- [Experience Data Model (XDM) - systemöversikt](../../../xdm/home.md): Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [!DNL Experience Data Model (XDM)]som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

## Integrering av kunddataplattform i realtid

Adobe kunddataplattform i realtid (CDP i realtid) bygger på Adobe Experience Platform och hjälper er att samla in kända och anonyma data från flera olika företagskällor. På så sätt kan ni skapa kundprofiler som kan användas för att leverera personaliserade kundupplevelser över alla kanaler och enheter i realtid. Följande krävs för att skicka data om samtycke till CDP i realtid via AEP Web SDK:

- En datauppsättning som baseras på [!DNL XDM Individual Profile] klassen, som är aktiverad för användning i [!DNL Real-time Customer Profile], med integritetsmixen för profiler.
- En edge-konfiguration som har konfigurerats med CDP i realtid och den profildatauppsättning som nämns ovan.

Se självstudiekursen om [hur du skapar datauppsättningar för att hämta TCF 2.0-samtycke](../../../rtcdp/privacy/iab/dataset-preparation.md) för hur du skapar den önskade datauppsättningen.

Mer information om hur du skapar edge-konfigurationen finns i [IAB TCF 2.0-kompatibilitetsöversikten](../../../rtcdp/privacy/privacy-overview.md) .

## Integrering med Audience Manager

Adobe Audience Manager (AAM) har stöd för IAB TCF 2.0, som gör att du kan utvärdera, följa och vidarebefordra kundsekretessval till partners i senare led. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Om du vill integrera med Audience Manager via AEP Web SDK måste du ha en edge-konfiguration som är konfigurerad att vidarebefordra till Adobe Audience Manager.

## Experience Events och integrering med Adobe Analytics

Medan CDP och Audience Manager-målgrupperna i realtid håller reda på en kunds nuvarande medgivandepreferenser, kan Experience Events behålla en kunds medgivandepreferenser som var aktiva när händelsen samlades in.

Följande krävs för att samla in information om samtycke vid händelser:

- En datauppsättning baserad på [!DNL XDM Experience Event] klassen, med [!DNL Experience Event] integritetsmixin.
- En edge-konfiguration som har konfigurerats med [!DNL XDM Experience Event] datauppsättningen ovan.

Mer information om hur du konverterar en XDM Experience Event till en Analytics-träff får du genom att läsa [översiktsdokumentationen](../../data-collection/adobe-analytics/analytics-overview.md) för Analytics.

## Integrering med AEP Web SDK

Avsnitten nedan beskriver de viktigaste integrationspunkterna mellan IAB TCF 2.0 och AEP Web SDK.

>[!NOTE]
>
>Även om du inte har konfigurerat CDP eller Audience Manager i realtid kan du ändå integrera IAB TCF 2.0 med Web SDK. Medgivandeinställningarna kan användas för att styra samlingen av upplevelsehändelser och för att ange en identitetscookie.

### Standardsamtycke

Standardsamtycke används när det inte finns någon inställning för samtycke som redan har sparats för en kund. Det innebär att standardalternativen för samtycke kan styra beteendet för AEP Web SDK och ändra baserat på kundens region.

Om du till exempel har en kund som inte omfattas av den allmänna dataskyddsförordningen (GDPR) kan standardmedgivandet anges till `in`, men inom GDPR:s jurisdiktion, kan standardmedgivandet anges till `pending`. Din molnhanteringsplattform (CMP) kan identifiera kundens region och ge flaggan `gdprApplies` till IAB TCF 2.0. Den här flaggan kan användas för att ange standardsamtycke.

Mer information om standardmedgivande finns i avsnittet [om](../../fundamentals/configuring-the-sdk.md#default-consent) standardmedgivande i SDK-konfigurationsdokumentationen.

### Ange samtycke när det ändras

AEP Web SDK har ett `setConsent` kommando som meddelar dina kunders samtycke till alla Adobe-tjänster med hjälp av IAB TCF 2.0. Om du integrerar med CDP i realtid uppdateras kundens profil. Om du integrerar med Audience Manager uppdateras kundinformationen. Om du anropar detta anges även en cookie med en medgivandeinställning som helt eller inte alls som kontrollerar om framtida Experience Events får skickas. Den här åtgärden anropas när medgivandet ändras. Vid framtida sidinläsningar läses cookien för Experience Edge-medgivande in för att avgöra om Experience Events kan skickas och om en identitetscookie kan anges.

På samma sätt som för integreringen med Audience Manager IAB TCF 2.0 ger Experience Edge sitt medgivande när en kund har gett sitt uttryckliga medgivande för följande syften:

- **Syfte 1:** Lagra och/eller få åtkomst till information på en enhet
- **Syfte 10:** Utveckla och förbättra produkter
- **Specialsyfte 1:** Säkerställ säkerhet, förhindra bedrägeri och felsökning. (Enligt reglerna för IAB TCF godkänner detta alltid)
- **Adobe:** Godkännande för Adobe (leverantör 565)

Mer information om `setConsent` kommandot finns i dokumentationen [Supporting Consent](../../consent/supporting-consent.md).

### Lägga till samtycke till upplevelsehändelser

AEP Web SDK har ett `sendEvent` kommando som samlar in en Experience Event. Om ni integrerar med Experience Events eller Adobe Analytics och vill ha medgivandeinställningarna för varje Experience Event bör ni lägga till medgivandeinformationen för varje `sendEvent` kommando.

Mer information om `sendEvent` kommandot finns i dokumentationen om [spårningshändelser](../../fundamentals/tracking-events.md).

## Nästa steg

Nu när du har en grundläggande förståelse för IAB Transparency &amp; Consent Framework 2.0 kan du läsa någon av guiderna för användning av IAB TCF 2.0 [med Adobe Experience Platform Launch](./with-launch.md) eller [utan Adobe Experience Platform Launch](./without-launch.md).
