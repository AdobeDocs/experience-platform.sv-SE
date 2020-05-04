---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Integritetstjänst och Experience Cloud-program
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Integritetstjänst och Experience Cloud-program

Integritetstjänsten för Adobe Experience Platform är byggd för att stödja sekretessförfrågningar för flera Adobe Experience Cloud-program. Varje program har stöd för olika produktvärden och ID:n för att identifiera de registrerade.

Det här dokumentet fungerar som referens för Experience Cloud-programdokumentation som beskriver hur du konfigurerar det programmet för sekretessrelaterade åtgärder. Detta inkluderar hur du formaterar och etiketterar data. Det finns två typer av ansökningar:

* [Applikationer som är integrerade med Integritetstjänst](#integrated): Appar som kan skicka begäran om åtkomst, borttagning eller avanmälan till Integritetstjänst.
* [Självbetjäningsprogram](#self-serve): Appar som måste hantera sina sekretessförfrågningar internt och som inte kan kommunicera direkt med sekretesssystemet.

Läs dokumentationen för dina Experience Cloud-program för att lära dig hur du formaterar dina sekretessförfrågningar och vilka värden som stöds för dessa förfrågningar.

## Applikationer som är integrerade med Integritetstjänst {#integrated}

Nedan följer en lista över Experience Cloud-program som är integrerade med Integritetstjänst, inklusive de sekretessfunktioner de är kompatibla med och länkar till dokumentation för mer information.

| Program | Åtkomst/borttagning | Avanmäl dig från försäljningen | Dokumentation och överväganden |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Advertising Cloud utnyttjar de befintliga globala avanmälningsfunktionerna från Adobe Privacy Center. Mer information finns i guiden [om hur du begär](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) datasekretess.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>Analytics hanterar avanmälningsbegäranden med hjälp av [sekretessrapporteringsvariabler](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Dokumentation om avanmälan](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Dokumentation om avanmälan](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Åtkomst/borttagningsdokumentation för datasjön](../catalog/privacy.md)</li><li>[Åtkomst/radering av dokumentation för kundprofil i realtid](../profile/privacy.md)</li><li>Experience Platform uppfyller kraven på [avanmälan för målgruppssegment](../segmentation/honoring-opt-outs.md).</li></ul> |
| Adobe Primetime-autentisering | ✓ | Ej tillämpligt | <ul><li>[Åtkomst/borttagning av dokumentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime har inte möjlighet att överföra data, och därför är begäran om att avanmäla sig från försäljning inte tillämplig.</li></ul> |
| Adobe Target | ✓ | Ej tillämpligt | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>Target har inte möjlighet att överföra data, och därför är begäran om avanmälan från försäljning inte tillämplig.</li></ul> |

<!-- (To include once access/delete documentation is available)
Adobe Customer Attributes (CRS) | ✓ | N/A | <ul><li>Customer Attributes does not have the capability to transfer data, therefore opt-out-of-sale requests are not applicable.</li></ul>
-->

## Självbetjäningsprogram {#self-serve}

Nedan följer en lista över Experience Cloud-program som inte är integrerade med Integritetstjänst och som måste hantera sina integritetsfrågor internt. Det finns länkar till respektive programs dokumentation tillsammans med beskrivningar av dokumentationens innehåll.

| Program | Dokumentationsbeskrivning |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | En översikt över GDPR-funktioner för Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/en/dtm/using/tools/opt-in.html) | Steg för att förhindra att Adobe-taggar avfyras tills medgivande erhålls. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | En översikt över hur en kundsekretessadministratör eller AEM-administratör kan hantera GDPR-begäranden. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Steg för att göra GDPR-åtkomst och ta bort begäranden med Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Hur utvecklare kan använda tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan. |
