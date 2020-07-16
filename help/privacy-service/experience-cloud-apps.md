---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service och Experience Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 9%

---


# [!DNL Privacy Service] och [!DNL Experience Cloud] program

Adobe Experience Platform [!DNL Privacy Service] har tagits fram för att stödja sekretessförfrågningar för flera Adobe Experience Cloud-program. Varje program har stöd för olika produktvärden och ID:n för att identifiera de registrerade.

Det här dokumentet fungerar som referens för [!DNL Experience Cloud] programdokumentation som beskriver hur du konfigurerar programmet för sekretessrelaterade åtgärder. Detta inkluderar hur du formaterar och etiketterar data. Det finns två typer av ansökningar:

* [Program som är integrerade med Privacy Servicen](#integrated): Program som kan skicka begäran om åtkomst, borttagning eller avanmälan till [!DNL Privacy Service].
* [Självbetjäningsprogram](#self-serve): Program som måste hantera sina sekretessförfrågningar internt och som inte kan kommunicera [!DNL Privacy Service] direkt.

Läs igenom dokumentationen för dina [!DNL Experience Cloud] program för att lära dig hur du formaterar dina sekretessförfrågningar och vilka värden som stöds för dessa förfrågningar.

## Program som är integrerade med [!DNL Privacy Service] {#integrated}

Nedan följer en lista med program som är integrerade med [!DNL Experience Cloud] , inklusive de [!DNL Privacy Service][!DNL Privacy Service] funktioner som de är kompatibla med och länkar till dokumentation för mer information.

| Program | Åtkomst/borttagning | Avanmäl dig från försäljningen | Dokumentation och överväganden |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>[!DNL Advertising Cloud] utnyttjar befintliga funktioner för global avanmälan från Adobe Privacy Center. Mer information finns i guiden [om hur du begär](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) datasekretess.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] hanterar avanmälningsbegäranden med hjälp av variabler för [sekretessrapportering](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Dokumentation om avanmälan](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[Dokumentation om avanmälan](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobes kundattribut (CRS) | ✓ | Ej tillämpligt | <ul><li>[Åtkomst/radering av dokumentation för GDPR](https://docs.adobe.com/content/help/sv-SE/core-services/interface/customer-attributes/gdpr.html)</li><li>[Åtkomst-/borttagningsdokumentation för CCPA](https://docs.adobe.com/content/help/sv-SE/core-services/interface/customer-attributes/ccpa.html)</li><li>Kundattribut har inte möjlighet att överföra data, och därför kan du inte avanmäla dig från försäljning.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Åtkomst/borttagningsdokumentation för datasjön](../catalog/privacy.md)</li><li>[Åtkomst/radering av dokumentation för kundprofil i realtid](../profile/privacy.md)</li><li>[!DNL Experience Platform] uppfyller [avanmälningsbegäranden för målgruppssegment](../segmentation/honoring-opt-outs.md).</li></ul> |
| Adobe Primetime-autentisering | ✓ | Ej tillämpligt | <ul><li>[Åtkomst/borttagning av dokumentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] har inte möjlighet att överföra data, och därför är begäran om avanmälan från försäljning inte tillämplig.</li></ul> |
| Adobe Target | ✓ | Ej tillämpligt | <ul><li>[Åtkomst/borttagning av dokumentation](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] har inte möjlighet att överföra data, och därför är begäran om avanmälan från försäljning inte tillämplig.</li></ul> |


## Självbetjäningsprogram {#self-serve}

Nedan följer en lista över [!DNL Experience Cloud] program som inte är integrerade med [!DNL Privacy Service] och som måste hantera sina integritetsfrågor internt. Det finns länkar till respektive programs dokumentation tillsammans med beskrivningar av dokumentationens innehåll.

| Program | Dokumentationsbeskrivning |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | En översikt över GDPR-funktionerna för Adobe Campaign Classic. |
| [Adobe Dynamic Tag Manager](https://docs.adobe.com/content/help/sv-SE/dtm/using/tools/opt-in.html) | Steg för att förhindra att Adobe-taggar avfyras tills medgivande erhålls. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | En översikt över hur en kundsekretessadministratör eller AEM-administratör kan hantera GDPR-begäranden. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Steg för att göra GDPR-åtkomst och ta bort begäranden med Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Hur utvecklare kan använda tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan. |
