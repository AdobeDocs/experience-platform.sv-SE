---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Privacy Service och Experience Cloud
description: Det här dokumentet innehåller en referens för hur du konfigurerar olika Experience Cloud-program för sekretessrelaterade åtgärder.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: adc6d50f2784fe665d0590c3af053a057f8e4e38
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 4%

---

# [!DNL Privacy Service] och [!DNL Experience Cloud] program

Adobe Experience Platform [!DNL Privacy Service] har utformats för att stödja sekretessförfrågningar för flera Adobe Experience Cloud-program. Varje program har stöd för olika produktvärden och ID:n för att identifiera de registrerade.

Det här dokumentet fungerar som referens för [!DNL Experience Cloud]-programdokumentation som beskriver hur du konfigurerar det programmet för sekretessrelaterade åtgärder. Detta inkluderar hur du formaterar och etiketterar data. Det finns två typer av ansökningar:

* [Program som är integrerade med Privacy Service](#integrated): Program som kan skicka begäran om åtkomst, borttagning eller avanmälan till [!DNL Privacy Service].
* [Självbetjäningsprogram](#self-serve): Program som måste hantera sina sekretessförfrågningar internt och som inte kan kommunicera direkt med [!DNL Privacy Service].

Läs igenom dokumentationen för dina [!DNL Experience Cloud]-program för att lära dig hur du formaterar dina sekretessförfrågningar och vilka värden som stöds för dessa förfrågningar.

## Program integrerade med [!DNL Privacy Service] {#integrated}

Nedan följer en lista över [!DNL Experience Cloud] program som är integrerade med [!DNL Privacy Service], inklusive de [!DNL Privacy Service]-funktioner som de är kompatibla med, deras protokoll för behandling av borttagningsbegäranden och länkar till dokumentation för mer information.

>[!NOTE]
>
>Alla integrerade produkter svarar på förfrågningar om sekretess inom 30 dagar eller mindre.

| Program | Åtkomst/borttagning | Avanmäl dig från försäljningen | Ta bort beteende | Dokumentation och andra överväganden |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | Den registrerades cookie-ID eller enhets-ID tas bort från systemet tillsammans med alla kostnads-, klick- och intäktsdata som är kopplade till cookien. | <ul><li>[Åtkomst/borttagningsdokumentation för GDPR](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Åtkomst/borttagningsdokumentation för CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Dokumentation om avanmälan för CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics tillhandahåller verktyg för märkning av data utifrån dess känslighet och avtalsbegränsningar. Etiketter är ett viktigt steg för:<ol><li>Identifiera registrerade personer.</li><li>Avgör vilka data som ska returneras som en del av en åtkomstbegäran.</li><li>Identifierar datafält som måste tas bort som en del av en raderingsbegäran.</li></ol> | <ul><li>[Sekretessarbetsflöde](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Analysetikett](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Analysalternativ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Alla egenskaper och segment som är kopplade till Audience Manager-identifieraren som ingår i begäran tas bort. Dessutom är respektive identifierare för den enskilda personen avanmäld från ytterligare datainsamling och respektive ID-mappningar tas bort. | <ul><li>[Åtkomst](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [ta bort](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data) dokumentation</li><li>[Avanmäl dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[Avanmäl förfrågningar](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Sekretesshantering](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=sv).</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=sv)</li><li>[Avanmäl dokumentation](../segmentation/tutorials/consents.md)</li></ul> |
| Adobe kundattribut (CRS) | ✓ | N/A | Den registrerades attribut tas bort från systemet. | <ul><li>[Åtkomst/borttagningsdokumentation för GDPR](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[Åtkomst/borttagningsdokumentation för CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Kundattribut har inte möjlighet att överföra data, och därför kan du inte avanmäla dig från försäljning.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | När Experience Platform tar emot en borttagningsbegäran från Privacy Service skickar Platform en bekräftelse till Privacy Service om att begäran har tagits emot och att data som påverkas har markerats för borttagning. Posterna tas sedan bort från datasjön eller profilarkivet när sekretessjobbet har slutförts. Innan jobbet är klart tas data bort på skärmen och är därför inte tillgängliga för någon plattformstjänst. | <ul><li>[Åtkomst/borttagningsdokumentation för datasjön](../catalog/privacy.md)</li><li>[Åtkomst/borttagning av dokumentation för identitetstjänsten](../identity-service/privacy.md)</li><li>[Åtkomst/borttagning av dokumentation för kundprofil i realtid](../profile/privacy.md)</li><li>[!DNL Experience Platform] följer [avanmälningsbegäranden för målgruppssegment](../segmentation/tutorials/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N/A | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass-autentisering | ✓ | N/A | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Åtkomst/borttagning av dokumentation](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Godkännandet har inte möjlighet att överföra data, och därför är begäran om att avanmäla sig från försäljning inte tillämplig.</li></ul> |
| Adobe Target | ✓ | N/A | Alla data som är kopplade till den registrerade personens ID tas bort från deras besökarprofil. Aggregerade eller anonyma uppgifter som inte identifierar den enskilda personen eller som på annat sätt är orelaterade (t.ex. innehållsdata) gäller inte för borttagningsförfrågningar. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] har inte möjlighet att överföra data och därför kan du inte välja bort från försäljning.</li></ul> |
| Commerce (Personalization) | ✓ | N/A | Privacy Service tar bort [!DNL Commerce] data som lagras i Commerce SaaS-tjänster för marknadsföringsändamål, vilket innebär att profiler och beställningar av registrerade inte längre skickas till Adobe marknadsföringsprogram för användning i kampanjer och kundresor. Privacy Service tar dock inte bort data i programmet [!DNL Commerce] eftersom det fortfarande kan behövas för handelstransaktionsbehov. Handlare ansvarar för alla begäranden om borttagning/åtkomst av data i programmet [!DNL Commerce]. | <ul><li>[Åtkomst/borttagning av dokumentation för Commerce](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | N/A | Den registrerades lagrade data tas bort från systemet. | <ul><li>[Åtkomst/borttagning av dokumentation](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] har inte möjlighet att överföra data och därför kan du inte välja bort från försäljning.</li></ul> |

{style="table-layout:auto"}

## Självbetjäningsprogram {#self-serve}

Nedan följer en lista över [!DNL Experience Cloud]-program som inte är integrerade med [!DNL Privacy Service] och som måste hantera sina integritetsproblem internt. Det finns länkar till respektive programs dokumentation tillsammans med beskrivningar av dokumentationens innehåll.

| Program | Dokumentationsbeskrivning |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | En översikt över hur en kundsekretessadministratör eller AEM-administratör kan hantera GDPR-begäranden. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Steg för att göra GDPR-åtkomst och ta bort begäranden med Livefyre. |
| [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/overview) | Se till att era Adobe Commerce-installationer uppfyller kraven i specifik integritetslagstiftning. |
| [Taggar i Adobe Experience Platform](../tags/ui/client-side/consent.md) | Hur utvecklare kan använda tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan. |
| [Workfront](https://www.workfront.com/privacy-notice) | Läs om hur Workfront samlar in personuppgifter och hur den registrerade kan skicka in en begäran om integritet via ett formulär. |

{style="table-layout:auto"}
