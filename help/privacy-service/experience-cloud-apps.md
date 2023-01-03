---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Privacy Service och Experience Cloud
topic-legacy: overview
description: Det här dokumentet innehåller en referens för hur du konfigurerar olika Experience Cloud-program för sekretessrelaterade åtgärder.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 5%

---

# [!DNL Privacy Service] och [!DNL Experience Cloud] program

Adobe Experience Platform [!DNL Privacy Service] har tagits fram för att stödja sekretessförfrågningar för flera Adobe Experience Cloud-program. Varje program har stöd för olika produktvärden och ID:n för att identifiera de registrerade.

Det här dokumentet fungerar som referens för [!DNL Experience Cloud] programdokumentation som visar hur du konfigurerar programmet för sekretessrelaterade åtgärder. Detta inkluderar hur du formaterar och etiketterar data. Det finns två typer av ansökningar:

* [Program som är integrerade med Privacy Servicen](#integrated): Program som kan skicka begäran om åtkomst, borttagning eller avanmälan till [!DNL Privacy Service].
* [Självbetjäningsprogram](#self-serve): Program som måste hantera sina sekretessförfrågningar internt och som inte kan kommunicera med [!DNL Privacy Service] direkt.

Läs dokumentationen till [!DNL Experience Cloud] program för att lära dig hur du formaterar dina sekretessförfrågningar och vilka värden som stöds för dessa förfrågningar.

## Program som är integrerade med [!DNL Privacy Service] {#integrated}

Här följer en lista med [!DNL Experience Cloud] program som är integrerade med [!DNL Privacy Service], inklusive [!DNL Privacy Service] funktioner som de är kompatibla med, deras protokoll för behandling av borttagningsbegäranden och länkar till dokumentation för mer information.

>[!NOTE]
>
>Alla integrerade produkter svarar på förfrågningar om sekretess inom 30 dagar eller mindre.

| Program | Åtkomst/borttagning | Avanmäl dig från försäljningen | Ta bort beteende | Dokumentation och andra överväganden |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | Den registrerades cookie-ID eller enhets-ID tas bort från systemet tillsammans med alla kostnads-, klick- och intäktsdata som är kopplade till cookien. | <ul><li>[Åtkomst/radering av dokumentation för GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Åtkomst-/borttagningsdokumentation för CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Dokumentation för avanmälan av försäljning för CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | If `analyticsDeleteMethod` utelämnas eller anges till `anonymize` När en sekretessförfrågan görs görs alla data som refereras av den angivna samlingen med användar-ID anonyma. If `analyticsDeleteMethod` är inställd på `purge`, tas alla data bort helt. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] hanterar avanmälningsbegäranden med [sekretessrapporteringsvariabler](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Alla egenskaper och segment som är associerade med Audience Manager-ID:t som ingår i begäran tas bort. Dessutom är respektive identifierare för den enskilda personen avanmäld från ytterligare datainsamling och respektive ID-mappningar tas bort. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Dokumentation om avanmälan](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=sv)</li><li>[Dokumentation om avanmälan](../segmentation/consents.md)</li></ul> |
| Adobe kundattribut (CRS) | ✓ | Ej tillämpligt | Den registrerades attribut tas bort från systemet. | <ul><li>[Åtkomst/radering av dokumentation för GDPR](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[Åtkomst-/borttagningsdokumentation för CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Kundattribut har inte möjlighet att överföra data, och därför kan du inte avanmäla dig från försäljning.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | När Experience Platform tar emot en begäran om borttagning från Privacy Servicen skickar Platform en bekräftelse till Privacy Servicen om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från datasjön eller profilarkivet när sekretessjobbet har slutförts. Innan jobbet är klart tas data bort på skärmen och är därför inte tillgängliga för någon plattformstjänst. | <ul><li>[Åtkomst/borttagningsdokumentation för datasjön](../catalog/privacy.md)</li><li>[Åtkomst/borttagning av dokumentation för identitetstjänsten](../identity-service/privacy.md)</li><li>[Åtkomst till/radera dokumentation för kundprofil i realtid](../profile/privacy.md)</li><li>[!DNL Experience Platform] honorar [avanmälningsbegäran för målgruppssegment](../segmentation/consents.md).</li></ul> |
| Adobe Primetime-autentisering | ✓ | Ej tillämpligt | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Åtkomst/borttagning av dokumentation](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] har inte möjlighet att överföra data, och därför är begäran om avanmälan från försäljning inte tillämplig.</li></ul> |
| Adobe Target | ✓ | Ej tillämpligt | Alla data som är kopplade till den registrerade personens ID tas bort från deras besökarprofil. Aggregerade eller anonyma uppgifter som inte identifierar den enskilda personen eller som på annat sätt är orelaterade (t.ex. innehållsdata) gäller inte för borttagningsförfrågningar. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] har inte möjlighet att överföra data, och därför är begäran om avanmälan från försäljning inte tillämplig.</li></ul> |
| Marketo Engage | ✓ | Ej tillämpligt | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] har inte möjlighet att överföra data, och därför är begäran om avanmälan från försäljning inte tillämplig.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Självbetjäningsprogram {#self-serve}

Här följer en lista med [!DNL Experience Cloud] program som inte är integrerade med [!DNL Privacy Service] och måste hantera sina integritetsfrågor internt. Det finns länkar till respektive programs dokumentation tillsammans med beskrivningar av dokumentationens innehåll.

| Program | Dokumentationsbeskrivning |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=sv) | Översikt över GDPR-funktioner för Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | En översikt över hur en administratör eller AEM kan hantera GDPR-begäranden. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Steg för att göra GDPR-åtkomst och ta bort begäranden med Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Se till att Magento Commerce installationer uppfyller kraven i specifik integritetslagstiftning. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Läs om hur sekretessbestämmelser gäller för Marketo. |
| [Taggar i Adobe Experience Platform](../tags/ui/client-side/consent.md) | Hur utvecklare kan använda tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan. |
| [Workfront](https://www.workfront.com/privacy-notice) | Läs om hur Workfront samlar in personuppgifter och hur den registrerade kan skicka in en begäran om integritet via ett formulär. |

{style=&quot;table-layout:auto&quot;}
