---
title: Stöd för IAB TCF 2.0 i Adobe Experience Platform Web SDK
description: Lär dig hur du stöder IAB TCF 2.0-medgivanden med Adobe Experience Platform Web SDK
keywords: samtycke;setConsent;Profile Privacy Field group;Experience Event Privacy Field group;Privacy Field group;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Stöd för IAB TCF 2.0 i Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK har stöd för Interactive Advertising Bureau Transparency &amp; Consent Framework, version 2.0 (IAB TCF 2.0). Den här guiden visar kraven för stöd av IAB TCF 2.0 via Adobe Experience Platform Web SDK som är integrerat med Adobe Real-Time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics och Edge Network.

Följande handböcker är dessutom tillgängliga för att lära dig hur du integrerar IAB TCF 2.0 med och utan taggar.

- [Med taggar](./with-tags.md)
- [Utan taggar](./without-tags.md)

## Komma igång

För att kunna implementera Web SDK med IAB TCF 2.0 måste du ha en fungerande förståelse för Experience Data Model (XDM) och Experience Events. Läs följande dokument innan du börjar:

- [Systemöversikt för XDM (Experience Data Model)](../../../xdm/home.md): Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [!DNL Experience Data Model (XDM)], som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

## Integrering med Experience Platform

Följande krävs för att skicka data om samtycke till Adobe Experience Platform med SDK:

- En datauppsättning vars schema baseras på klassen [!DNL XDM Individual Profile] och innehåller TCF 2.0-tillståndsfält, som är aktiverade för användning i [!DNL Real-Time Customer Profile].
- En datastream som har konfigurerats med Experience Platform och den profilaktiverade datauppsättning som nämns ovan.

I guiden om [TCF 2.0-kompatibilitet](../../../landing/governance-privacy-security/consent/iab/overview.md) finns instruktioner om hur du skapar de nödvändiga datauppsättningarna och dataströmmen.

## Integrering med Audience Manager

Adobe Audience Manager (AAM) har stöd för IAB TCF 2.0, som gör att du kan utvärdera, följa och vidarebefordra kundsekretessval till partners längre fram i kedjan. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Om du vill integrera med Audience Manager via Adobe Experience Platform Web SDK måste du ha en datastream som kan vidarebefordras till Adobe Audience Manager.

## Experience Events och integrering med Adobe Analytics

Medan målgrupperna i Real-Time CDP och Audience Manager håller reda på kundernas aktuella medgivandepreferenser kan Experience Events göra en kunds medgivandepreferenser som var aktiva när händelsen samlades in.

Följande krävs för att samla in information om samtycke vid händelser:

- En datamängd baserad på klassen [!DNL XDM Experience Event], med fältgruppen [!DNL Experience Event] för sekretesschema.
- En datastream har konfigurerats med datauppsättningen [!DNL XDM Experience Event] ovan.

Mer information om hur du konverterar en XDM Experience Event till en Analytics-träff finns i [Skicka data till Adobe Analytics med Web SDK](/help/web-sdk/use-cases/adobe-analytics.md).

## Integrering med Adobe Experience Platform Web SDK

Avsnitten nedan beskriver de viktigaste integrationspunkterna mellan IAB TCF 2.0 och Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Även om du inte har Real-Time CDP eller Audience Manager kan du integrera IAB TCF 2.0 med Web SDK. Medgivandeinställningarna kan användas för att styra samlingen av upplevelsehändelser och för att ange en identitetscookie.

### Standardsamtycke

Standardsamtycke används när det inte redan finns någon inställning för samtycke för en kund. Det innebär att standardalternativen för samtycke kan styra Adobe Experience Platform Web SDK och ändra deras beteende beroende på kundens region.

Om du till exempel har en kund som inte omfattas av den allmänna dataskyddsförordningen (GDPR) kan standardmedgivandet anges till `in`, men inom GDPR:s jurisdiktion kan standardmedgivandet anges till `pending`. Din CMP (Consent Management Platform) kan identifiera kundens region och tillhandahålla flaggan `gdprApplies` till IAB TCF 2.0. Den här flaggan kan användas för att ange standardsamtycke. Mer information finns i [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md).

### Ange samtycke när det ändras

Adobe Experience Platform Web SDK har ett `setConsent`-kommando som meddelar dina kunders samtycke till alla Adobe-tjänster med IAB TCF 2.0. Om du integrerar med Real-Time CDP uppdateras kundens profil. Om du integrerar med Audience Manager uppdateras kundinformationen. Om du anropar detta anges även en cookie med en medgivandeinställning som helt eller inte alls som kontrollerar om framtida Experience Events får skickas. Den här åtgärden anropas när medgivandet ändras. Vid framtida sidinläsningar läses Edge Network cookie för godkännande in för att avgöra om Experience Events kan skickas och om en identitetscookie kan anges.

På samma sätt som för Audience Manager IAB TCF 2.0-integrering ger Edge Network sitt medgivande när en kund uttryckligen har gett sitt medgivande för följande syften:

- **Syfte 1:** Lagra och/eller få åtkomst till information på en enhet
- **Syfte 10:** Utveckla och förbättra produkter
- **Särskilt syfte 1:** Säkerställ säkerhet, förhindra bedrägeri och felsökning. (Enligt reglerna för IAB TCF godkänner detta alltid)
- **Adobe leverantörsbehörighet:** Medgivande för Adobe (leverantör 565)

Mer information om kommandot `setConsent` finns i den dedikerade Web SDK-dokumentationen om [setConsent](../../../web-sdk/commands/setconsent.md).

### Lägga till samtycke till upplevelsehändelser

Adobe Experience Platform Web SDK har ett [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md)-kommando som samlar in en Experience Event. Om du integrerar med Experience Events eller Adobe Analytics och vill ha medgivandeinställningarna för varje Experience Event, lägger du till medgivandeinformation för varje `sendEvent`-kommando.

## Nästa steg

Nu när du har en grundläggande förståelse för IAB Transparency &amp; Consent Framework 2.0 kan du läsa någon av guiderna för användning av IAB TCF 2.0 [med taggar](./with-tags.md) eller [utan taggar](./without-tags.md).
